# korchagina

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

Открываем файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя:

 `````sudo vi docker-compose.yaml`````
 
![image](https://github.com/user-attachments/assets/fed6e754-011f-499b-8df2-8d9a6dfb66c3)
![image](https://github.com/user-attachments/assets/375b6bc4-6d93-49bc-b02a-832b90ecfe5e)


