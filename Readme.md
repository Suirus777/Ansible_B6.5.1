Skillfactory: Module 6 - Ansible!!!!

Задание B6.5.1

1. Напишите плейбук, который будет на удаленной системе создавать пользователя user1 и задавать ему SSH-ключ (создавая заданный ключ в /home/user1/.ssh/id_rsa.pub). 
   Ключ не должен передаваться в открытом виде. Используйте для шифрования ключа ansible-vault. Ключ можете сгенерировать, используя SSH-keygen.
   Ответ:
   Был создан playbook: useradd.yml
   С помощью ssh-keygen был сгенерирован новый ключ User1.pub
   Ключ User1.pub был зашифрован ansible-vault: ansible-vault encrypt --ask-password ~/.ssh/user1.pub
   Для создания пользователя на удалённом сервере и расшифровки ssh ключа user1.pub 
   Использовалась команда: ansible-playbook --ask-vault-pass useradd.yml

2. Создайте плейбук, который устанавливает, либо удаляет почтовый сервер postfix в зависимости от тега.
   При запуске ansible-playbook <путь_к_плейбуку> --tags "init postfix" должен устанавливаться и запускаться с конфигурацией по умолчанию. 
   При запуске ansible-playbook <путь_к_плейбуку> --tags drop postfix должен удаляться с машины.
   Ответ:
   Был создан playbook: postfix.yml
   Были --tags "init postfix" и --tags drop postfix для установки и удаления postfix в зависимости от использования тэга в команде.

   Команда для установки postfix: ansible-playbook postfix.yml --tags "init postfix"
   Postfix был установлен: root@devops1:/home/odmin#  ps aux | grep postfix
                           root      102991  0.0  0.4  38068  4500 ?        Ss   14:43   0:00 /usr/lib/postfix/sbin/master -w
                           postfix   102994  0.0  0.6  38336  6152 ?        S    14:43   0:00 pickup -l -t unix -u -c
                           postfix   102995  0.0  0.6  38388  6168 ?        S    14:43   0:00 qmgr -l -t unix -u
                           root      103818  0.0  0.0   6432   724 pts/0    S+   14:46   0:00 grep --color=auto postfix

   Команда для удаления postfix: ansible-playbook postfix.yml --tags "drop postfix"
   Postfix был удалён:     root@devops1:/home/odmin# ps aux | grep postfix
                           root      104600  0.0  0.0   6432   656 pts/0    S+   14:53   0:00 grep --color=auto postfix
                                      
