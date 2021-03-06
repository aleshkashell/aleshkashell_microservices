# aleshkashell_microservices    [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=master)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
aleshkashell microservices repository

# Table of content
- [Docker 1](#docker-1) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=docker-1)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Docker 2](#docker-2) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=docker-2)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Docker 3](#docker-3) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=docker-3)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Docker 4](#docker-4) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=docker-4)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Gitlab CI 1](#gitlab-ci-1) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=#gitlab-ci-1)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Gitlab CI 2](#gitlab-ci-2) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=gitlab-ci-2)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Monitoring 1](#monitoring-1) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=monitoring-1)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Monitoring 2](#monitoring-2) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=monitoring-2)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Logging 1](#logging-1) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=logging-1)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Kubernetes 1](#kubernetes-1) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=kubernetes-1)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Kubernetes 2](#kubernetes-2) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=kubernetes-2)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Kubernetes 3](#kubernetes-3) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=kubernetes-3)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Kubernetes 4](#kubernetes-4) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=kubernetes-4)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)
- [Kubernetes 5](#kubernetes-5) [![Build Status](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices.svg?branch=kubernetes-5)](https://travis-ci.com/Otus-DevOps-2018-05/aleshkashell_microservices)

# Docker 1

## 1. Что было сделано
- Установлены docker, docker-compose, docker-machine
- Рассмотрена работа с конетейнерами и образами
- Сохранен вывод команды docker images
- Описано отличие образа от конетейнера
- Добавлена интеграция с travis

## 2. Данные для проверки
- Содержимое файла docker-1.log

# Docker 2

## 1. Что было сделано
- Создан новый проект GCE
- Рассмотрена работа docker-machine с удаленными сервисами
- Произведена сборка docker образа и его запуск в GCE
- Образ залин на docker hub
- Созданы и описаны прототипы создания инфраструктуры с помощью terraform, ansible, packer

## 2. Как запустить проект
```
docker run --name reddit -d -p 9292:9292 aleshkashell/otus-reddit:1.0
```

## 3. Как проверить
- http://127.0.0.1:9292

# Docker 3

## 1. Что было сделано
- Созданы Dockerfile для компонентов приложения
- Произведены сборка и запуск приложения, проверена его работоспособность
- Проверена работа приложения с другими сетевыми алиасами контейнеров
- Образ UI пересобран на основе alpine
- Создан и использован volume

## 2. Как запустить проект
```
docker run -d --network=reddit --network-alias=post_db --network-alias=comment_db  -v reddit_db:/data/db  mongo:latest
docker run -d --network=reddit --network-alias=post aleshkashell/post:1.0
docker run -d --network=reddit --network-alias=comment aleshkashell/comment:1.0
docker run -d --network=reddit -p 9292:9292 aleshkashell/ui:3.0
```

## 3. Как проверить
- http://'docker-host-ip':9292

# Docker 4

## 1. Что было сделано
- Рассмотрена работа с сетью в docker
- Произведено развертывание окружения при помощи docker-compose
- Рассмотрена работа с сетью в docker-compose
- Docker-compose с помощью переменных окружения, значения которых вынесены в отдельный файл
- Изменить базовое имя проекта можно при помощи переменной окружения COMPOSE_PROJECT_NAME или с помощью опции -p:
```
docker-compose -p 'prefix' up -d
```
- Создан docker-compose.override.yml, который позволяет
    - Изменять код каждого из приложений, не выполняя сборку образа
    - Запускать puma для руби приложений в дебаг режиме с двумя воркерами (флаги --debug и -w 2)

## 2. Как запустить проект
```
docker-compose up -d
```

## 3. Как проверить
- http://'docker-host-ip':9292

# Gitlab CI 1

## 1. Что было сделано
- Развернут Gitlab CI с помощью docker-compose
- Создан проект в gitlab
- Добавлен pipeline в репозиторий
- Развернут и зарегистрирован runner
- Добавлена конфигурация ansible для автоматического развертывания большого количества runner'ов
- Добавлена интеграция со слак

## 2. Как проверить
- Сервис gitlab
```
http://35.233.90.26/
```
- Интеграция со слак
```
https://devops-team-otus.slack.com/messages/CB57RQQLA
```

# Gitlab CI 2

## 1. Что было сделано
 - Создан новый проект
 - Добавлены окружения в pipeline
 - Сделана возможность запускасть job кнопкой из интерфейса
 - Добавлено теггирование
 - Рассмотрены динамические окружения
 - При пуше новой ветки создается сервер для окружения с возможностью удалить кнопкой из ui
 - Добавлена сборка контейнера в шаге build

## 2. Как запустить проект
```
git push gitlab2 gitlab-ci-2
```

## 3. Как проверить
 - Появится сервер в gcp для окружения

# Monitoring 1

## 1. Что было сделано
 - Рассмотрена работа Prometheus
 - Переупорядочена структура директорий
 - Создан docker-образ prometheus
 - Произведена сборка контейнеров скриптами
 - Настроены healthchecks
 - Рассмотрена работа node-exporter
 - Добавлен мониторинг mongodb
 - Добавлен мониторинг ui, post, comment с помощью blackbox_exporter
 - Создан Makefile для сборки и заливки на docker hub образов

## 2. Как запустить проект
```
cd docker; docker-compose up -d
```

## 3. Как проверить
- http://'docker-host-ip':9090

# Monitoring 2

## 1. Что сделано
 - Реорганизованы файлы docker-compose
 - Рассмотрена работа cAdvisor
 - Рассмотрена работы Grafana и дашбордов
 - Созданы дашборды с метриками приложения
 - Настроена система алертинга
 - Образы запушены в docker-hub

## 2. Как запустить проект
```
docker-compose up -d
docker-compose -f docker-compose-monitoring.yml up -d
```

## 3. Как проверить
- http://'docker-host-ip':9090
- Канал в слаке:  #aleksey_sheludchenkov

# Logging 1

## 1. Что сделано
 - Пересобраны образы приложения для сборки логов
 - Рассмотрена работа логгирования на базе стека EFK
 - Рассмотрен сбор структурированных
 - Рассмотрена работы Kibana
 - Рассмотрен сбор и парсинг неструктурированных логов в fluentd
 - Добавлен дополнительный grok парсер для поля message в fluentd
 - Рассмотрена работ zipkin

## 2. Как запустить проект
В папке docker:
```
docker-compose up -d
docker-compose -f docker-compose-monitoring.yml up -d
```
## 3. Как проверить
 - http://'docker-host-ip':5601 - Kibana
 - http://'docker-host-ip':9411 - Zipkin

# Kubernetes 1

## 1. Что сделано
 - Созданы файлы с Deployment манифестами приложений
 - Пройден туториал Kubernetes The Hard way

## 2. Как проверить
 - Наличие файлов в kubernetes/the_hard_way

# Kubernetes 2

## 1. Что сделано
 - Развернуто локальное окружение kubernetes
 - Сконфигурирован и произведен деплой приложения reddit
 - Рассмотрена работа с сетью в kubernetes
 - Расмотрены namespaces
 - Рассмотрен dasboard kubernetes
 - Развернут kubernetes в gke
 - Развернуто приложение reddit в кластере gke

## 2. Как запустить проект
```
kubectl apply -f ./kubernetes/reddit/
```

## 3. Как проверить
```
http://<ClusterIP>:<NodePort>
```
# Kubernetes 3

## 1. Что сделано
 - Рассмотрена работа сервисов kubernetes
 - Рассмотрена работа LoadBalancer
 - Настроен Ingress
 - Настроен TLS
 - Созданы Network Policy при помощи плагина Calico
 - Рассмотрена работа с хранилищами для кластера
 - Подключен динамический Persistent Volume Claim (PVC)

## 2. Как запустить проект
```
kubectl apply -f ./kubernetes/reddit/
```

## 3. Как проверить
```
http://<ClusterIP>:<NodePort>
```

# Kubernetes 4

## 1. Что было сделано
 - Рассмотрена работа с helm
 - Развернут gitlab в kubernetes
 - Настроен CI/CD конвейер в Gitlab

## 2. Как проверить
```
http://<ClusterIP>
```

# Kubernetes 5

## 1. Что сделано
 - Рассмотрена работа мониторинга в kubernetes с помощью prometheus
 - Настроена визуализация с помощью Grafana (с использованием переменных)
 - Рассмотрен стек логирования EFK

