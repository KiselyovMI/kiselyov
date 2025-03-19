# kiselyov
Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Иметь образ Linux Выделить 2+ ядер. Выделать 4096+ МБ оперативы. При установки операционной системы, нужно будет выбрать английский язык.

Далее переходим к установке docker с использованием grafana, вводим следующий набор команд:

1. >sudo yum install wget

• Устанавливает утилиту wget на вашу систему

![image](https://github.com/user-attachments/assets/d4bc09d5-f41a-4f34-9eff-ea392d03784d)

2. >sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

• Скачиваем файл репозитория
![image](https://github.com/user-attachments/assets/7bc73d5c-6ccd-4dcd-86f9-165f0fa6c1c2)

3. >sudo yum install docker-ce docker-ce-cli containerd.io

• Устанавливаем docker
![image](https://github.com/user-attachments/assets/f2281b18-d0eb-4b81-9c09-9c13032d2146)

4. >sudo systemctl enable docker --now

• Запускаем его и разрешаем автозапуск

5. >sudo yum install curl

• Для этого сначала убедимся в наличие пакета curl

6. >COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)

• Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose
![image](https://github.com/user-attachments/assets/1a9ddd83-6878-4032-9608-30b7ca91a9f3)
![image](https://github.com/user-attachments/assets/cc5a539e-2a58-4c57-af79-cf17618b196b)

7. >sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

• Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

![image](https://github.com/user-attachments/assets/688352dd-69d5-4f39-a7b2-38e5a2b42fdb)

8. >sudo chmod +x /usr/bin/docker-compose

• Предоставление прав на выполнение файла docker-compose.

9. >docker --version

• Проверка установленной версии Docker.

![image](https://github.com/user-attachments/assets/7cab30e6-ffd6-4237-9919-2c35ddf18f53)

• Можно скачать git прямо из командной строки прописав Y

10. >git clone https://github.com/skl256/grafana_stack_for_docker.git

• Выдаст ошибку и предложит скачать git, согласиться и продолжить

![image](https://github.com/user-attachments/assets/7309f8cd-bd42-4e27-bb90-3d7c763f9239)

11. >cd grafana_stack_for_docker

• переход в папку

12. >sudo mkdir -p /mnt/common_volume/swarm/grafana/config

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

13. >sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}

• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

14. >sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}

• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе

15. >touch /mnt/common_volume/grafana/grafana-config/grafana.ini

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

16. >cp config/* /mnt/common_volume/swarm/grafana/config/

• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

17. >mv grafana.yaml docker-compose.yaml

• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls

18. >sudo docker compose up -d

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.

![image](https://github.com/user-attachments/assets/4f4a25b2-54bd-43ab-87ea-e3bc2305513b)
![image](https://github.com/user-attachments/assets/f15de654-f593-4a8c-970d-46b10d3a6496)

19. • Открываем браузер и переходим по адресу localhost:3000
>Вводим логин и пароль

>Логин: admin
>Пароль: admin

20. • Попадаем на страницу Home
![image](https://github.com/user-attachments/assets/891e2151-b6f0-4c0f-876c-494ba7952f53)


• -d Он означал что мы вошли в "detached mode" (фоновый режим)

![image](https://github.com/user-attachments/assets/079c82ae-9e2f-4468-81b3-a54a0e5fa649)

>sudo docker compose stop

![image](https://github.com/user-attachments/assets/51e73aa3-e79d-4c71-af92-2a469701558a)

 >Что делает: Останавливает все запущенные контейнеры, определённые в файле docker-compose.yml, но не удаляет их (рис. 2).
 >Пояснение: Контейнеры остаются в состоянии "остановленных", и их можно снова запустить командой docker compose start.
 >Пример: Когда вам нужно временно остановить работу приложения, но сохранить состояние контейнеров для дальнейшего использования.

• sudo docker compose down

![image](https://github.com/user-attachments/assets/13623d59-a119-4046-b06c-94ef296265b9)

>Что делает: Полностью останавливает и удаляет все контейнеры, сети, объёмы данных (volumes) и другие ресурсы, созданные с помощью docker-compose.yml (рис. 3).
>Пояснение: Это более радикальная команда, чем stop. После выполнения этой команды все данные, хранящиеся в объёмах, будут удалены, если явно не указано их сохранение.
>Пример: Когда вам нужно полностью очистить окружение и начать с чистого листа.

• sudo docker compose ps

![image](https://github.com/user-attachments/assets/abc1d2b2-2582-4f68-8d3d-b9ce5b07f827)

>Что делает: Показывает статус всех контейнеров, определённых в файле docker-compose.yml (рис. 4).
>Пояснение: Команда выводит список контейнеров вместе с их состоянием (запущен/остановлен), портами, сетями и другими параметрами.
>Пример: Используется для мониторинга текущего состояния контейнеров.

• Командой выполняем клонирование удаленного Git-репозитория с GitHub на компьютер

>git clone https://github.com/KiselyovMI/kiselyov

![image](https://github.com/user-attachments/assets/4361eb2d-9d8a-4ee6-8793-3f55a899a78e)

• Перенёс prometheus.yaml в корневую папку Grafana 
![image](https://github.com/user-attachments/assets/2a49256e-3994-44bc-9589-92341fdad4a6)

• Удостоверился в правильном нахождении файла prometheus.yaml в папке grafana/config
![image](https://github.com/user-attachments/assets/1e83056c-756c-448b-88c8-918e6268a262)

• запускаем docker compose в фоновом режиме
• переходим на сайт localhost:3000
>Пользователь и Пароль GRAFANA: admin

>Код графаны: 3000

>Код прометеуса: http://prometheus:9090

• в меню выбираем вкладку Dashboards и создаем Dashboard

 >нажимаем кнопку +Добавить визуализацию, а затем «Настроить новый источник данных»
 >выбираем Prometheus

![image](https://github.com/user-attachments/assets/92792b69-ba77-4591-9543-87bb325f6d28)

• Заполняем данные в открывшемся окне
 
 • Пункт Connection
  >http://prometheus:9090
 
 • Пункт Authentication
 
  >Базовая аутентификация
  
  >Пользователь: admin
  
  >Пароль: admin
  
  >Нажимаем на Save & test и должно показывать зелёную галочку
  
 • в меню выбираем вкладку Dashboards и создаем Dashboard

   >жмем кнопку "Import dashboard"

  ![image](https://github.com/user-attachments/assets/c60048cc-8fef-41d4-9060-8249017717b4)

  >В пункт **Find and import dashboards for common applications at grafana.com/dashboards:** вписываем 1860

  ![image](https://github.com/user-attachments/assets/a1afba2c-a53e-43d6-bde7-ed83ee48a53a)

 • жмем кнопку Load

  >Select Prometheus ждем кнопку "Import"

В итоге открывается такой Dashboard для мониторинга загрузки ОС

![image](https://github.com/user-attachments/assets/db864a79-27c3-4d8e-9069-e695d4743a2f)

# Victoria

• Вводим команду 

>echo -e "# TYPE light_metric1 gauge\nlight_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus 

которая, отправляет бинарные данные (например, метрики в формате Prometheus) на локальный сервер, который слушает на порту 8428.

![image](https://github.com/user-attachments/assets/e5eb5987-1cee-4342-8575-84b465923970)

• Переходим в браузере по ссылке http://localhost:8428/, открывается такое меню в нём нужно выбрать vmui

![image](https://github.com/user-attachments/assets/aa0ab359-3045-4fb8-8845-9cf4c8a4d83a)

• Вписываем light_metric1 и нажимаем Execute Query

![image](https://github.com/user-attachments/assets/301dd558-54d7-4725-a989-5b73fe942389)
![image](https://github.com/user-attachments/assets/5cc2a84c-b504-4b5b-962d-643a2479d6ba)

• Переходим на http://localhost:3000 выбираем Dashboard и нажимаем New Dashboard, далее Add Visualization

![image](https://github.com/user-attachments/assets/1fbe37c6-76bb-482a-a01d-cc1dcfc9f396)

• Нажимаем Configure a new data source и выбираем Prometheus

![image](https://github.com/user-attachments/assets/cf7e88d4-1420-47ba-b17f-4f7b43c6c1ae)

• Вписываем:

>Name: vik

>Connection: http://victoriametrics:8428

>Нажимаем Save & TestВписываем:

![image](https://github.com/user-attachments/assets/953a1bea-bad6-437d-a4cb-60a01b169d85)

• Вписываем light_metric1

![image](https://github.com/user-attachments/assets/be166b29-8ae5-4424-9883-8aabdbf8d3d0)

• Выходит панель с графиком, где есть активность light_metric1

![image](https://github.com/user-attachments/assets/5142f70a-a712-4580-95ce-3c75d82e39db)
