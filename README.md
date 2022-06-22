# Steps to Reproduce (`aaw-fc` namespace in aaw-dev-cc-00)

**Case 1**: deploy everything into the same namespace created by kubeflow.

1. Deploy manifests folder to cluster `kubectl apply -f manifests-same-namespace --recursive`
2. Open a shell into the pod `test-employee-notebook` in namespace `aaw-fc`
3. Run `curl -svL -o /dev/null -D - https://edition.cnn.com/politics`

**Result**: the request completes with status code `200` and an access log is recorded in the egress gateway.

Tear down the example with `kubectl delete -f manifests-same-namespace --recursive`.