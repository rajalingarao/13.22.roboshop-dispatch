
# Dispatch

We use bastion host as Docker server and EKS client.
Make sure `aws configure` is done in bastion and connected to EKS cluster.
```
aws eks update-kubeconfig --region us-east-1 --name roboshop-dev
```
```
kubectl create namespace roboshop
```
```
git clone https://github.com/Lingaiahthammisetti/13.22.roboshop-dispatch.git
```
```
cd 13.22.roboshop-dispatch
```

* Login to ECR
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 484907532817.dkr.ecr.us-east-1.amazonaws.com
```
* Build Dispatch image.
```
docker build -t 484907532817.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/dispatch:v1.0.2 .
```
* Push image
```
docker push 484907532817.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/dispatch:v1.0.2
```
* Now install using Helm. move to helm directory
```
cd helm
```

```
helm upgrade --install dispatch . -n roboshop
```