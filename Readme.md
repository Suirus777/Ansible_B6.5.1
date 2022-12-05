Skillfactory: Module 6 - Ansible!!!!</br>

Задание B6.5.1</br>

1. Напишите плейбук, который будет на удаленной системе создавать пользователя user1 и задавать ему SSH-ключ (создавая заданный ключ в /home/user1/.ssh/id_rsa.pub). </br>
   Ключ не должен передаваться в открытом виде. Используйте для шифрования ключа ansible-vault. Ключ можете сгенерировать, используя SSH-keygen.</br>
   
   Ответ:</br>
   Был создан playbook: <b>useradd.yml </b></br>
   С помощью ssh-keygen был сгенерирован новый ключ User1.pub</br>
   Ключ User1.pub был зашифрован ansible-vault: <b>ansible-vault encrypt --ask-password ~/.ssh/user1.pub </b></br>
   Для создания пользователя на удалённом сервере и расшифровки ssh ключа user1.pub использовалась команда: 
   </br> <b>ansible-playbook --ask-vault-pass useradd.yml</b></br>

2. Создайте плейбук, который устанавливает, либо удаляет почтовый сервер postfix в зависимости от тега.</br>
   При запуске ansible-playbook <путь_к_плейбуку> --tags "init postfix" должен устанавливаться и запускаться с конфигурацией по умолчанию. </br>
   При запуске ansible-playbook <путь_к_плейбуку> --tags drop postfix должен удаляться с машины.</br>
   
   Ответ:</br>
   Был создан playbook: <b>postfix.yml</b></br>
   Были добавлены тэги: <b>--tags "init postfix" и --tags drop postfix </b>для установки и удаления postfix в зависимости от использования тэга в команде.</br>

   Команда для установки postfix: <b>ansible-playbook postfix.yml --tags "init postfix" </b></br>
   Postfix был установлен:<b>root@devops1:/home/odmin#  ps aux | grep postfix</br>
                           root      102991  0.0  0.4  38068  4500 ?        Ss   14:43   0:00 /usr/lib/postfix/sbin/master -w </br>
                           postfix   102994  0.0  0.6  38336  6152 ?        S    14:43   0:00 pickup -l -t unix -u -c </br>
                           postfix   102995  0.0  0.6  38388  6168 ?        S    14:43   0:00 qmgr -l -t unix -u </br>
                           root      103818  0.0  0.0   6432   724 pts/0    S+   14:46   0:00 grep --color=auto postfix </br>
</b>
   Команда для удаления <b>postfix: ansible-playbook postfix.yml --tags "drop postfix"</b></br>
   Postfix был удалён:  <b>   root@devops1:/home/odmin# ps aux | grep postfix </br>
                           root      104600  0.0  0.0   6432   656 pts/0    S+   14:53   0:00 grep --color=auto postfix</br></b>
                                      
