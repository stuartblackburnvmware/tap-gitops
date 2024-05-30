# Tanzu GitOps Reference Implementation

Use this archive contains an opinionated approach to implementing GitOps workflows on Kubernetes clusters.

This reference implementation is pre-configured to install Tanzu Application Platform.

For detailed documentation, refer to [VMware Tanzu Application Platform Product Documentation](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.7/tap/install-gitops-intro.html).

# Run cluster setup noes (WIP)

Set context to the View cluster and cd into the base of the `tap-gitops` directory

```
export RUN_CLUSTER=tap-run
MDS_CA_CERT=$(kubectl get secret -n metadata-store ingress-cert -o json | jq -r ".data.\"ca.crt\"")
cat <<EOF > clusters/$RUN_CLUSTER/cluster-config/dependent-resources/metadata-store-ca.yaml
---
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: store-ca-cert
  namespace: metadata-store-secrets
data:
  ca.crt: $MDS_CA_CERT
EOF
```