# Steps to Reproduce (`aaw-fc` namespace in aaw-dev-cc-00)

**Case 1**: deploy everything into the same namespace created by kubeflow.

1. Deploy manifests folder to cluster `kubectl apply -f manifests-same-namespace --recursive`
2. Open a shell into the pod `test-employee-notebook` in namespace `aaw-fc`
3. Run `curl -svL -o /dev/null -D - https://edition.cnn.com/politics`

**Result**: the request completes with status code `200` and an access log is recorded in the egress gateway.

Tear down the example with `kubectl delete -f manifests-same-namespace --recursive`.

# Steps to Reproduce (`collin-brown` namespace in aaw-dev-cc-00)

**Case 2**: deploy notebook pod into different namespace (`collin-brown`), egress gateway into a namespace created by kubeflow (`aaw-fc`), and add network policies to allow communication between the two namespaces.

1. Deploy manifests folder `kubectl apply -f manifests-different-namespace/ --recursive`
2. Open a shell into the `test-employee-notebook` pod in namespace `collin-brown`
3. Run `curl -svL -o /dev/null -D - https://edition.cnn.com/politics`

**Result**: the curl request fails with error message `OpenSSL SSL_connect: Connection reset by peer in connection to edition.cnn.com:443`.

Tear down example with `kubectl delete -f manifests-different-namespace/ --recursive`

# Steps to Reproduce (`cloud-main-system` namespace in aaw-dev-cc-00)

**Case 3**: deploy notebook pod into different namespace (`collin-brown`), egress gateway into system namespace (`cloud-main-system`), and add network policies to allow communication between the two namespaces.

1. Deploy manifests folder `kubectl apply -f manifests-different-namespace/ --recursive`
2. Open a shell into the `test-employee-notebook` pod in namespace `collin-brown`
3. Run `curl -svL -o /dev/null -D - https://edition.cnn.com/politics`

**Result**: the curl request fails with error message `OpenSSL SSL_connect: Connection reset by peer in connection to edition.cnn.com:443`.

Tear down example with `kubectl delete -f manifests-cloud-main/ --recursive`