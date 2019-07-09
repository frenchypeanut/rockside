# How to install Rockside on Kubernetes

This tutorial shows you how to deploy Rockside on Kubernetes.

## Before you begin

You need a Kubernetes cluster, and the [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/) command-line tool must be configured to communicate with your cluster.
If you do not already have a cluster, you can create one by using [`minikube`](https://kubernetes.io/docs/setup/learning-environment/minikube/).
You also need a running MySQL server.

Download the following configuration files:

1. [db-secret.yaml](db-secret.yaml)
1. [rockside-config.yaml](rockside-config.yaml)
1. [engine-deployment.yaml](engine-deployment.yaml)
1. [scheduler-deployment.yaml](scheduler-deployment.yaml)
1. [front-deployment.yaml](front-deployment.yaml)


## Create Secrets

A Secret is an object that stores a piece of sensitive data like a password or private key. The manifest files are already configured to use a Secret, but you have to create your own Secret.

### MySQL

In the `db-secret.yaml` file, the keys `host`, `password` and `username` must be base64 encoded. For instance, you can get them with this command:

```
echo -n 'my-host' | base64
```
Modify `db-secret.yaml` with those values:
```
apiVersion: v1
kind: Secret
metadata:
  name: rockside-db
data:
  host: BASE64_OF_HOST
  username: BASE64_OF_USERNAME
  password: BASE64_OF_PASSWORD
```

Then create your secret

```
kubectl apply -f db-secret.yaml
```

### Rockside Engine

#### Slave Token

```
# Generate a random token
YOUR_TOKEN=$(cat /dev/urandom | head -c 2048 | shasum | head -c 40)

kubectl create secret generic rockside-slave-token --from-literal=token=$YOUR_TOKEN
```

#### Application Key

```
# Generate a random key
YOUR_KEY=$(cat /dev/urandom | head -c 32 | base64)

kubectl create secret generic rockside-app-key --from-literal=key=base64:$YOUR_KEY
```

### Rockside Front SSL Certificate

1. First generate dhparam file

  ```
  openssl dhparam -dsaparam -out dhparam.pem 2048
  ```

1. Next, generate self-signed certificate and private keys. If you already have certificate and keys, then ignore this step.

  ```
   openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out cert.pem
  ```

1. Finally, create secret with certificate, private key and dhparam.

  ```
  kubectl create secret generic rockside-front-certs-keys --from-file=./key.pem --from-file=./cert.pem --from-file=./dhparam.pem
  ```

### Docker registry credentials

Create a secret to store docker registry credentials used to access rockside images.

```
kubectl create secret docker-registry private-docker-key --docker-username="DOCKER_USERNAME" --docker-password="DOCKER_PASSWORD" --docker-email="DOCKER_EMAIL" --docker-server="https://index.docker.io/v1/"
```

## Create ConfigMap

Create a ConfigMap to keep the configuration to be shared between the different rockside deployments.

Edit the `rockside-config.yaml` file and add the URL where the rockside app will be available.

```
app_url: https://cloud.rockside.io
```
Then create your config map:

```
kubectl apply -f rockside-config.yaml
```

## Deploy Rockside Engine

1. Deploy Rockside Engine with the `engine-deployment.yaml` file:

  ```
  kubectl create -f engine-deployment.yaml
  ```

1. Verify that a PersistentVolume got dynamically provisioned.

  ```
  kubectl get pvc
  ```

  The result should be like this:

  ```
  NAME                      STATUS    VOLUME            CAPACITY   ACCESS MODES   STORAGECLASS   AGE
  rockside-engine-pv-claim  Bound     pvc-ded5ff20...   10Gi       RWO            standard       66s
  ```

1. Verify that the Pod is running with the following command:

  ```
  kubectl get pods
  ```

  The result should be like this:

  ```
  NAME                     READY     STATUS       RESTARTS   AGE
  engine-7bc8fcbb5-4622p   1/1       Running		0          66s
  ```

## Deploy Rockside Scheduler

1. Deploy Rockside Scheduler with the `scheduler-deployment.yaml` file:

  ```
  kubectl create -f scheduler-deployment.yaml
  ```

1. Verify that the Pod is running with the following command:

  ```
  kubectl get pods
  ```

  The result should be like this:

  ```
  NAME                     READY     STATUS       RESTARTS   AGE
  scheduler-7bc8fcbb5-4622p   1/1       Running		0          66s
  ```

## Deploy Rockside Front

1. Deploy Rockside Front with the `front-deployment.yaml` file:

  ```
  kubectl create -f front-deployment.yaml
  ```

1. Verify that the Pod is running with the following command:

  ```
  kubectl get pods
  ```

  The result should be like this:

  ```
  NAME                     READY     STATUS       RESTARTS   AGE
  front-7bc8fcbb5-4622p    1/1       Running		0          66s
  ```

## Setup Rockside

To populate the database and setup rockside you will have to execute the following commands:

First get the pod name of the engine:

```
kubectl get pods -l tier=backend
```

The response should be like this:

```
NAME                               READY   STATUS    RESTARTS   AGE
rockside-engine-695669df6f-qvxpz   1/1     Running   0          7m44s
```

Then execute:

```
kubectl exec -it rockside-engine-695669df6f-qvxpz -- bash -c  "php artisan migrate --no-interaction --force && php artisan passport:install --no-interaction"
```

## Configure SMTP settings

Define the following environment variables:

```
MAIL_HOST=
MAIL_PORT=
MAIL_ENCRYPTION=
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_FROM_ADDRESS=notification@rockside.io
MAIL_FROM_NAME=rockside
```
