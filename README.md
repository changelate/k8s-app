# Установка зависимостей

### minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube


### Helm
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

### Ingres Nginx

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm install nginx-ingress ingress-nginx/ingress-nginx --set controller.hostPort.enabled=true


# Запуск

Minikube с помощью docker:
minikube start --driver=docker 


## Применяем configmap:
kubectl apply -f configmap.yaml --record

## Применяем deployment:
kubectl apply -f deployment.yaml --record

## Применяем service:
kubectl apply -f service.yaml --record

## Применяем ingress:
kubectl apply -f ingress.yaml --record


## Настройка host файла:
sudo nano /etc/hosts

### Добавляем строку
127.0.0.1 hello.local


# Проверка

curl -H "Host: hello.local" http://127.0.0.1

или 

Открыть http://hello.local в браузере


# Логи и отладка

## Проверка состояния подов:
kubectl get pods -o wide

## Проверка логов Ingress-контроллера:
kubectl logs -l app.kubernetes.io/name=ingress-nginx --tail=50 (показать 50 последних записей)

## kubectl describe ingress nginx-ingress

## Остановка Minikube:
minikube stop
