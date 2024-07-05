## Part 1. Установка ОС

- Установим Ubuntu 20.04 Server LTS без графического интерфейса. Далее выполним команду `cat /etc/issue.net`, чтобы узнать версию Ubuntu.<br>
![./screenshots/1.1.png](./screenshots/1.1.png)<br>

## Part 2. Создание пользователя

- Создадим нового пользователя и добавим в группу adm, используя команду `sudo useradd -g adm new_user`.<br>
![./screenshots/2.1.png](./screenshots/2.1.png)<br>

- Вывод команды `cat /etc/passwd`<br>
![./screenshots/2.2.png](./screenshots/2.2.png)<br>

## Part 3. Настройка сети ОС

- Сменим название машины на user-1: `sudo nano /etc/hostname`.<br>
![./screenshots/3.1.png](./screenshots/3.1.png)<br>
Сделаем `reboot` и проверим<br>
![./screenshots/3.2.png](./screenshots/3.2.png)<br>

- Установка временной зоны при помощи команды `dpkg-reconfigure tzdata`.<br>
![./screenshots/3.3.png](./screenshots/3.3.png)<br>

- Вывод названий сетевых интерфейсов: `ip addr show`.<br>
lo (local loopback) используется для того, чтобы компьютер мог обращаться к самому себе и имеет по умолчанию ip-адрес 127.0.0.1 на всех компьютерах.<br>
![./screenshots/3.4.png](./screenshots/3.4.png)<br>

- Получение ip-адреса устройства от DHCP сервера: `hostname -I`.<br>
DHCP - Dynamic Host Configuration Protocol - протокол, использующийся для автоматического выставления различной конфигурации, в том числе IP-адресов.<br>
![./screenshots/3.5.png](./screenshots/3.5.png)<br>

- Внешний ip-адрес шлюза (ip): `wget -O - -q icanhazip.com`.<br>
![./screenshots/3.6.png](./screenshots/3.6.png)<br>

- Внутренний IP-адрес шлюза, он же ip-адрес по умолчанию (gw): `ip route show | grep default | awk '{print $3}'`.<br>
![./screenshots/3.7.png](./screenshots/3.7.png)<br>

- Установка статичных настроек ip, gw, dns используя `sudo vim /etc/netplan/00-installer-config.yaml`.<br>
![./screenshots/3.8.png](./screenshots/3.8.png)<br>

- Пингование удаленных хостов 1.1.1.1 и ya.ru прошло успешно.<br>
![./screenshots/3.9.png](./screenshots/3.9.png)<br>
![./screenshots/3.10.png](./screenshots/3.10.png)<br>

## Part 4. Обновление ОС

- Воспользуемся двумя командами. Команда `apt update` обновляет индекс пакетов в системе Linux или списки пакетов. Команда `apt upgrade` обновляет пакеты программного обеспечения до последних версий.<br>

Проверим<br>
![./screenshots/4.1.png](./screenshots/4.1.png)<br>
![./screenshots/4.2.png](./screenshots/4.2.png)<br>

## Part 5. Использование команды **sudo**

- `sudo` - (substitute user and do) позволяет строго определенным пользователям выполнять указанные команды с административными привилегиями.<br>
- Смена hostname от имени пользователя, созданного в пункте Part2.<br>
![./screenshots/5.1.png](./screenshots/5.1.png)<br>

## Part 6. Установка и настройка службы времени

- Для синхронизации времени используем команду `sudo timedatectl set-ntp 1`. Для отключения вместо 1 ставим 0.<br>
Вывод команды `timedatectl show`, показывающей время часового пояса.<br>
![./screenshots/6.1.png](./screenshots/6.1.png)<br>

## Part 7. Установка и использование текстовых редакторов 

- Команды для установки текстовых редакторов VIM, NANO и JOE.<br>
`sudo apt install vim`<br>
`sudo apt install nano`<br>
`sudo apt install joe`<br>
- VIM: для выхода с сохранением изменений нажал ESC и набрал команду `:wq test_VIM.txt`.<br>
![./screenshots/7.1.png](./screenshots/7.1.png)<br>
- NANO: для выхода с сохранением изменений нажал Ctrl + O, ввёл test_NANO.txt, нажал Ctrl + X.<br>
![./screenshots/7.2.png](./screenshots/7.2.png)<br>
- JOE: для выхода с сохранением изменений нажал Ctrl + K + X, ввёл test_JOE.txt.<br>
![./screenshots/7.3.png](./screenshots/7.3.png)<br>

