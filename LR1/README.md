# ЛР 1. Loki + Zabbix + Grafana

## Ход работы:
1. Созданы файлы `docker-compose.yml`, `promtail_config.yml`, `template.yml` для дальнейшей работы.
2. Подняты контейнеры при помощи `docker compose`
![Поднятые контейнеры](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/1.jpg)
3. Создана админка в NextCloud и проверили логи
![Проверенные логи](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/3.jpg)
4. Проверили promtail в логах
![Проверенные логи](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/2.jpg)
5. Настроили общение между заббиксом и некстклаудом по своим коротким именам внутри докеровской сети
![Настройка](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/4.jpg)
6. Создали новый хост в zabbix
![Новый хост](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/5.jpg)
7. Получили первые данные
![Получение первых данных](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/6.jpg)
8. Установили плагин для графаны
![Установление плагинов](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/7.jpg)
9. Подключили дата сурсы и проверили их работу
![Проверка работы loki](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/8.jpg)
![Проверка работы zabbix](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/9.jpg)
10. Сделали визуализацию в виде графика и таблицы.
![Настроенная визуализация](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR1/images/10.jpg)

## Ответы на вопросы
1. SLO - это целевое значение SLI, которое необходимо достичь, а SLA - это формальный договор между поставщиком услуги и заказчиком, который описывает общие условия и штрафные санкции и который как раз включает в себя SLO.
2. Инкрементальный бэкап сохраняет изменения с последнего любого бэкапа, дифференциальный — с последнего полного.
3. Мониторинг — это часть observability. Мониторинг отслеживает известные показатели, а observability уже отслеживает их корреляцию и произоводит диагностику не одного конкретного показателя, а всей системы целиком.
