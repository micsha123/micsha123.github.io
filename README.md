## Инструкция по созданию своего vpn-соединения

Что понадобится:
1) банковская карта для списания средств за аренду
2) документ (водительское удостоверение или паспорт для верификации аккаунта) - может потребоваться, может нет
3) ноутбук (желательно с macOS)

Все  5 простых пунктов (каждый пункт будет ниже подробно разобран):
1) арендовать свой виртуальных сервер
2) установить на него vpn-программу
3) скачать сертификат на свое устройство
4) установить сертификат на устройства
5) запустить vpn

Касательно аренды серверов нас будет интересует только одно - его нахождение зарубежом.
Для доступа к заблокированному контенту нам подойдет самая дешевая/базовая конфигурация, доступная на известных хостингах.

От себя могу выделить несколько хостингов, самые известные из которых:
- [Digital Ocean](https://www.digitalocean.com/) (на 25.02.2022 не принималась банковская карта из России - возможно, санкции)
Если есть аккаунт - отлично, если нет, рекомендую второй вариант:
- [Hetzner](https://www.hetzner.com/)

Мой выбор лежит в сторону **Hetzner** - за 4,6 евро вы получаете большой объем траффика (_хоть видео на YouTube смотри_), а цена одна из самых низких.
Дальнейшая инструкция будет касатся развертывания VPN на этом хостинге.

### Аренда сервера

1) Для начала заводим аккаунт на сайте https://www.hetzner.com/
2) После регистрации аккаунта на почту прилетит письмо с верификацией почты аккаунта
3) В процессе верификации можете ввести любые данные, касающиеся своего имени, адреса, телефона и прочее
4) Далее вам будет предложено привязать банковскую карту для оплаты аренды - опция <img width="50" alt="Снимок экрана 2022-02-25 в 22 38 52" src="https://user-images.githubusercontent.com/100441263/155784154-9b765bfc-e8c4-49d9-823d-60adddc4b4c4.png">
5) По завершению ввода платежной информации вам может быть предложена верификация аккаунта через сервис проверки документов - делается два фото и сопоставляются лица на них
5) В финале откроется следующий экран, на котором виден список созданных проектов (сейчас их у нас нет):
<img width="1430" alt="Снимок экрана 2022-02-26 в 12 50 09" src="https://user-images.githubusercontent.com/100441263/155839018-2829fe25-3e6b-47e8-8642-58d502f1bb5d.png">

Для аренды сервера нажмите на кнопку "NEW PROJECT" - задайте любое имя, например:
<img width="553" alt="Снимок экрана 2022-02-26 в 13 13 15" src="https://user-images.githubusercontent.com/100441263/155839294-07858806-84a3-42fd-8c6f-862ebae7fb15.png">


**Внимание:**
Если вы увидели такое окно:
<img width="100" alt="Снимок экрана 2022-02-26 в 12 50 51" src="https://user-images.githubusercontent.com/100441263/155839019-a3663e89-2c05-4614-8177-75e350633178.png">
, значит процедура верификации документов не пройдена - повторите ее еще раз (кликнув по ссылке из описания).


После этого экран сменится на следующий:
<img width="1430" alt="Снимок экрана 2022-02-26 в 13 22 32" src="https://user-images.githubusercontent.com/100441263/155839601-b2065267-f94c-47e3-b477-3deba3b8382e.png">

Открываем наш новосозданный проект (в данном случае _Azaza_) и в открывшемся окне нажимаем на кнопку "ADD SERVER":
<img width="631" alt="Снимок экрана 2022-02-26 в 13 32 53" src="https://user-images.githubusercontent.com/100441263/155839970-c3b5d0ec-d372-4fd4-9721-ba8287753ab6.png">

