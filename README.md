
# Application 1
eksctl create cluster -f eksctl/app1.yaml

**switch context to cluster application1**
kubectl create ns application1
kubectl create -f k8s/

# Application 2
eksctl create cluster -f eksctl/app2.yaml

**switch context to cluster application2**
kubectl create ns application2
kubectl create -f k8s/

