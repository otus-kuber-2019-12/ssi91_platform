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
