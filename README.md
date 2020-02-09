# ssi91_platform
ssi91 Platform repository

## HW №2
* Создан ReplicaSet для подов с образом `hipster-frontend:v0.0.1`
* Изменён образ образ контейнера в манифесте `frontend-replicaset.yaml`. 
	* После применения манифеста ничего не происходит до того момента, пока явно не удалить созданные этим ReplicaSet поды. Это происходит потом что ReplicaSet не проверяет соответствие запущенных Pod'ов шаблону
* Созданы образы `ssi91/paymentservice:v0.0.1` и `ssi91/paymentservice:v0.0.2`
* Созданы манифесты `paymentservice-replicaset.yaml` и `paymentservice-deployment.yaml`
* В манифесте `paymentservice-deployment.yaml` измененена версия образа с `ssi91/paymentservice:v0.0.1` на `ssi91/paymentservice:v0.0.2`
* После применения изменнёного манифеста поды будут обновленны сами
* Добавлены манифесты `paymentservice-deployment-bg.yaml`, как аналог blue-green, и `paymentservice-deployment-reverse.yaml` - Reverse Rolling Update
* Добавлен манифест `frontend-deployment.yaml` с `readinessProbe`
* Создан манифест `node-exporter-daemonset.yaml` c DaemonSet, создающим поды с Node Exporter
* Добавлена секция `tolerations` для того, чтобы DaemonSet создавал поды не только на worker, но и на master нодах

## HW №3
### task 01
* Создан ServiceAccount с именем bob
* Создан манифест ClusterRoleBinding, в котором ServiceAccount'у bob выданы права admin в рамках всего кластера
* Создан Service Account dave

### task 02
* Создан Namespace prometheus
* Создан Service Account jane в Namespace dev
* Создан манифест ClusterRoleBinding, в котором всем Service Account в Namespace prometheus возможность делать get, list, watch в отношении Pods всего кластера

### task 03
* Создан Namespace dev
* Создан Service Account jane в Namespace prometheus
* Создан манифест RoleBinding, в котором ServiceAccount'у jane роль admin в рамках Namespace dev
* Создан Service Account ken в Namespace dev
* Создан манифест RoleBinding, в котором ServiceAccount'у ken роль view в рамках Namespace dev

## HW №4
* Добавлено `readinessProbe` в манифест `web-pod`
* Добавлено `livenessProbe` в манифест `web-pod`
* Создан `deployment` для `web-pod` (web-deploy.yaml)
* Добавлен блок `strategy` в манифест web-deploy.yaml
* Создан манифест web-svc-cip.yaml
* В ключен IPVS вместо iptables
	* Удалены лишние цепочки iptables
* Создан MetalLB из манифеста https://raw.githubusercontent.com/google/metallb/v0.8.0/manifests/metallb.yaml
	* из указанного манифеста в версии k8s 1.17 не создаётся PodSecurityPolicy из-за неверно `apiVersion` в манифесте. Нужно заменить `apiVersion: extensions/v1beta1` на `apiVersion: policy/v1beta1` (см. манифест kubernetes-network/metallb.yml)
* Создан манифест metallb-config.yaml - ConfigMap, создающий пул адресов для сервисов типа LoadBalancer
* Создан web-svc-lb.yaml - манифест Service'а с типом LoadBalancer вместо ClusterIP
* Установлен `ingress-nginx`, применив [манифест](https://raw.githubusercontent.com/kubernetes/ingressnginx/master/deploy/static/mandatory.yaml)
* Создан манифест nginx-lb.yaml
* Создан web-svc-headless.yaml
* Создан web-ingress.yaml - манифест Ingress'а, направляющий на Service `web-svc`, определённый в web-svc-headless.yaml
