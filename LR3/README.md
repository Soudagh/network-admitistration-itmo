# Лабораторная работа №3

## Часть 1. Поднятие Postgres
1. Создание и поднятие docker контейнеров:
![docker](https://github.com/user-attachments/assets/02b8c7a7-361e-4ed0-a380-bbbcf4cbc207)
2. Определение master и slave ноды (master - pg_master, slave - pg_slave)
![Нода postgres0](https://github.com/user-attachments/assets/4cfede9b-c4b4-41b1-8696-eae75d4b781c)
![Нода postgres1](https://github.com/user-attachments/assets/7c61a020-d417-4ec5-9c92-0b667457212b)
3. Проверка, что зукипер запустился
![Zookiper](https://github.com/user-attachments/assets/7afaa003-5f2a-4f17-ad5c-e98a51450297)

## Часть 2. Репликации
4. Подключение к нодам постгреса
![подключение 1](https://github.com/user-attachments/assets/c0adc207-e2ee-459d-89a9-9f220db1150f)
![подключение 2](https://github.com/user-attachments/assets/b367df64-3d05-47bc-ae94-89893a456eeb)
5. В ноду лидера кластера (pg_master) добавляем таблицу и вставляем в неё данные
![создание таблицы](https://github.com/user-attachments/assets/e3247c97-24e3-4185-87dc-6d9b79df7988)
![image](https://github.com/user-attachments/assets/01aae2d5-5147-4321-83f4-07050ad469e0)
6. Проверяем, что в pg_slave также создалась эта таблица с теми же данными
![image](https://github.com/user-attachments/assets/7e8e5341-bcfc-491a-87ad-50561b8a345b)
7. Неудачно пытаемся удалить строчку из таблицы подключения pg_slave
![image](https://github.com/user-attachments/assets/5e3cdda4-1672-45a2-9bc9-036a4c6ca803)

## Часть 3. Высокая доступность и HAProxy
8. Перезапускаем docker контейнеры после добавления необходимых конфигурационных файлов и обновления docker-compose.yml для HAProxy
![image](https://github.com/user-attachments/assets/8189e4dc-6822-4880-8366-0f8912d44543)
9. Проверяем перераспределение ролей (всё осталось как было)
![image](https://github.com/user-attachments/assets/73684d12-5a32-4745-8d6d-84573fbbf0b7)
![image](https://github.com/user-attachments/assets/a1c52aeb-7b08-4583-80ea-713e2f2ace53)
10. Проверяем Zookiper
![image](https://github.com/user-attachments/assets/7847740b-49eb-418a-a63c-1befb43c839b)
11. Создаём подключение к psql_entrypoint (haproxy)
![image](https://github.com/user-attachments/assets/ceaf3d82-a440-45fd-bcc8-bb39f8c8c8cc)
12. Пытаемся заселектить данные из мастер-ноды (получилось!)
![image](https://github.com/user-attachments/assets/f47b922b-8738-47cf-9313-1d55e56da5d6)

## Задание
13. Отключаю мастер-ноду командой `docker stop pg-master`
14. Наблюдаю за логами pg-slave и haproxy. В логах у pg-slave замечаю, patroni перераспределил роли, и теперь pg-slave является лидером.
![image](https://github.com/user-attachments/assets/25f63b9c-5084-494b-b63f-0ea4c367a4d7)
![image](https://github.com/user-attachments/assets/d5fc1cb0-fd78-49f7-b1cd-2491814a1aa7)
15. В entrypont-подключение добавляю новую строчку, которая дублируется и в pg-slave
![image](https://github.com/user-attachments/assets/c7d8a97a-810f-4829-9218-ffb3248f0fca)
![image](https://github.com/user-attachments/assets/cc62154a-76bb-4e89-be69-aa8229a17880)
Также можно заметить, что у pg-slave пропало read-only ограничение!

## Ответы на вопросы
1. **Порты 8008 и 5432 вынесены в разные директивы, expose и ports. По сути, если записать 8008 в ports, то он тоже станет exposed. В чем разница?
Порты в директивах expose доступны только в пределах сети docker compose, а в директивах ports порты будут открыты на хост-машины, и будут доступны извне.
2. **При обычном перезапуске композ-проекта, будет ли сбилден заново образ? А если предварительно отредактировать файлы postgresX.yml? А если содержимое самого Dockerfile? Почему?**
Compose образы не пересобираются, если не используется флаг --build, так как изменения в конфигурации применяются сразу, а изменения в Dockerfile требуют пересборки.










 

