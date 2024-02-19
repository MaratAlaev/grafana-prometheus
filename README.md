# Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Задание повышенной сложности

**При решении задания 1** не используйте директорию [help](./help) для сборки проекта. Самостоятельно разверните grafana, где в роли источника данных будет выступать prometheus, а сборщиком данных будет node-exporter:

- grafana;
- prometheus-server;
- prometheus node-exporter.

За дополнительными материалами можете обратиться в официальную документацию grafana и prometheus.

В решении к домашнему заданию также приведите все конфигурации, скрипты, манифесты, которые вы 
использовали в процессе решения задания.

**При решении задания 3** вы должны самостоятельно завести удобный для вас канал нотификации, например, Telegram или email, и отправить туда тестовые события.

В решении приведите скриншоты тестовых событий из каналов нотификаций.

## Обязательные задания

### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
1. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
1. Подключите поднятый вами prometheus, как источник данных.
1. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

![image](https://github.com/MaratAlaev/grafana-prometheus/assets/46092593/5eaa7de4-3338-4a9c-b57d-e29b56d58384)


## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels

- утилизация CPU для nodeexporter (в процентах, 100-idle)

 ```
    100 - (avg by (instance) (rate(node_cpu_seconds_total{job="nodeexporter",mode="idle"}[2m])) * 100)
 ```
- CPULA 1/5/15;

  ```
  100 - (avg(rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100) 100 - (avg(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) 100 - 
  (avg(rate(node_cpu_seconds_total{mode="idle"}[15m])) * 100)
  ```

- количество свободной оперативной памяти;
  ```
  node_memory_MemAvailable_bytes
  ```
- количество места на файловой системе.
  ```
  ((node_filesystem_size_bytes{mountpoint="/"} - node_filesystem_avail_bytes{mountpoint="/"}) - node_filesystem_size_bytes{mountpoint="/"}) * -1
  ```
  

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

![image](https://github.com/MaratAlaev/grafana-prometheus/assets/46092593/b7b99268-4c1f-45a1-9809-8741e336c06b)


## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
1. В качестве решения задания приведите скриншот вашей итоговой Dashboard.
   
![image](https://github.com/MaratAlaev/grafana-prometheus/assets/46092593/f6501cd4-d522-4e91-89e1-9480a2fd9475)

![image](https://github.com/MaratAlaev/grafana-prometheus/assets/46092593/6efa6267-a63b-4310-ab87-1d2fa38bd6ce)




## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
1. В качестве решения задания приведите листинг этого файла.

[dashbord](https://github.com/MaratAlaev/grafana-prometheus/blob/main/dashbord.json)

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
