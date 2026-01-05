```bash

helm repo list
helm repo update

# See resources created by Helm release

helm get manifest my-release -n namespace
helm get manifest mysql-exporter -n mysql

helm ls -A
helm ls -n monitoring

# Create helm chart 
helm create greeting-app

# Uninstall chart
helm uninstall myrelease-3.0 -n default

# Check files installed by chart
helm install --dry-run=client debug . > yaml-files/out.yml

# Sintax for rendered templates: helm template my-release .
helm template greeting .
helm template greeting . -f values.yaml

# Check deployment.yaml created
helm template -s templates/deployment.yaml -n flask . > yaml-files/deploy.yml

# Usefull one
helm template greeting . \
  --show-only templates/service.yaml \
  --show-only templates/deployment.yaml \
  --show-only templates/tests/test-connection.yaml \
  > yaml-files/out.yml


# Validates helm chart 
helm lint .

# Packs helm chart. Creates greeting-app-0.1.0.tgz
helm package greeting-app/

move greeting-app-0.1.0.tgz ../charts

cd ../chars

helm repo idex .

git add .
git commit -m "added repo greeting-app-0.1.0.tgz"
git push


helm repo add lmonzalvo-github https://l-monzalvo.github.io/charts/

helm search repo lmonzalvo-github

helm install --dry-run="client" helm lmonzalvo-github/greeting-app

# Install helm chart from github repository
helm install greeting-app lmonzalvo-github/greeting-app -n default

kubectl create namespace flask
kubectl apply -f deploy.yml -n flask

kubectl create secret docker-registry dockerhub-secret \
  --docker-server=https://index.docker.io/\ \
  --docker-username=XXXXXXXX \
  --docker-password=XXXXXXXX \
  --docker-email=XXXXXXXXXXX \
  -n flask


# Login to docker hub
docker login

# The login process creates or updates a config.json file that holds an authorization token.
cat ~/.docker/config.json

# This one is secure for using it hardcoded
kubectl create secret docker-registry dockerhub-secret  \
    --docker-server='https://index.docker.io/v1/' \
    --from-file=.dockerconfigjson=/home/lmonzalvo/.docker/config.json \
    -n flask
    
kubectl get secrets -n flask -o yaml > yaml_files/mysec.yml

docker search lmonzalvo/greeting_app
docker pull lmonzalvo/greeting_app

kubectl port-forward svc/greeting-app-service 8085:8015 -n flask


```