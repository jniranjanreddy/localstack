# localstack

## What is Localstack

## LocalStack in helm
```
root@dev-server01 ~ # helm repo add localstack https://helm.localstack.cloud
"localstack" has been added to your repositories

root@dev-server01 ~ # helm repo ls
NAME            URL
localstack      https://helm.localstack.cloud


root@dev-server01 ~ # helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "localstack" chart repository
Update Complete. ⎈Happy Helming!⎈

helm upgrade --install localstack localstack/localstack --namespace localstack --create-namespace --values values.yaml

root@dev-server01 /myworkspace/localstack # helm upgrade --install localstack localstack/localstack --namespace localstack --create-namespace --values values.yaml
Release "localstack" does not exist. Installing it now.
NAME: localstack
LAST DEPLOYED: Thu Jun 23 17:35:03 2022
NAMESPACE: localstack
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace localstack -o jsonpath="{.spec.ports[0].nodePort}" services localstack)
  export NODE_IP=$(kubectl get nodes --namespace localstack -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT
  
root@dev-server01 /myworkspace/localstack # k get ns
NAME              STATUS   AGE
default           Active   36d
jenkins           Active   36d
keel              Active   44h
kube-node-lease   Active   36d
kube-public       Active   36d
kube-system       Active   36d
localstack        Active   15s

export LOCALSTACK_URL=http://127.0.0.1:31566

export AWS_ACCESS_KEY_ID=test
export AWS_SECRET_ACCESS_KEY=test
export AWS_DEFAULT_REGION=us-east-1

alias aws="aws --endpoint-url $LOCALSTACK_URL"
```
