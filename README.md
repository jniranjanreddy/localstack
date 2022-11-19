# localstack
Source: https://pypi.org/project/localstack/

## LocalStack in helm
```
root@dev-server01 ~ # helm repo add localstack https://helm.localstack.cloud
"localstack" has been added to your repositories

root@dev-server01 ~ # helm repo ls
NAME            URL
localstack      https://helm.localstack.cloud


root@dev-server01 ~ # helm repo update
Hang tight while we grab the latest from your chart repositories...
Successfully got an update from the "localstack" chart repository
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
## Python Based Installation
```
#source: https://pypi.org/project/localstack/
pip3 install localstack
localstack start -d
localstack status services

root@swarm01:/myworkspace# localstack status services
┏━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━┓
┃ Service                  ┃ Status      ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━┩
│ acm                      │ ✔ available │
│ apigateway               │ ✔ available │
│ cloudformation           │ ✔ available │
│ cloudwatch               │ ✔ available │
│ config                   │ ✔ available │
│ dynamodb                 │ ✔ available │
│ dynamodbstreams          │ ✔ available │
│ ec2                      │ ✔ available │
│ es                       │ ✔ available │
│ events                   │ ✔ available │
│ firehose                 │ ✔ available │
│ iam                      │ ✔ available │
│ kinesis                  │ ✔ available │
│ kms                      │ ✔ available │
│ lambda                   │ ✔ available │
│ logs                     │ ✔ available │
│ opensearch               │ ✔ available │
│ redshift                 │ ✔ available │
│ resource-groups          │ ✔ available │
│ resourcegroupstaggingapi │ ✔ available │
│ route53                  │ ✔ available │
│ route53resolver          │ ✔ available │
│ s3                       │ ✔ available │
│ s3control                │ ✔ available │
│ secretsmanager           │ ✔ available │
│ ses                      │ ✔ available │
│ sns                      │ ✔ available │
│ sqs                      │ ✔ available │
│ ssm                      │ ✔ available │
│ stepfunctions            │ ✔ available │
│ sts                      │ ✔ available │
│ support                  │ ✔ available │
│ swf                      │ ✔ available │
│ transcribe               │ ✔ available │
└──────────────────────────┴─────────────┘

root@swarm01:~# pip3 install awscli-local
Successfully built awscli-local
Installing collected packages: awscli-local
Successfully installed awscli-local-0.20


## Docker compose
```
root@minikube01 /myworkspace/local-stack # cat docker-compose.yml
version: "3.4"
services:
  localstack:
    container_name: localstack-test
    image: localstack/localstack:latest
    ports:
      - 4566:4566
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

networks:
  default:
    name: localstack
```
## Localstack docker baes
```
```
1. awscli need to be installed
2. awscli-local to be installed
3. docker run -itd -v "/var/run/docker.sock":"/var/run/docker.sock" -v "/volume/tmp/localstack":"/tmp/localstack" -p 4566:4566 --network localstack --name localstack localstack/localstack:latest
4. docker create network localstack

testing...
create Iam user..
root@dev-server01:~# awslocal iam create-user --user-name niru
{
    "User": {
        "Path": "/",
        "UserName": "niru",
        "UserId": "q4qpsrrf9ewyho0lz39j",
        "Arn": "arn:aws:iam::000000000000:user/niru",
        "CreateDate": "2022-11-19T07:45:36.995000+00:00"
    }
}
list Iam users
root@dev-server01:~# awslocal iam list-users
{
    "Users": [
        {
            "Path": "/",
            "UserName": "niru",
            "UserId": "q4qpsrrf9ewyho0lz39j",
            "Arn": "arn:aws:iam::000000000000:user/niru",
            "CreateDate": "2022-11-19T07:45:36.995000+00:00"
        }
    ]
}

```
