Клонировать репозиторий и упаковать чарт
git clone https://github.com/Dias21B030874/sonarqube-helm-chart.git
cd sonarqube-helm-chart
helm package .

Установить чарт
helm install sonar . --namespace sonar --create-namespace -f values.yaml

Проверить статус подов
kubectl get pods -n sonar

Получить доступ к веб-интерфейсу
• Через порт-форвард:
kubectl port-forward svc/sonarqube-sonarqube 9000:9000 -n sonar
Открыть в браузере http://localhost:9000
• Через NodePort:
kubectl patch svc sonarqube-sonarqube -n sonar -p '{"spec":{"type":"NodePort","ports":[{"port":9000,"nodePort":30080}]}}'
minikube ip (например, 192.168.49.2)
Открыть http://<minikube-ip>:30080

Авторизация в SonarQube
Логин: admin
Пароль: admin

Удаление
helm uninstall sonar -n sonar
kubectl delete pvc -n sonar --all


