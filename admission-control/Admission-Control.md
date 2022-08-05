# Admission Control

The Admission Control feature is disabled by default. Please go to Policy -> Admission Control page to enable it in the NeuVector console.

All admission control events for allowed and denied events can be found in the Notifications -> Security Risks menu.

## Run as root

Requirements:
- The check requires the image to be scanned
- The check is based on the deployment file

```bash
kubectl apply -f run-as-root.yaml
```

## Environment variables with secrets

```bash
kubectl apply -f env-var-with-secrets.yaml
```
