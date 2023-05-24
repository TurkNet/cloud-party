# TurkNet Cloud Party Demo

### Containerize Log Generate App
```
git clone https://github.com/turknet/cloud-party.git
cd cloud-party/log-generate-app
docker build -t turknethub/log-generate-app:v1 .
docker push turknethub/log-generate-app:v1 
```

### Create Namespace
```
kubectl create ns demo
```

### Deploy Log Generate App
```
kubectl apply -f https://raw.githubusercontent.com/turknet/cloud-party/main/log-generate-app/deployment.yaml -n demo
```

### Deploy EFK Stack
```
kubectl apply -f https://raw.githubusercontent.com/turknet/cloud-party/main/efk-stack/1-es-sts.yaml -n demo
kubectl apply -f https://raw.githubusercontent.com/turknet/cloud-party/main/efk-stack/2-kibana-deployment.yaml -n demo
kubectl apply -f https://raw.githubusercontent.com/turknet/cloud-party/main/efk-stack/3-fluentd-ds.yaml -n demo
```
Extra! Show Kibana Public IP
```
kubectl get svc kibana -n demo -o jsonpath='{.status.loadBalancer.ingress[0].ip}'
```

### BONUS! (Deploy ES Curator)
```
kubectl apply -f https://raw.githubusercontent.com/turknet/cloud-party/main/efk-stack/4-curator-cronjob.yaml -n demo
```
