# Process Profile Rules

## Demo

Create `neuvector-demo-2` namespace

```bash
kubectl apply -f 01-ns-neuvector-demo-2.yaml
namespace/neuvector-demo-2 created
```

Create a group `nv.sle-bci.neuvector-demo-2` where process `cat` is allowed

```bash
kubectl apply -f 02-nv.sle-bci.neuvector-demo-2.yaml
nvsecurityrule.neuvector.com/nv.sle-bci.neuvector-demo-2 created
```

Create pod `sle-bci-test` in namespace `neuvector-demo-2` (will be member of `nv.sle-bci.neuvector-demo-2`)

```bash
kubectl apply -f 03-sle-bci-pod.yaml
pod/sle-bci-test created
```

Exec into the pod and run `cat`

```bash
kubectl exec -n neuvector-demo-2 -it sle-bci-test -- sh
sh-4.4# cat /etc/os-release 
NAME="SLES"
[...]
sh-4.4# exit
```

Command `cat` is working as expected.

Now let's create a group to Deny `cat` process in all pods of the `neuvector-demo-2` namespace

```bash
kubectl apply -f 04-custgrp-neuvector-demo-ns.yaml
nvclustersecurityrule.neuvector.com/ns-neuvector-demo-2 created
```

Exec into the pod again and run `cat`

```bash
sh-4.4# cat /etc/os-release 
sh: /usr/bin/cat: Operation not permitted
```

It is now blocked.
