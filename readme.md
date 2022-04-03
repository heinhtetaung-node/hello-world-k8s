Note for Devop Session Up and Running
1. fork and clone repo https://github.com/heinhtetaung-node/hello-world-k8s
docker build --platform linux/amd64 -t hello-world-k8s . -f Dockerfile
docker run -d -p 3333:3000 --name hello-world-k8s hello-world-k8s

gcloud beta container --project effective-might-323902 clusters create-auto "hein-cluster" --region asia-southeast1 --release-channel regular --network projects/effective-might-323902/global/networks/default --subnetwork projects/effective-might-323902/regions/asia-southeast1/subnetworks/default --cluster-ipv4-cidr /17 --services-ipv4-cidr /22


docker tag hello-world-k8s asia.gcr.io/effective-might-323902/hello-world-k8s-hha:1.0.0
docker push asia.gcr.io/effective-might-323902/hello-world-k8s-hha:1.0.0
2. kubectl create configmap hello-world-k8s-hein-env --from-literal=FIRSTNAME=Hein
3. kubectl create secret generic hello-world-k8s-hein-secret --from-literal=LASTNAME=Aung
4. fix kube-deployment.yml , cloudbuild.yml file
from https://github.com/JeremyRms/hello-world-k8s/blob/master/kube-deployment.yml
to https://github.com/heinhtetaung-node/hello-world-k8s/blob/master/kube-deployment.yml
from https://github.com/JeremyRms/hello-world-k8s/blob/master/cloudbuild.yamlto
to https://github.com/heinhtetaung-node/hello-world-k8s/blob/master/cloudbuild.yaml

5. Create trigger

Event - Manual invocation

https://console.cloud.google.com/cloud-build/triggers?referrer=search&authuser=6&project=effective-might-323902

6. Click run 


--------------------------------------------------------------- 
Add kustomize folder

run kubectl apply -k kustomize/overlays/staging
