# Grafana

# Instalar Grafana
Al igual que con Prometheus, el canal estable de los Helm charts oficiales para Grafana se han discontinuado. Los charts que ahora se recomiendan son aquellos ofrecidos por el repositorio Grafana Community Kubernetes Helm Charts.

Del mismo modo que antes, comenzaremos agregando el repositorio a nuestra configuración de Helm:

helm repo add grafana https://grafana.github.io/helm-charts

A continuación instalamos Grafana utilizando los charts disponibles:

[n]helm install grafana stable/grafana[\n]
kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-np

Nuevamente, considerando que estamos utilizando Minikube, para poder acceder de forma sencilla a la interfaz web de Grafana, exponemos el servicio como un NodePort.

Nota: La interfaz de Grafana está protegida por password por defecto, para conseguir el password del usuario admin, podemos ejecutar el siguiente comando:

kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

Ahora ya podemos acceder a la interfaz web de Grafana utilizando el usuario admin y el password que hemos obtenido en el paso anterior.

minikube service grafana-np

## Configurar el Datasource de Prometheus
Una vez hemos accedido a la interfaz de administración, es el momento de que configuremos el Datasource de Prometheus.

Para ello, debeos de acceder al menú Configuration > Datasources y añadir una nueva instancia de Prometheus.

La URL para nuestra instancia de Prometheus coincide con el nombre del servicio http://prometheus-server:80
