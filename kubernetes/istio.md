# Installation
Requires [[helm]]

```shell
# install the helm repo (optionally) # may not be required
helm repo add istio https://istio-release.storage.googleapis.com/charts
helm repo update

# create namespace
kubectl create namespace istio-system

# install istio core chart
helm install \
	--repo https://istio-release.storage.googleapis.com/charts \
	--namespace istio-system \
	istio-base \
	istio/base

# install istio discovery chart
helm install \
	--repo https://istio-release.storage.googleapis.com/charts \
	--namespace istio-system \
	istiod \
	istio/istiod --wait --debug
```

# Extensions
## Gateway
```shell
# Install Istio Gateway (optional)
kubectl create namespace istio-ingress
kubectl label namespace istio-ingress istio-injection=enabled
helm install \
    --repo https://istio-release.storage.googleapis.com/charts \
    --namespace istio-system \
    istio-ingress-gateway \
    istio/gateway --wait --debug
```

## Kiali
```shell
# Install Kiali (optional)
helm install \
  --namespace istio-system \
  --set auth.strategy="anonymous" \
  --repo https://kiali.org/helm-charts \
  kiali-server \
  kiali-server
```