- VIM: для выхода без сохранения изменений нажал ESC и набрал команду `:q!`.<br>
![./screenshots/7.4.png](./screenshots/7.4.png)<br>
- NANO: для выхода без сохранения изменений нажал Ctrl + X и N.<br>
![./screenshots/7.5.png](./screenshots/7.5.png)<br>
- JOE: для выхода без сохранения изменений нажал Ctrl + C и y.<br>
![./screenshots/7.6.png](./screenshots/7.6.png)<br>

- VIM: поиск: `/слово(необезательно) для поиска`<br>
![./screenshots/7.7.png](./screenshots/7.7.png)<br>
- VIM: замена: `:s/что заменить/на что`<br>
![./screenshots/7.8.png](./screenshots/7.8.png)<br>

- NANO: поиск: `Ctrl + W`<br>
![./screenshots/7.9.png](./screenshots/7.9.png)<br>
- NANO: замена: `Ctrl + \, [что заменить] [на что], Y`<br>
![./screenshots/7.10.png](./screenshots/7.10.png)<br>

- JOE: поиск: `Ctrl + K, F, что найти, I`<br>
![./screenshots/7.11.png](./screenshots/7.11.png)<br>
- JOE: замена: `Ctrl + K, F, что заменить, R, на что, Y`<br>
![./screenshots/7.12.png](./screenshots/7.12.png)<br>

## Part 8. Установка и базовая настройка сервиса **SSHD**

- Установил службу SSHd.<br>
`sudo apt-get install ssh`<br>
`sudo apt install openssh-server`<br>
![./screenshots/8.1.png](./screenshots/8.1.png)<br>

- Добавил автостарт службы при загрузке системы.<br>
`sudo systemctl enable ssh`<br>
`systemctl status ssh`<br>
![./screenshots/8.2.png](./screenshots/8.2.png)<br>

- Перенастроил службу SSHd на порт 2022.<br>
Ввёл команду: `sudo vim /etc/ssh/sshd_config`, чтобы отредактировать файл конфигурации службы SSHd, нашёл строку, содержащую порт SSH и изменил значение порта на 2022.<br>
![./screenshots/8.3.png](./screenshots/8.3.png)<br>
Перезапустил службу SSHd для применения новых настроек: `sudo systemctl restart sshd`.<br>

- Показать наличие процесса sshd можно используя команду `ps -C sshd`.<br>
![./screenshots/8.4.png](./screenshots/8.4.png)<br>
`ps` - команда для получения информации о текущих процессах.<br>
`-C` - ключ для фильтрации вывода процессов по имени команды (названию процесса). В данном случае, мы указываем sshd как имя команды для фильтрации.<br>

- Перезагрузил систему, используя команду `sudo reboot`.<br>

- Вывод команды `netstat -tan`.<br>
![./screenshots/8.5.png](./screenshots/8.5.png)<br>
Ключ `-t` или `--tcp` отображает только TCP-соединения в выводе netstat.<br>
Ключ `-a` или `--all` отображает все активные подключения TCP, включая слушающие порты.<br>
Ключ `-n` или `--numeric` выводит активные подключения TCP, отображая адреса и номера портов в числовом формате, а не в виде FQDN (Fully Qualified Domain Name) и имен сервисов.<br>
Proto: Указывает на название протокола, является ли это TCP или UDP.<br>
Recv-Q: Очередь получения, отображающая количество непрочитанных байтов, ожидающих чтения.<br>
Send-Q: Очередь отправки, отображающая количество байтов, ожидающих отправки.<br>
Local Address: Адрес локального компьютера и используемый номер порта для данного соединения.<br>
Foreign Address: Адрес и номер удаленного компьютера, к которому подключен данный сокет.<br>
State: Состояние сокета, показывающее, находится ли соединение в активном, ожидающем, закрытом или другом состоянии.<br>
Значение в столбце Local Address равно 0.0.0.0, это означает, что прослушивается IP-адрес на локальной машине для указанного порта.<br>

## Part 9. Установка и использование утилит **top**, **htop**

- Установил и запустил утилиту top<br>
uptime - 14;<br>
количество авторизованных пользователей - 1;<br>
общую загрузку системы - 0.00, 0.01, 0.03;<br>
общее количество процессов - 96;<br>
загрузку cpu - 0.3%;<br>
загрузку памяти - 159.7/1971.4;<br>
pid процесса занимающего больше всего памяти - 1207, команда: `top -o %MEM`;<br>
pid процесса, занимающего больше всего процессорного времени - 638, команда: `top -o %CPU`;<br>