Далее пройдемся по графам:
1) Location - местоположение сервера. Выбирайте любое (моя рекомендация - Хельсинки или Германия)
2) Image - здесь достаточно выбора по умолачанию в виде **Ubuntu**
3) Type - оставляем вариант **Standart**, а в списке конфигураций ниже выбираем самый дешевый вариант
4) Volume 5) Network 6) Firewalls 7) Additional features и 9) Name - оставляем без изменений
8) SSH key - важный для дальнейшей работы пункт. Остановимся сейчас на нем:
8.1) откройте в macOS Терминал
8.2) введите команду ```ssh-keygen -t rsa``` и нажмите ```Enter```
8.3) после этого вам дважды будут заданы вопросы о расположении ключа и пасс-фразы - пропускайте их с помощью ```Enter```
8.4) в конце генерирования ключа вы увидите примерно следующее:
```
Your identification has been saved in /Users/myname/.ssh/id_rsa.
Your public key has been saved in /Users/myname/.ssh/id_rsa.pub.
The key fingerprint is:
ae:89:72:0b:85:da:5a:f4:7c:1f:c2:43:fd:c6:44:38 myname@mymac.local
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|         .       |
|        E .      |
|   .   . o       |
|  o . . S .      |
| + + o . +       |
|. + o = o +      |
| o...o * o       |
|.  oo.o .        |
+-----------------+
```
Поздравляю, ключ успешно сгененировался!
8.5) Теперь вводим команду в терминал ```pbcopy < ~/.ssh/id_rsa.pub``` - таким образом ключ будет скопировано в буффер обмена. Осталось его ввести!)
8.6) На сайте нажимаем **Add SSH** и вводим наш ключ в большое окно ввода , в графе **Name** произойдет автоподстановка имени
<img width="927" alt="Снимок экрана 2022-02-26 в 13 55 29" src="https://user-images.githubusercontent.com/100441263/155840608-3bafd99c-0ae6-4e27-aac9-69bc08d5e6a8.png">
8.7) Сохраняем ключ по кнопке **ADD SSH KEY**
8.8) В финале проверяем, что количество арендуемых серверов не превышает одного, смотрим на конечную стоимость - и подтверждаем создание сервера
<img width="1360" alt="Снимок экрана 2022-02-26 в 16 32 55" src="https://user-images.githubusercontent.com/100441263/155845195-84056154-d1ff-4dc1-83f0-2589bfc49051.png">

Готово! Сервер арендован!

### Установка VPN на сервер

В открытом окне нас интересует одна информация - ip адрес нашего сервера. Увидеть можно в списке, который показывается после создания сервера из предыдущего пункта:
<img width="1362" alt="Снимок экрана 2022-02-26 в 16 35 15" src="https://user-images.githubusercontent.com/100441263/155845296-0d0284c1-a8b9-4aef-ac6c-2e5fc234a8a4.png">

Как видно, наш адрес - ```65.21.188.95```.

Отлично, далее, откроем Терминал в macOS и вводим в открывшуюся консоль ```ssh root@{ip_адрес_сервера}```, например для нашего адреса:
```
ssh root@65.21.188.95
```

При первом соединении с сервером может последовать вопрос, касающийся авторизации - просто пишем в ответ ```yes```:
```
The authenticity of host '65.21.188.95 (65.21.188.95)' can't be established.
ED26627 key fingerprint is SHA256:t3QRXWLJ/IZFDjejyLVFuvaYJYt3QRXs5EJzejyLVFuvs5EkXWLJlISc.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? **yes**
```

После подключения вы увидете строку, начинающуюся с названия вашего сервера на хостинге, в нашем случае:
```
root@ubuntu-2gb-hel1-4:~# 
```
Поздравляю, вы подключены к своему удаленному серверу!

Осуществим установку vpn-сервиса на свой сервер, для этого вводим строку в консоль:
```
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```

Произойдет установка и откроется помощник для настройки сервиса. Первым вопросом будет протокол, используем рекомендуемые настройки:
```
Which protocol should OpenVPN use?
   1) UDP (recommended)
   2) TCP
Protocol [1]: **1** 

What port should OpenVPN listen to?
Port [1194]: **1194**

Select a DNS server for the clients:
   1) Current system resolvers
   2) Google
   3) 1.1.1.1
   4) OpenDNS
   5) Quad9
   6) AdGuard
DNS server [1]: **1**
```

Затем нам потребуется ввести название для первого клиента. В данном случае, клиентом будем считать устройство, которое будет подключаться к VPN-сервису.
Рекомендую использовать имена понятные для вас, вроде, **mobile** или **desktop** - для телефона и ноутбука, соответственно.
**ВАЖНО:** запомните/запишите эти имена, они пригодятся в следующей главе!
```
Enter a name for the first client:
Name [client]: **mobile**  
```

Далее вы увидете текст о готовности установки к старту - нажмите любу клавишу.
```
OpenVPN installation is ready to begin.
Press any key to continue...
```

