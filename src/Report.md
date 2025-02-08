# Отчёт по DO01


## Part 1. Установка ОС

1. Скачал .iso образ системы с официального сайта ubuntu
2. Установил VM VirtualBox
3. Создал и настроил новую виртуальную машину
4. Запустил машину и прошёл процесс стандартной установки
5. Проверил версию Ubuntu через `cat /etc/issue`

![img.png](Screenshots/img.png)


## Part 2. Создание пользователя

1. Создал нового пользователя `new_user` и задал его основные параметры через `adduser`

![img2.png](Screenshots/img2.png)

2. Добавил нового пользователя `new_user` в группу `adm` через `usermod`

![img3.png](Screenshots/img3.png)

3. Проверил список всех пользователей через `cat /etc/passwd`

![img4.png](Screenshots/img4.png)

Новый пользователь был успешно добавлен


## Part 3. Настройка сети ОС

1. Изменил имя машины через редактирование файлов `/etc/hostname` и `/etc/hosts`

![img6.png](Screenshots/img6.png)

![img7.png](Screenshots/img7.png)

![img8.png](Screenshots/img8.png)

![img9.png](Screenshots/img9.png)

2. Установил свою временную зону через `timedatectl set-timezone`

![img10.png](Screenshots/img10.png)

3. Вывел имена сетевых интерфейсов через `ls /sys/class/net`

![img11.png](Screenshots/img11.png)

> Интерфейс `lo` (loopback) - это виртуальный сетевой интерфейс по умолчанию Linux. Является локальной петлей, имеющей IP-адрес 127.0.0.1.

4. Попытался получить IP-адрес от DHCP-сервера через `dhclient`, но IP уже был выдан

![img12.png](Screenshots/img12.png)

> `DHCP` (Dynamic Host Configuration Protocol) - это сетевой протокол, который позволяет устройствам в сети автоматически получать и присваивать IP-адреса, а также другие параметры

5. Вывел внутренний и внешний IP-адрес интерфейса через `ip route` и `curl ifconfig.me`, соответственно

![img13.png](Screenshots/img13.png)

![img14.png](Screenshots/img14.png)

6.  Отключил получение IP-адреса по dhcp, задал статический IP-адрес и DNS-сервера в файле `/etc/netplan/*.yaml` и применил настройки через `netplan-apply`

![img15.png](Screenshots/img15.png)

![img16.png](Screenshots/img16.png)

![img17.png](Screenshots/img17.png)

7. Перезагрузил систему и проверил, что настройки сохранились через `ifconfig`

![img18.png](Screenshots/img18.png)

![img19.png](Screenshots/img19.png)

8. Пропинговал хосты `1.1.1.1` и `ya.ru` через `ping`

![img20.png](Screenshots/img20.png)


## Part 4. Обновление ОС

1. Получил список доступных для обновления пакетов через `apt update`

![img21.png](Screenshots/img21.png)

2. Обновил пакеты через `apt upgrade`

![img22.png](Screenshots/img22.png)

3. Проверил, что все обновления установлены

![img23.png](Screenshots/img23.png)


## Part 5. Использование команды sudo

> Команда `sudo` (substitute user and do) позволяет подменить текущего пользователя на `root` и выполнять команды от имени суперпользователя с ведением протокола работы

1. Дал новому пользователю права суперпользователя, путем добавления его в группу `sudo` через `usermod -aG sudo`

![img24.png](Screenshots/img24.png)

2. Переключился на нового пользователя через `su`, затем проверил текущее название машины через `hostnamectl`, затем поменял имя машины через `hostnamectl set-hostname` 

![img25.png](Screenshots/img25.png)

![img26.png](Screenshots/img26.png)


## Part 6. Установка и настройка службы времени

1. Вывел текущее время и дату через `date`
 
![img27.png](Screenshots/img27.png)

2. Включил службу автоматической синхронизации времени через `timedatectl set-ntp true`

![img28.png](Screenshots/img28.png)

3. Проверил успешность настройки службы `NTP`

![img29.png](Screenshots/img29.png)


## Part 7. Установка и использование текстовых редакторов

### Создание и сохранение файлов

* **Vim**. Для редактирования нажать `I`, для выхода в режим команд `ESC`, для сохранения `SHIFT + : -> wq` 

![img30.png](Screenshots/img30.png)

![img31.png](Screenshots/img31.png)

* **Nano**. Для выхода нажать `CTRL + X`, затем `Y` для сохранения, и `ENTER` для подтверждения записи в файл

![img32.png](Screenshots/img32.png)

![img33.png](Screenshots/img33.png)

* **Joe**. Для выхода нажать `CTRL + K`, а затем `X` для сохранения

![img34.png](Screenshots/img34.png)

![img35.png](Screenshots/img35.png)

### Редактирование файлов без сохранения

* **Vim**. Для выхода без изменений нажать `SHIFT + :`, а затем ввести `q!` 