- htop сортировка по PID<br>
![./screenshots/9.1.png](./screenshots/9.1.png)<br>
- htop сортировка по PERCENT_CPU<br>
![./screenshots/9.2.png](./screenshots/9.2.png)<br>
- htop сортировка по PERCENT_MEM<br>
![./screenshots/9.3.png](./screenshots/9.3.png)<br>
- htop сортировка по TIME<br>
![./screenshots/9.4.png](./screenshots/9.4.png)<br>
- скрин с выводом команды htop отфильтрованному для процесса sshd<br>
![./screenshots/9.5.png](./screenshots/9.5.png)<br>
- скрин с выводом команды htop с процессом syslog, найденным, используя поиск<br>
![./screenshots/9.6.png](./screenshots/9.6.png)<br>
- скрин с выводом команды htop с добавленным выводом hostname, clock и uptime<br>
![./screenshots/9.7.png](./screenshots/9.7.png)<br>

## Part 10. Использование утилиты **fdisk**

- Запуск команды `sudo fdisk -l`.<br>
![./screenshots/10.1.png](./screenshots/10.1.png)<br>
название жесткого диска - vbox harddisk;<br>
размер - 25GiB;<br>
количество секторов - 52428800.<br>

- Запуск команды `sudo swapon --show`.<br>
![./screenshots/10.2.png](./screenshots/10.2.png)<br>
размер swap - 2G.<br>

## Part 11. Использование утилиты **df** 

- Запустил команду `df`.<br>
![./screenshots/11.1.png](./screenshots/11.1.png)<br>
размер раздела - 11758760;<br>
размер занятого пространства - 4775812;<br>
размер свободного пространства - 6363840;<br>
процент использования - 43;<br>
Определить и написать в отчёт единицу измерения в выводе - KB.<br>

- Запустил команду `df -Th`.<br>
![./screenshots/11.2.png](./screenshots/11.2.png)<br>
размер раздела - 12G;<br>
размер занятого пространства - 4.6G;<br>
размер свободного пространства - 6.1G;<br>
процент использования  - 43;<br>
Тип файловой системы для раздела - ext4.<br>

## Part 12. Использование утилиты **du**

- Запустил команду `du`.<br>
![./screenshots/12.1.png](./screenshots/12.1.png)<br>
q
- Размер папок /home, /var, /var/log (в байтах), команда: `sudo du -s /var/log /home /var`<br>
![./screenshots/12.2.png](./screenshots/12.2.png)<br>

- Размер папок /home, /var, /var/log (в человекочитаемом виде), команда: `sudo du -sh /var/log /home /var`<br>
![./screenshots/12.3.png](./screenshots/12.3.png)<br>

- Размер всего содержимого в /var/log, команда: `sudo du -sh /var/log/*`<br>
![./screenshots/12.4.png](./screenshots/12.4.png)<br>

## Part 13. Установка и использование утилиты **ncdu**

- Установил утилиту ncdu<br>.
`sudo apt-get install ncdu`<br>
![./screenshots/13.1.png](./screenshots/13.1.png)<br>

- Размеры папок /home, /var, /var/log.<br>
![./screenshots/13.2.png](./screenshots/13.2.png)<br>
![./screenshots/13.3.png](./screenshots/13.3.png)<br>
![./screenshots/13.4.png](./screenshots/13.4.png)<br>

## Part 14. Работа с системными журналами

- Команды для открытия:<br>
`sudo vim /var/log/dmesg`<br>     
`sudo vim /var/log/syslog`<br>          
`sudo vim /var/log/auth.log`<br>

- Время последней успешной авторизации, имя пользователя и метод входа в систему:<br>
`(15:07:44; ehtelfos by LOGIN)`<br>

- Перезапуск службы SSHd.<br>
`sudo systemctl restart ssh`<br>

- Сообщениее о рестарте службы.<br>
![./screenshots/14.1.png](./screenshots/14.1.png)<br>

## Part 15. Использование планировщика заданий **CRON**

- Используя планировщик заданий, запустил команду uptime через каждые 2 минуты.<br>
![./screenshots/15.1.png](./screenshots/15.1.png)<br>

- Строчки в системном журнале о выполнении.<br>
![./screenshots/15.2.png](./screenshots/15.2.png)<br>

- Список текущих заданий для CRON<br>
![./screenshots/15.3.png](./screenshots/15.3.png)<br>

- Удалил все задания из планировщика заданий, скрин со списком текущих заданий для CRON.<br>
![./screenshots/15.4.png](./screenshots/15.4.png)<br>
