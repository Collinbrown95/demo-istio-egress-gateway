## Steps to reproduce

1. `task k3d:cluster:create`
2. `kubectl create ns istio-system`
3. `task istio:operator`


- Helm chart borrowed from https://github.com/istio/istio/tree/1.7.8/manifests/charts/istio-operator

# Notes

## API Versions of Ingress no longer supported after v1.22

The extensions/v1beta1 and networking.k8s.io/v1beta1 API versions of Ingress is no longer served as of v1.22.

- See [Deprecated API Migration Guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/#ingress-v122)

When cluster changes from 1.21.X to >= 1.22.X, will need to update Istio Operator accordingly to support new Ingress API.