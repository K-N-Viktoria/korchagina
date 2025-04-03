# korchagina

АИС (Автоматизированной Информационной Системы)
![image](https://github.com/user-attachments/assets/2b43bc62-faae-41ad-b1dc-e646c88ebe08)


Начинаем работу с установки утилиты wget:

`````sudo yum install wget`````

![image](https://github.com/user-attachments/assets/3c3d630d-bc97-48bd-b85d-585573da215d)

Скачиваем файл репозитория:

`````sudo wget -P /etc/yum.repos.d/https://download.docker.com/linux/centos/docker-ce.repo`````

![image](https://github.com/user-attachments/assets/eef00eb9-303e-4ec7-b752-fd6bc7700a2a)

Устанавливаем docker:

`````sudo yum install docker-ce docker-ce-cli containerd.io`````


![image](https://github.com/user-attachments/assets/1c0e3aff-ab1b-412a-8549-7feafca68200)
![image](https://github.com/user-attachments/assets/c6f7afbf-a111-46a1-845c-1eb3f9264b82)

Запускаем docker и разрешаем автозапуск:

`````sudo systemctl enable docker --now`````

![image](https://github.com/user-attachments/assets/5ccdadc9-20da-49d3-87a2-eb9b01f8a46b)

Перед этим проверим установлен ли пакет curl:  

`````sudo yum install curl`````

![1](https://github.com/user-attachments/assets/658f208e-5404-4747-a61a-2188dfdac881)


 Определяем последнюю версию docker с помощью api github:

````` COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`````

![image](https://github.com/user-attachments/assets/323406a0-3f01-4205-81e8-b3c9d18f2bce)

Скачиваем скрипт docker-compose последней версии:

`````sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`````

![image](https://github.com/user-attachments/assets/a6b8e225-7d2b-42cf-8908-f8a7abde9352)

Предоставляем правва файл docker-compose:

`````sudo chmod +x /usr/bin/docker-compose`````

![image](https://github.com/user-attachments/assets/79591ce8-d89f-452d-83c9-7918f0a68f1a)

Проверяем версию:

`````docker-compose --version`````

![image](https://github.com/user-attachments/assets/50f4b3b5-44b0-4ca0-818f-903fab2ae4c8)


Скачаем git:

`````git clone https://github.com/skl256/grafana_stack_for_docker.git`````

![image](https://github.com/user-attachments/assets/82fa5cd4-254d-4309-a9f7-74d6d2f5b839)

Переходим в папку:

`````cd grafana_stack_for_docker`````

![image](https://github.com/user-attachments/assets/4f734f26-5ca6-49f2-85c1-1f37633a6c2e)

Создаём полный путь:

`````sudo mkdir -p /mnt/common_volume/swarm/grafana/config`````

![image](https://github.com/user-attachments/assets/26a4e176-51d2-41bc-ad20-73c8f8e0b8a1)


Создание структуры каталогов Grafana и компонентов (если нужно):

`````sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`````

![2](https://github.com/user-attachments/assets/aee4def5-932e-4b9a-8724-271edda09547)


Создаём структуру каталогов:

`````sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`````

![image](https://github.com/user-attachments/assets/ba26e191-3da2-4a30-90ff-794e56980bc8)

Создаём млм обновляем файл grafana.ini:

`````touch /mnt/common_volume/grafana/grafana-config/grafana.ini`````

![image](https://github.com/user-attachments/assets/5f599b7b-5d6e-432d-b52a-f2eab20e8955)

Копируем все файлы:

`````cp config/* /mnt/common_volume/swarm/grafana/config/ `````

![image](https://github.com/user-attachments/assets/d174d1c1-ba05-4d74-9fa0-77083cbdd547)

Переименовываем файл grafana.yaml в docker-compose.yaml:

`````mv grafana.yaml docker-compose.yaml`````

![image](https://github.com/user-attachments/assets/53c88747-7627-48f9-b368-58cd15bb32bf)

Запускаем контейнеры в фоновом режиме:

`````sudo docker compose up -d`````

![image](https://github.com/user-attachments/assets/2022042b-0b92-45e8-a1f0-f8a0b172f723)
![image](https://github.com/user-attachments/assets/f63284ad-7ec5-4b88-982b-623388effbe3)

Открываем файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя. Изменяем файл, вот как он должен выглядеть вот так:

 `````sudo vi docker-compose.yaml`````
 
![image](https://github.com/user-attachments/assets/fed6e754-011f-499b-8df2-8d9a6dfb66c3)
![3](https://github.com/user-attachments/assets/acff0aa0-8889-444d-8a6d-1cce12b37c18)

Открываем файл prometheus.yaml  в текстовом редакторе vi с правами суперпользователя. И так-же меняем файл как скрине:

`````sudo vi  prometheus.yaml`````

![image](https://github.com/user-attachments/assets/a0d0faa2-0caa-4529-8673-f38cead83540)


Запуск докера в фоновом режиме:

`````sudo docker compose up -d`````

![5](https://github.com/user-attachments/assets/df948991-bb5e-461b-aad6-99e4e2d5fc84)


Отсановка докера, без удаления контейнерова:

`````sudo docker compose stop`````

![6](https://github.com/user-attachments/assets/d0bea8b8-6b7c-4126-a05b-8c880e8d9b37)


Удаляет контейнеры:

`````sudo docker compose down`````

![7](https://github.com/user-attachments/assets/35702b54-250f-4ca3-a7e6-9394ce0c2f6e)


Отображает текущее состояние:
`````sudo docker compose ps`````

![image](https://github.com/user-attachments/assets/ac579dd5-ec3f-4fb7-9700-d96002a494a2)


клонируем репозиторий гитзаба себе в виртуалку:

`````git clone https://github.com/K-N-Viktoria/korchagina`````

![8](https://github.com/user-attachments/assets/9040493f-3695-4182-87df-2d710841c1bb)

<h1> Grafana </h1>

Запускаем браузер и переходим по localhost:3000 и вводим В логин: admin, В пароль: admin:

![10](https://github.com/user-attachments/assets/8d2211d4-52d6-4ed6-adbe-2674f53229e0)


Выбираем DASHBOARDS:

![11](https://github.com/user-attachments/assets/4dd0ff47-c8cf-486e-abfd-e5a659597d19)

Выбираем Prometheus:

![image](https://github.com/user-attachments/assets/ce62bf54-ff02-453e-8552-4c9164dde7c5)


В ссылке пишем `````http://prometheus:9090`````, в аутентификации выбираем Basic authentication, в логин и пароль так-же вводим admin:

![image](https://github.com/user-attachments/assets/b382d04e-cb8e-4239-b9f3-bcb73aff7751)

Опять переходим на вкладку DASHBOARDS, и выбираем import a dashboard:

![image](https://github.com/user-attachments/assets/b20064de-dbf9-4213-933e-005460728750)


После чего вводим имя для dashboarda и выбираем prometheus:

![13](https://github.com/user-attachments/assets/4b2b6443-5660-4b06-80c8-3f71871b6ce1)

И всё готово:

![14](https://github.com/user-attachments/assets/4e0a90af-4e27-471c-8119-954aa91babee)

<h1> VictoriaMetrics </h1>

Для создания VictoriaMetrics, мы сначала заходим в графану с помощью команды: 

`````cd grafana_stack_for_docker`````

Затем запускаем докер командой:

`````sudo docker compose up -d`````

После проделанных комнад, мы переходим по  localhost:3000 и создаём новый dashboard :

![Снимок экрана 2025-04-03 204035](https://github.com/user-attachments/assets/fb9b6159-4a70-4188-9bab-5253cc470242)

Далее создаём VictoriaMetrics:

![Снимок экрана 2025-04-03 204144](https://github.com/user-attachments/assets/d5bb6e80-7cc6-460b-bc5e-71f56f73035c)

После создания, переходим в консоль и вводим комнаду:

`````echo -e "# TYPE light_metric1 gauge\nlight_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus`````

Потом переходим по ссылкам http://localhost:8428/api/v1/query и http://localhost:8428
В ссылке http://localhost:8428 мы переходим в vmui, после вводим в строку light_metric1:

![image](https://github.com/user-attachments/assets/4c3255c9-9e6f-4f4c-8164-0a10382787c4)

После возращаемся к нашей VictoriaMetrics, редактируя её, указываем в Default editor - code:

![Снимок экрана 2025-04-03 204207](https://github.com/user-attachments/assets/f3ed1016-ba32-43dc-b946-9ed756e8d4cd)

В заверешеия, мы сохраняем изменения и переходим в DASHBOARDS, выбираем нашу VictoriaMetrics и указываем в ней light_metric1 и получем результат:

![image](https://github.com/user-attachments/assets/03a7f1d9-0f7d-4495-aedb-36298fd6076a)