Оставляем установщик на некоторое время - примерно минуту/две.
После успешной установки мы увидим в конце консоли следующее:
```
Finished!

The client configuration is available in: /root/mobile.ovpn
New clients can be added by running this script again.
root@ubuntu-2gb-hel1-4:~# 
```

Поздравляю, VPN уже работает на сервере - и у вас готов один сертификат! 
Для добавления сертификатов/устройств, которые могут подключаться к серверу - еще раз запустите скрипт, введя в консоль:
```
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```
Меню будет немного отличать от увиденного ранее, общий вид будет следующим:
```
Select an option:
   1) Add a new client
   2) Revoke an existing client
   3) Remove OpenVPN
   4) Exit
Option: **1**
```
Введите цифру 1 - дальше увидите знакомый сценарий добавления нового клиента!
Приступим к скачиванию сертификата!)

### Скачивание сертификата с сервера

Для скачивания сертификата выйдем из консоли сервера, введя команду ```exit```:
```
root@ubuntu-2gb-hel1-4:~# **exit**
```

Далее вводим в терминал команду ```sftp root@{ip_адрес_сервера}:{имя_клиента}.ovpn ~/```, например, для нашего клиента ```mobile``` будет так:
```
sftp root@65.21.188.95:mobile.ovpn ~/
```
Появится текст о выгрузке файла с сервера:
```
Connected to 65.21.188.95.
Fetching /root/mobile.ovpn to /Users/dmitrydenisenko/mobile.ovpn
/root/mobile.ovpn                             100% 4996    36.2KB/s   00:00    
Connection closed. 
```
Теперь вы можете найти полученный файл у себя на macbook'е:
1) откройте Finder
2) нажмите ```COMMAND```+```SHIFT```+```H```
3) в списке файлов находим файл с именем клиента, например, **mobile.ovpn**

Отлично, дальше мы установим приложение для запуска VPN

### Установить сертификата на macOS и запуск

Установим необходимые приложения для работы с нашим VPN-сервером:
(Tunnelblick)[https://tunnelblick.net/downloads.html#:~:text=Stable-,Tunnelblick%203.8.7a,-(build%205770%2C%20macOS] для macOS

Установка для Tunnelblick простая - достаточно открыть программу во вкладке Конфигурации и перенести наш полученный файл **mobile.ovpn**,, как показано на рисунке:
<img width="911" alt="Снимок экрана 2022-02-26 в 17 36 06" src="https://user-images.githubusercontent.com/100441263/155847090-4eda5b75-77f6-49dc-8ec3-a36a7649bd41.png">
Система предложит выбрать пользователей системы для доступа к VPN и попросить ввести пароль системы.

После этого установленная конфигурация отобразится в списке:
<img width="198" alt="Снимок экрана 2022-02-26 в 17 39 46" src="https://user-images.githubusercontent.com/100441263/155847136-83fdfeb6-451e-478a-bbbd-c11f7be1dbdf.png">

Осталось проверить подключение - в верхней части экрана нажмите на значок Tunnelblick и выберите пункт "Соединить ...":
<img width="208" alt="Снимок экрана 2022-02-26 в 17 40 26" src="https://user-images.githubusercontent.com/100441263/155847150-d18007b4-96a2-44a3-a62f-3f94a20b9c39.png">

Дождитесь соединения и проверьте работу VPN - для этого можно попробовать открыть недоступный ранее сайт, не нарушающий законов РФ.


### Установить сертификата на телефон и запуск
Установим необходимые приложения для работы с нашим VPN-сервером:
- OpenVPN [версия для Android](https://play.google.com/store/apps/details?id=de.blinkt.openvpn&hl=ru&gl=US)
- OpenVPN [версия для iOS](https://apps.apple.com/ru/app/openvpn-connect/id590379981)

Затем отправим наш файл **mobile.ovpn** на устройство любым удобным для вас способом - можно по email, можно через мессенджеры - и открываем файл.
По итогу должно открыться приложение OpenVPN с настройками - сохраняем их!

После этого у вас будет примерно следующий вид приложения:
![IMAGE 2022-02-26 17:50:26](https://user-images.githubusercontent.com/100441263/155847457-788011f0-fc31-4183-998d-7b93abd438b8.jpg)

Для включения VPN на мобильном устройстве достаточно включить тумблер возле названия - теперь VPN соединение доступно для всех приложений на вашем смартфоне!)
