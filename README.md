## Steps to reproduce

1. `task k3d:cluster:create`
2. `task istio:operator-controller`
3. `task istio:operator`
4. `kubectl apply -f netshoot.yaml`
5. `kubectl apply -f virtual-service.yaml`
6. Run `curl -sL -o /dev/null -D - https://edition.cnn.com/politics`


- Helm chart borrowed from https://github.com/istio/istio/tree/1.7.8/manifests/charts/istio-operator

# Notes

- It appears that creating multiple istio operators is the intended mechanism to create multiple ingress/egress gateways.

- Once we install the istio controller and the istio operator, we get an egress gateway deployed into the `cloud-main-system` namespace.

- The `Gateway` CRD is used to **configure** an ingress/egress gateway, where the latter is an envoy proxy + service and the former is a CRD providing configuration to the latter.

## API Versions of Ingress no longer supported after v1.22

The extensions/v1beta1 and networking.k8s.io/v1beta1 API versions of Ingress is no longer served as of v1.22.

- See [Deprecated API Migration Guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/#ingress-v122)

When cluster changes from 1.21.X to >= 1.22.X, will need to update Istio Operator accordingly to support new Ingress API.

# Useful Resources

- [Isto Operator Install Guide (v1.7)](https://istio.io/v1.7/docs/setup/install/operator/)

- [Multiple Istio Gateways](https://getistio.io/istio-in-practice/multiple-ingress-gateways/)

- [Envoy access logs](https://istio.io/latest/docs/tasks/observability/logs/access-log/)