# ssi91_platform
ssi91 Platform repository

# ДЗ 3:

* Добавлено `readinessProbe` в манифест `web-pod`
* Добавлено `livenessProbe` в манифест `web-pod`
* Создан `deployment` для `web-pod` (web-deploy.yaml)
* Добавлен блок `strategy` в манифест web-deploy.yaml
* Создан манифест web-svc-cip.yaml
* В ключен IPVS вместо iptables
	* Удалены лишние цепочки iptables
* Создан MetalLB
* Создан манифест metallb-config.yaml - ConfigMap, создающий пул адресов для сервисов типа LoadBalancer
* Создан web-svc-lb.yaml - манифест Service'а с типом LoadBalancer вместо ClusterIP
* Установлен `ingress-nginx`, применив [манифест](https://raw.githubusercontent.com/kubernetes/ingressnginx/master/deploy/static/mandatory.yaml)
* Создан манифест nginx-lb.yaml
* Создан web-svc-headless.yaml
* Создан web-ingress.yaml - манифест Ingress'а, направляющий на Service `web-svc`, определённый в web-svc-headless.yaml
