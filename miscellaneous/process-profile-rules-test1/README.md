# Process Profile Rules

## Test case 1

Create `neuvector-demo-1` namespace

```bash
kubectl apply -f 01-ns-neuvector-demo-1.yaml
namespace/neuvector-demo-1 created
```

Create a group `nv.sle-bci.neuvector-demo-1` where process `ls` is allowed

```bash
kubectl apply -f 02-nv.sle-bci.neuvector-demo-1.ls.yaml
nvsecurityrule.neuvector.com/nv.sle-bci.neuvector-demo-1 created
```

Create pod `sle-bci-test` in namespace `neuvector-demo-1` (will be member of `nv.sle-bci.neuvector-demo-1`)

```bash
kubectl apply -f 03-sle-bci-pod.yaml
pod/sle-bci-test created
```

Exec into the pod and run `ls`

```bash
kubectl exec -n neuvector-demo-1 -it sle-bci-test -- sh
sh-4.4# ls -l /etc/os-release
-rw-r--r-- 1 root root 227 May 12  2022 /etc/os-release
sh-4.4# exit
```

Command `ls` is working as expected.

Now let's remove `ls` from the allowed processes

```bash
kubectl apply -f 04-nv.sle-bci.neuvector-demo-1.no-ls.yaml
nvsecurityrule.neuvector.com/nv.sle-bci.neuvector-demo-1 configured
```

Exec into the pod again and run `ls`

```bash
kubectl exec -n neuvector-demo-1 -it sle-bci-test -- sh
sh-4.4# ls -l /etc/os-release
-rw-r--r-- 1 root root 227 May 12  2022 /etc/os-release
```

It is still allowed ! Should not be the case...
