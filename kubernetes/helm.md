# Helm
Helm helps you manage **Kubernetes ([[k3s]])** applications — Helm Charts help you define, install, and upgrade even the most complex Kubernetes application.
# Installation
```shell
curl https://baltocdn.com/helm/signing.asc | apt-key add -
apt install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | tee /etc/apt/sources.list.d/helm-stable-debian.list
apt update
apt install helm
```



