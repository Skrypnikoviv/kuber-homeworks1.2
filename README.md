# Домашнее задание к занятию «Базовые объекты K8S» - Скрыпников Илья

---

## Задание 1: Создать Pod с именем `hello-world`

### Шаги выполнения:

1. **Создание манифеста Pod:**

   Создал файл `hello-world-pod.yaml` со следующим содержимым:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: hello-world
   spec:
     containers:
     - name: echoserver
       image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
       ports:
       - containerPort: 8080
   ```

2. **Применение манифеста:**

   Выполнил команду для создания Pod:

   ```bash
   kubectl apply -f hello-world-pod.yaml
   ```

   Результат:
   ```
   pod/hello-world created
   ```

3. **Подключение к Pod с помощью `kubectl port-forward`:**

   Запустил перенаправление портов:

   ```bash
   kubectl port-forward pod/hello-world 8080:8080
   ```

   Результат:
   ```
   Forwarding from 127.0.0.1:8080 -> 8080
   Forwarding from [::1]:8080 -> 8080
   ```

4. **Проверка подключения:**

   Использовал `curl` для проверки:

   ```bash
   curl http://localhost:8080
   ```

   Результат:
 ![image](https://github.com/user-attachments/assets/fd0796d7-e44c-49f1-bead-6774924bbf73)

---

## Задание 2: Создать Service и подключить его к Pod

### Шаги выполнения:

1. **Создание манифеста Pod:**

   Создал файл `netology-web-pod.yaml` со следующим содержимым:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: netology-web
     labels:
      app: netology
   spec:
     containers:
     - name: echoserver
       image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
       ports:
       - containerPort: 8080
   ```

2. **Применение манифеста:**

   Выполнил команду для создания Pod:

   ```bash
   kubectl apply -f netology-web-pod.yaml
   ```

   Результат:
   ```
   pod/netology-web created
   ```

3. **Создание манифеста Service:**

   Создал файл `netology-svc.yaml` со следующим содержимым:

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: netology-svc
   spec:
     selector:
       app: netology
     ports:
     - protocol: TCP
       port: 80
       targetPort: 8080
   ```

4. **Применение манифеста:**

   Выполнил команду для создания Service:

   ```bash
   kubectl apply -f netology-svc.yaml
   ```

   Результат:
   ```
   service/netology-svc created
   ```

5. **Подключение к Service с помощью `kubectl port-forward`:**

   Запустил перенаправление портов:

   ```bash
   kubectl port-forward service/netology-svc 8080:80
   ```

   Результат:
   ```
   Forwarding from 127.0.0.1:8080 -> 8080
   Forwarding from [::1]:8080 -> 8080
   ```

6. **Проверка подключения:**

   Использовал `curl` для проверки:

   ```bash
   curl http://localhost:8080
   ```

   Результат:
 
   ![image](https://github.com/user-attachments/assets/8e401e60-13b3-479b-8c1e-72367ea5e246)

---

