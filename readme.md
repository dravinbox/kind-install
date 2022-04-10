# kind

## 创建集群

````sh

kind create cluster --config=kind_create.yml

````
## 安装loadBalance

```sh
cd yml/metallb
kubectl apply -f namespace.yaml
kubectl apply -f mainfest.yaml
kubectl apply -f metallb-configmap.yaml

```

## 安装ingress

使用Ambassador

```sh
kubectl apply -f https://github.com/datawire/ambassador-operator/releases/latest/download/ambassador-operator-crds.yaml

kubectl apply -n ambassador -f https://github.com/datawire/ambassador-operator/releases/latest/download/ambassador-operator-kind.yaml

kubectl wait --timeout=180s -n ambassador --for=condition=deployed ambassadorinstallations/ambassador


#使用时重新注解一下ingress 使用ambassador
kubectl annotate ingress example-ingress kubernetes.io/ingress.class=ambassador

```