![img36.png](Screenshots/img36.png)

* **Nano**. Для выхода без изменений нажать `CTRL + X`, а затем `N`

![img37.png](Screenshots/img37.png)

* **Joe**. Для выхода без изменений нажать `CTRL + K`, потом ввести `Q`, а затем `N`

![img38.png](Screenshots/img38.png)

### Поиск по содержимому файлов

* **Vim**. Для обычного поиска ввести `/` и слово

![img39.png](Screenshots/img39.png)

* **Vim**. Для поиска с заменой `SHIFT + :`, а затем команду `%s/word_to_replace/replacement/g` и нажать `ENTER`

![img40.png](Screenshots/img40.png)

![img41.png](Screenshots/img41.png)


* **Nano**. Для обычного поиска нажать `CTRL + W`, затем ввести слово

![img42.png](Screenshots/img42.png)

* **Nano**. Для поиска с заменой нажать `CTRL + \`, затем ввести заменяемое слово и слово для замены

![img43.png](Screenshots/img43.png)

![img44.png](Screenshots/img44.png)

![img45.png](Screenshots/img45.png)


* **Joe**. Для обычного поиска нажать `CTRL + K -> F`, ввести искомое слово и нажать `Enter`

![img46.png](Screenshots/img46.png)

* **Joe**. Для поиска с заменой нажать `CTRL + K -> F`, ввести заменяемое слово, `ENTER`, выбрать `R`, ввести слово для замены, подтвердить `Y`

![img47.png](Screenshots/img47.png)

![img48.png](Screenshots/img48.png)

![img49.png](Screenshots/img49.png)


## Part 8. Установка и базовая настройка сервиса SSHD
 
1. Установил `SSH` через `apt install`

![img50.png](Screenshots/img50.png)

2. Добавил службу `SSH` в автозагрузку через `systemctl enable`

![img51.png](Screenshots/img51.png)

3. Открыл конфигурационный файл службы `SSHd` по пути `/etc/ssh/sshd_config` и поменял строку с портом на необходимую, а затем перезапустил службу через `systemctl restart`

![img52.png](Screenshots/img52.png)

![img53.png](Screenshots/img53.png)

![img54.png](Screenshots/img54.png)

4. С помощью команды `ps -C` нашёл процесс по его имени

![img55.png](Screenshots/img55.png)

**Ключи ps:**

-A, -e, (a) - выбрать все процессы;  

-a - выбрать все процессы, кроме фоновых;  

-d, (g) - выбрать все процессы, даже фоновые, кроме процессов сессий; 

-N - выбрать все процессы кроме указанных;  

-С - выбирать процессы по имени команды; 

-G - выбрать процессы по ID группы;  

-p, (p) - выбрать процессы PID;  

--ppid - выбрать процессы по PID родительского процесса;  

-s - выбрать процессы по ID сессии;  

-t, (t) - выбрать процессы по tty;  

-u, (U) - выбрать процессы пользователя.

5. `reboot`
6.  Пробросил порты в Virtual Box

![img.png](Screenshots/img56.png)

7. Для проверки, подключаюсь по ssh с указанием логина, IP-адреса и нового порта, ввожу `yes` для добавления отпечатка, а затем пароль для подключения

![img_1.png](Screenshots/img57.png)

**netstat** - команда для вывода списка открытых портов и соответствующих им адресов, таблиц маршрутизации и скрытых соединений. 

**Список ключей**: 

-t - Отображение текущего подключения в состоянии переноса нагрузки с процессора на сетевой адаптер при передаче данных ( "offload" ); 

-a - Отображение всех подключений и ожидающих портов; 

-n - Отображение адресов и номеров портов в числовом формате. 

Proto - Протокол, используемый сокетом. 

Recv-Q - Счётчик байт не скопированных программой пользователя из этого сокета. 

Send-Q - Счётчик байтов, не подтверждённых удалённым узлом. 

Local Address - Адрес и номер порта локального конца сокета. 

Если не указана опция --numeric (-n), адрес сокета преобразуется в каноническое имя узла (FQDN), и номер порта преобразуется в соответствующее имя службы. 

Foreign Address - Адрес и номер порта удалённого конца сокета.
Аналогично "Local Address" State - Состояние сокета.

0.0.0.0 - это немаршрутизируемый адрес IPv4, который используется в качестве адреса по умолчанию или адреса-заполнителя.

## Part 9. Установка и использование утилит top, htop

1. Запустил улититу `top`

![img58.png](Screenshots/img58.png)

* **uptime** - 33 min
* **authorized users** - 1 user
* **average load** - 0.00 %
* **total process** - 120 process
* **cpu load** - 0.0 us
* **memory load** - 168.8 mb used
* **pid process with most memory use** - 602 (`M` для сортировки по загрузке памяти)
* **pid process with most cpu use** - 602 (`P` для сортировки по загрузке памяти)

2. Запустил утилиту `htop`

![img59.png](Screenshots/img59.png)

* Сортировка по PID (`F6` и выбрать столбец для сортировки, или запускать `htop --sort-key` с нужным столбцом)

![img60.png](Screenshots/img60.png)

* Сортировка по PERCENT_CPU

![img61.png](Screenshots/img61.png)

* Сортировка по PERCENT_MEM

![img62.png](Screenshots/img62.png)

* Сортировка по TIME

![img63.png](Screenshots/img63.png)

* Фильтр для процесса sshd (`F4`, либо `/` и ввести название процесса)

![img64.png](Screenshots/img64.png)

* Поиск по процессу syslog (`F3` и ввести название процесса)

![img65.png](Screenshots/img65.png)

* Добавление вывода hostname, clock и uptime (`F2` и выбрать необходимые метрики, и их расположение)

![img66.png](Screenshots/img66.png)


## Part 10. Использование утилиты fdisk

### Запустил утилиту `fdisk -l`

![img67.png](Screenshots/img67.png)

* **Название жесткого диска** - /dev/sda
* **Размер** - 5 Gib
* **Количество секторов** - 10485760 sectors

![img68.png](Screenshots/img68.png)

* **Размер swap** - 0 B

## Part 11. Использование утилиты df

### Запустил команду `df`

![img69.png](Screenshots/img69.png)

**Раздел / (`df /`, `df -h /` - для понятного вывода):**

![img70.png](Screenshots/img70.png)

![img71.png](Screenshots/img71.png)

* **Размер раздела** - 3273108 bytes
* **Размер занятого пространства** - 2781424 bytes
* **Размер свободного пространства** - 305112 bytes
* **Процент использования** - 91%
* **Единицы измерения** - байты

### Запустил команду `df -Th`

![img72.png](Screenshots/img72.png)

**Раздел / (`-T` - для вывода типа системы):**

* **Размер раздела** - 3.2 G 
* **Размер занятого пространства** - 2.7 G
* **Размер свободного пространства** -  298 M
* **Процент использования** - 91 %
* **Тип системы** - ext 4

## Part 12. Использование утилиты du

* Запустил команду `du`

![img73.png](Screenshots/img73.png)

* Вывел размер папок в `/home` в байтах (`-b`)

![img74.png](Screenshots/img74.png)

* Вывел размер папок в `/var` в байтах

![img75.png](Screenshots/img75.png)

* Вывел размер папок в `/var/log` в байтах

![img76.png](Screenshots/img76.png)

* Вывел размер папок в `/home` в человекочитаемом виде (`-h`)

![img77.png](Screenshots/img77.png)

* Вывел размер папок в `/var` в человекочитаемом виде

![img78.png](Screenshots/img78.png)

* Вывел размер папок в `/var/log` в человекочитаемом виде

![img79.png](Screenshots/img79.png)

* Вывел размер всего содержимого в `/var/log` (`*`)

![img80.png](Screenshots/img80.png)


## Part 13. Установка и использование утилиты ncdu

1. Установил утилиту `ncdu`

![img81.png](Screenshots/img81.png)

2. Вывел размер папок в `/home` (`ncdu /home`)

![img82.png](Screenshots/img82.png)

3. Вывел размер папок в `/var` (`ncdu /var`)

![img83.png](Screenshots/img83.png)

4. Вывел размер папок в `/var/log` (`ncdu /var/log`)

![img84.png](Screenshots/img84.png)


## Part 14. Работа с системными журналами

1. Открыл логи `/var/log/dmesg` (содержит сообщения, полученные от ядра)

![img85.png](Screenshots/img85.png)

2. Открыл логи `/var/log/syslog` (содержит все системные сообщения)

![img86.png](Screenshots/img86.png)

3. Открыл логи `/var/log/auth.log` (содержит информацию об авторизации пользователей в системе)

   3. **Время последней успешной авторизации** - 17 августа, 12:38
   3. **Имя пользователя** - quickbes
   3. **Метод входа в систему** - LOGIN

![img87.png](Screenshots/img87.png)

4. Перезапустил службу `SSHd` через `systemctl restart` и проверил наличие этого факта в `/var/log/syslog`

![img88.png](Screenshots/img88.png)

![img89.png](Screenshots/img89.png)


## Part 15. Использование планировщика заданий CRON

1. Добавил запуск команды `uptime` через каждые 2 минуты (`/2` означает каждые 2 минуты, а не каждую вторую минуту часа) с помощью `crontab -e`, и перенаправил её вывод в .log файл

![img90.png](Screenshots/img90.png)

2. Проверил список задач CRON через `crontab -l`

![img91.png](Screenshots/img91.png)

3. Проверил выполнения команды `uptime` в созданном .log файле

![img92.png](Screenshots/img92.png)

4. Проверил исполнение службы `cron` в логах

![img93.png](Screenshots/img93.png)

5. Очистил список текущего пользователя задач через `crontab -r`

![img94.png](Screenshots/img94.png)