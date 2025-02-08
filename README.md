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


• Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose
![image](https://github.com/user-attachments/assets/1a9ddd83-6878-4032-9608-30b7ca91a9f3)


