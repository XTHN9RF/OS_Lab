# Лабораторна робота №4

## Тема: "Створення сценарію terraform для надання інфраструктури в хмарі GCP (або AWS)"

Виконав студент ІІІ курсу

Напрям "ІПЗ", група 1.2

Дуран Владислав Юрійович

### План:
1. Створіть один екземпляр (зображення: ubuntu 20.04)

Перед виконанням цього завдання я створив акаунт на AWS та встановив тераформ на убунту (за допомогою sudo apt install terraform)

У графічному інтерфейсі AWS я отримав secret та access ключі щоб в подальшому використати їх у своєму конфіг-файлі


![image1](/assets/terraform_config.png)

Далі я виконав команду terraform init

![image2](/assets/terraform_init.png)

Після чого terraform plan

![image3](assets/terraform_plan.png)

Далі terraform apply

![image4](assets/terraform_apply.png)

Вигляд інтерфейсу в AWS

![image5](assets/terraform_instance.png)

2. Дозвольте трафік HTTP/HTTPS на мережевому адаптері

На AWS я створив security_group, де поставив дозволи для трафіку через HTTP та HTTPS

![image5](assets/security_group_terraform.png)

Після чого запустив команди:

```
terraform plan
terraform apply
```

Вигляд інтерфейсу в AWS

![image6](assets/security_group_add.png)

3. Надайте один відкритий ключ SSH для створеного екземпляра

Генерація ssh ключів (паблік та прайват)

![image7](assets/ssh_key.png)

Також потрібно додати у конфіг ці рядки:

```
ingress {
    description = "SSH"
    from_port = 22
    to_port = 22
    protocol = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
}
```

Далі додаю ключ до конфігу та дописую його до resource 

![image8](assets/shh_key_add.png)


4. Встановіть веб-сервер (HTTP-сервер Apache / HTTP-сервер NGINX) за сценарієм bash

На сайті AWS знаходжу команду підключення до інстансу через SSH

![image9](assets/move_to_aws.png)

Далі я створив баш скрипт для встановлення та запуску сервера

![image10](assets/bash_scenario.png)

Запуск баш

![image11](assets/setup_apache.png)

Далі я створюю html файл, змінюю йому дозволи та переміщаю у іншу папку для запуску

![image12](assets/creating%20_file.png)

Заповнюю цей файл

![image13](assets/filled_file_index.png)

Запущена сторінка

![image14](assets/completed_page.png)