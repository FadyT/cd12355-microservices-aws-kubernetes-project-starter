## Getting Started

### Deployment
#### Steps

check kubectl version
- kubectl version --short
check aws 
- which aws
- aws --version
configure aws account id , secret and region
- aws configure
create aks cluster 
- eksctl create cluster --name my-cluster --region us-east-1 --nodegroup-name my-nodes --node-type t3.small --nodes 1 --nodes-min 1 --nodes-max 2
- aws eks --region us-east-1 update-kubeconfig --name my-cluster
- kubectl config current-context
- kubectl get namespace
- kubectl get storageclass


- kubectl apply -f cd12355-microservices-aws-kubernetes-project-starter/deployment/pvc.yaml
- kubectl apply -f cd12355-microservices-aws-kubernetes-project-starter/deployment/pv.yaml
- kubectl apply -f cd12355-microservices-aws-kubernetes-project-starter/deployment/postgresql-deployment.yaml

- kubectl get pods
- kubectl exec -it postgresql-688c5c767c-tl8h2 -- bash
inside the pod
- psql -U myuser -d mydatabase
- kubectl apply -f cd12355-microservices-aws-kubernetes-project-starter/deployment/postgresql-service.yaml
- kubectl get svc
- kubectl port-forward service/postgresql-service 5433:5432 &

- apt update
- apt install postgresql postgresql-contrib
- export DB_PASSWORD=mypassword
- PGPASSWORD="$DB_PASSWORD" psql --host 127.0.0.1 -U myuser -d mydatabase -p 5433 -f cd12355-microservices-aws-kubernetes-project-starter/db/1_create_tables.sql
- PGPASSWORD="$DB_PASSWORD" psql --host 127.0.0.1 -U myuser -d mydatabase -p 5433 -f cd12355-microservices-aws-kubernetes-project-starter/db/2_seed_users.sql
- PGPASSWORD="$DB_PASSWORD" psql --host 127.0.0.1 -U myuser -d mydatabase -p 5433 -f cd12355-microservices-aws-kubernetes-project-starter/db/3_seed_tokens.sql
checking tables data
- PGPASSWORD="$DB_PASSWORD" psql --host 127.0.0.1 -U myuser -d mydatabase -p 5433


build analytics app
- apt update
- apt install build-essential libpq-dev
- pip install --upgrade pip setuptools wheel
- pip install -r cd12355-microservices-aws-kubernetes-project-starter/analytics/requirements.txt
export DB_USERNAME=myuser
export DB_PASSWORD=${POSTGRES_PASSWORD}
export DB_HOST=127.0.0.1
export DB_PORT=5433
export DB_NAME=mydatabase
python cd12355-microservices-aws-kubernetes-project-starter/analytics/app.py
pip install --upgrade Flask Werkzeug
curl http://127.0.0.1:5153/api/reports/daily_usage
curl http://127.0.0.1:5153/api/reports/user_visits

