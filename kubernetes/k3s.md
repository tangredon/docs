# Installation
```shell
curl -sfL https://get.k3s.io | sh -
```

# Configuration
## Disable Traefik
```shell
curl -sfL https://get.k3s.io | sh -s - --disable traefik
```

## User Permissions
```shell
curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
# or
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s -
```


