# Guide to install kubeflow

## Requirements

- minimum 16GB RAM
- minimum 4 vCPUs
- 100GB Memory

## Install k3d and kubectl

```bash
sudo apt-get install k3d
sudo snap install kubectl --classic
```

## Create a k3d cluster

```bash
k3d cluster list k3s-default || k3d cluster create --network host --k3s-arg "--disable=traefik"   --host-pid-mode
```

## Install kustomize

```bash
wget https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv5.0.3/kustomize_v5.0.3_linux_amd64.tar.gz
tar -xzvf kustomize_v5.0.3_linux_amd64.tar.gz
sudo mv kustomize /usr/bin/
```

## Install kubeflow manifests

```bash
# Clone kubeflow manifests repo
git clone https://github.com/kubeflow/manifests

# Go to manifests directory
cd manifests

# Apply the manifestswhile ! kustomize build example | kubectl apply -f -; do echo "Retrying to apply resources"; sleep 10; done
```

## Port-forward to access the kubeflow UI

```bash
# Port-forward the istio-ingressgateway service
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
```

## Access kubeflow

Kubeflow UI is accesible via [http://localhost:8080/](http://localhost:8080/)