# Лабораторная работа №2

## Ход выполнения
1. Проверили, что сервер с Ansible подключился к клиенту
![image](https://github.com/user-attachments/assets/709aba05-3c85-4e39-9ada-8b0c40bff1ae)
2. Создаём и удаляем файл
![image](https://github.com/user-attachments/assets/127262f2-087d-4338-b8cb-8a5384db37b9)
3. Создали папку `roles` и инициализировали исходное конфигурационное дерево
![image](https://github.com/user-attachments/assets/955f1910-7970-4352-8e9a-fe8100e620c5)
4. Запустили плейбук
![image](https://github.com/user-attachments/assets/fe16e122-f26c-46a4-9e40-ec22529c212d)
5. Добавили данные о домене, новые шаги в tasks/main.yml и запустили плейбук снова

[**https://balbesi.duckdns.org**](https://balbesi.duckdns.org)

![Плейбук с доменом](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR2/images/1.jpg)
![Тестовая страница](https://github.com/Soudagh/network-admitistration-itmo/blob/main/LR2/images/2.jpg)

## Задание 1
![Задание 1](https://github.com/user-attachments/assets/adc00366-be3e-4b26-9423-b3e03711730c)
Код плейбука
![Код плейбука](https://github.com/user-attachments/assets/de9f58cc-fae9-416c-9f19-46358df195a8)

## Задание 2
Изменённый `Caddyfile.j2`
```
{{ domain_name }} {
        root * /usr/share/caddy
        file_server

        log {
                output file {{ log.file }}
                format json
                level {{ log.level }}
        }
        header / {
          X-Custom-Header "Balbesnii header"
        }

        reverse_proxy /api/* localhost:3000
}
```

Создание директории и файла `index.html`
```
- name: Create /var/www/html directory
  file:
    path: /var/www/html
    state: directory
    owner: www-data
    group: www-data
    mode: '0755'

- name: Create custom index.html
  copy:
    content: |
      <html>
        <head>
          <title>LR2</title>
        </head>
        <body>
          <h1>Balbesi zahvatyat mir!</h1>
        </body>
      </html>
    dest: /var/www/html/index.html
    owner: www-data
    group: www-data
    mode: '0664'
```
![Задание 2](https://github.com/user-attachments/assets/d0484990-620c-4dd7-86a3-46da6af85464)

