## Part 1. Installation of the OS
### Проверяем версию Ubuntu командой `cat /etc/issue`.

![Результат работы команды cat /etc/issue](/screenshots/Part_1.png)

## Part 2. Creating a user
### Создаем пользователя и сразу же добавляем его в группу `adm` через команду useradd.

![useradd](/screenshots/Part_2_1.png)

### Результат работы команды `cat /etc/passwd`.

![cat /etc/passwd](/screenshots/Part_2_2.png)

## Part 3. Setting up the OS network

- Меняем хостнейм через команду `hostnamectl`.

![hostname_change](/screenshots/Part_3_1.png)

- Меняем временную зону на `Asia/Yekaterinburg`.

![timezone_change](/screenshots/Part_3_2.png)

* Вывод сетевых интерфейсов.

![ifconfig](/screenshots/Part_3_3.png)
* Сетевой интерфейс `lo` (loopback) - виртуальное устройство которым управляет ОС. Loopback не привязан ни к каким физическим устройствам. Работая 100% от времени, а также эмулируя настоящий интерфейс, в большинстве случаев используется разработчиками для тестирования.

* Используем команду `dhclient -v` чтобы найти выданный DHCP'ом IP адрес `10.0.2.15`.
* `DHCP` - Dynamic Host Configuration Protocol - протокол выдачи клиентам сети IP адресов.

![dhclient -v](/screenshots/Part_3_4.png)

* Узнаем свой внешний IP адрес.

![external ip](/screenshots/Part_3_5.png)

* Узнаем свой внутренний IP адрес.

![internal ip](/screenshots/Part_3_6.png)

* Открываем необходимый файл через `nano` и редактируем.

![nano ipchange](/screenshots/Part_3_7.png)

![ipchange](/screenshots/Part_3_8.png)

* Отключаем автоматический DHCP, в addresses меняем внутренний айпи на необходимый, кроме того в nameservers указываем адреса необходимых нам DNS серверов.

* Применяем изменения и перезагружаем виртуальную машину.

![netchange_apply](/screenshots/Part_3_9.png)

![reboot](/screenshots/reboot.png)

* Проверяем сохранились ли значения.

![ipcheck](/screenshots/Part_3_10.png)

* Успешно! Пингуем `1.1.1.1` и `ya.ru`

![pingcheck](/screenshots/Part_3_11.png)

## Part 4. OS Update
* Используем `apt` для того чтобы обновить пакеты до последних доступных версий.

![aptupdate](/screenshots/Part_4_1.png)

* Проверяем чтобы система была точно обновлена.

![aptcheck](/screenshots/Part_4_2.png)

## Part 5. Using the sudo command
 
 * `Sudo` - *От аббревиатуры `S`substitute `U`ser, `DO` (подменить пользователя, исполнить)* - программа, позволяющая выполнять команды от имени иных пользователей. 
Чаще всего используется для того чтобы выполнять команды от имени `root`, иначе недоступные для исполнения иным учетным записям ради безопасности.

![sudo](/screenshots/Part_5.png)

### Полная последовательность действий:
1. Выдаем пользователю `user` группу `sudo` через команду `usermod`
2. Меняем пользователя на `user`
3. От его лица меняем хостнейм через `hostnamectl`
4. Проверяем успешную смену через `cat /etc/hostname`
5. ???
6. PROFIT

#  Part 6. Installing and configuring the time service

* Включаем синхронизацию времени через NTP, после чего сверяем время с локальным. Работает верно.

![ntpsync](/screenshots/Part_6.png)

# Part 7. Installing and using text editors

* Заранее дополнительно устанавливаем `vim` и `emacs`

![texteditor_install](/screenshots/Part_7_1.png)

### Nano
* Создаем файл с нужным названием через `nano`

![nano_filecreate](/screenshots/Part_7_2.png)

* Набираем необходимый текст, после чего используем комбинацию `CTRL + S` и `CTRL + X` чтобы сохранить изменения и выйти.

![nano_1](/screenshots/Part_7_3.png)

* Снова открываем уже существующий файл той же командой. 

![nano_filecreate](/screenshots/Part_7_2.png)

* Меняем текст на необходимый. Выходим без изменений через `CTRL + X`, нажав N на вопросе промта о сохранении данных.

![nano_2](/screenshots/Part_7_4.png)

* Находим необходимую строчку через комбинацию клавиш `CTRL + W`

![nano_3](/screenshots/Part_7_6.png)

* Для того чтобы заменить строку используем `CTRL + \`, после чего вводим содержимое для замены и содержимое на которое нужно его заменить.

![nano_4](/screenshots/Part_7_7.png)

![nano_5](/screenshots/Part_7_8.png)

![nano_6](/screenshots/Part_7_9.png)

### Vim

* Создаем файл с необходимым названием через `vim`

![vim_filecreate](/screenshots/Part_7_10.png)

* Нажимаем `i` чтобы войти в режим `INSERT`, вводим необходимое, нажимаем `ESC` чтобы войти обратно в командный режим и вводим :wq чтобы сохранить данные и сразу же выйти из редактора.

![vim_1](/screenshots/Part_7_11.png)

![vim_2](/screenshots/Part_7_12.png)

* Снова открываем редактор, вводим в командном режиме `dd`, после чего входим в режим `INSERT` и меняем данные на необходимое. После всех манипуляций вводим :q! чтобы выйти не сохраняя изменений.

![vim_3](/screenshots/Part_7_13.png)

* В очередной раз открываем редактор. В командном режиме нажимаем `/` и вводим необходимый текст для поиска. Работает даже с регулярками. Нажимаем `Enter`

![vim_3](/screenshots/Part_7_14.png)

* Чтобы подменить текст, в командном режиме используем:
`:%s/старое_слово/новое_слово/g`

![vim_4](/screenshots/Part_7_15.png)

![vim_4](/screenshots/Part_7_16.png)

### Emacs

* Создаем файл через Emacs

![Emacs_filecreate](/screenshots/Part_7_17.png)

* Набираем в редакторе необходимый текст. Для сохранения используем комбинацию клавиш `CTRL + X` + `S`, после чего нажимаем `Y` для подтверждения. Выходим через `CTRL + X + C`

![Emacs_1](/screenshots/Part_7_18.png)

* Снова открываем необходимый файл, меняем содержимое согласно заданию. Для того чтобы выйти не сохраняя изменений используем `CTRL + X + C`, после чего на все промты о сохранении отвечаем `n`, при необходимости дополнительно отвечаем `yes` на промт выхода

![Emacs_1](/screenshots/Part_7_19.png)

* Для того чтобы начать поиск, используем комбинацию клавиш `CTRL + S` + `ENTER`, после чего вводим необходимое слово и еще раз нажимаем `ENTER`

![Emacs_2](/screenshots/Part_7_20.png)

* Для того чтобы заменить строку:
1. Используем `ESC + X`
2. В появившемся промте пишем replace-string
3. Выбираем строку под замену и для замены.

![Emacs_3](/screenshots/Part_7_21.png)

![Emacs_4](/screenshots/Part_7_22.png)

![Emacs_5](/screenshots/Part_7_23.png)

![Emacs_6](/screenshots/Part_7_24.png)

## Part 8. Installing and basic setup of the SSHD service

* Устанавливаем необходимый пакет `openssh-server`

![openssh_install](/screenshots/Part_8_1.png)

* Включаем автозапуск необходимого демона через systemctl

![ssh_service_enable](/screenshots/Part_8_2.png)

* Редактируем конфигурационный файл `/etc/ssh/sshd_config`

![ssh_open_config](/screenshots/Part_8_3.png)

![shh_config_port_commented](/screenshots/Part_8_4.png)

* Разкомменчиваем строку с портом и меняем его на необходимый

![shh_config_port_changed](/screenshots/Part_8_5.png)

* Перезапускаем службу и смотрим статус чтобы проверить что порт успешно сменился.

![shh_reset](/screenshots/Part_8_6.png)

* Находим процесс через команду `ps aux | grep sshd`

* a - отображение всех процессов
* u - отображение процессов в удобном для пользователя формате
* x - отображение процессов, принадлежащих текущему пользователю

![process_List](/screenshots/Part_8_7.png)

* Ребутаем систему

![reboot](/screenshots/reboot.png)


* Вывод работы команды netstat -tan

![netstat](/screenshots/Part_8_9.png)

* Флаг -t - показывать соединения с протоколом TCP
* Флаг -а - показывает все соединения, как слушащие так и нет
* Флаг -n - использует для отображения нумерические адреса вместо хостнеймов

* Proto - Протокол

* Recv-Q - Счётчик байтов не скопированных программой пользователя из этого сокета.

* Send-Q - Счётчик байтов, не подтверждённых удалённым узлом.

* Local Address - Адрес и номер порта локального конца сокета.

* Foreign Address - Адрес и номер порта удалённого конца сокета.

* State - Состояние сокета.

* LISTEN - Сокет ожидает входящих подключений.

* SYN_SENT - Сокет, находящийся в режиме активной попытки установки подключения.

* 0.0.0.0 - это немаршрутизируемый адрес IPv4, который используется в качестве адреса по умолчанию или адреса-заполнителя.

## Part 9. Installing and using the top, htop utilities

### Устанавливаем необходимые утилиты

![htop_install](/screenshots/Part_9_1.png)


### Результат вывода программмы top

![top_output](/screenshots/Part_9_2.png)


* uptime: `2:15`
* number of authorised users: `1`
* average system load: `0.01`
* total number of processes: `120`
* cpu load: `1.4`
* memory load: `178.3 MB`
* pid of the process with the highest memory usage: `1`
* pid of the process taking the most CPU time: `10`


* Результат вывода команды htop

![htop_output](/screenshots/Part_9_3.png)

### Сортировка в htop производится путем нажатия клавиши F6 и дальнейшей выборке через контекстное меню

![htop_sort](/screenshots/Part_9_4.png)

### Сортировки по `PID, PERCENT_CPU, PERCENT_MEM, TIME`:

![htop_output](/screenshots/Part_9_5.png)
![htop_output](/screenshots/Part_9_6.png)
![htop_output](/screenshots/Part_9_7.png)
![htop_output](/screenshots/Part_9_8.png)

### Фильтрация по имени процесса `sshd`
* Работает через нажатие клавиши F4

![htop_output](/screenshots/Part_9_9.png)

### Нахождение процесса ответственного за syslog
* Используем поиск через нажатие клавиши `/` и дальнейшего поиска путем перебирания вариантов через `F3`. Как и Vim работает с регулярками! (должно, надеюсь)

![htop_panel](/screenshots/Part_9_10.png)

### Вывод hostname, clock и uptime на главную панель сверху
* Делается через меню на F2

![htop_panel](/screenshots/Part_9_11.png)
![htop_panel](/screenshots/Part_9_12.png)

## Part 10. Using the fdisk utility

### Результат работы команды `fdisk -l`

![fdisk_l](/screenshots/Part_10_1.png)

* Имя диска - `sda`
* Вместимость - `32212254720` байт (~30 гб)
* Кол-во секторов - `29351936`
* Swap-раздел - `0` байт (отсутствует)

## Part 11. Using the df utility

### Результат работы команды df

![df](/screenshots/Part_11_1.png)

* Статистика по рут-разделу (/dev/mapper/ubuntu--vg-ubuntu--lv или /dev/sda3)
* Размер раздела: `14339080` КБ
* Занятое место: `5246140` байт
* Свободное место: `8342760` байт
* Занято: `39%`

### Результат работы команды df -Th

![df_Th](/screenshots/Part_11_2.png)

* Размер раздела: `14` ГБ
* Использовано: `5` ГБ
* Свободно: `8` ГБ
* Занято: `39%`

## Part 12. Using the du utility

### Вывод размера папок `/home/` `/var/` `/var/log/` в человекочитаемом формате:

![du_human_1](/screenshots/Part_12_1.png)

### Вывод размеров содержимого `/var/log`:

![du_human_2](/screenshots/Part_12_2.png)

## Part 13. Installing and using the ncdu utility

### Устанавливаем утилиту `ncdu`
![ncdu_install](/screenshots/Part_13_1.png)

### Результат работы утилиты для папок `/home/`, `/var/` и `/var/log/`

![ncdu_home](/screenshots/Part_13_5.png)

![ncdu_var](/screenshots/Part_13_6.png)

![ncdu_var_log](/screenshots/Part_13_7.png)

---

![ncdu_home](/screenshots/Part_13_2.png)

![ncdu_var](/screenshots/Part_13_3.png)

![ncdu_var_log](/screenshots/Part_13_4.png)

## Part 14. Working with system logs

### Открываем логи:

![logs_1](/screenshots/Part_14_1.png)
![logs_2](/screenshots/Part_14_2.png)
![logs_3](/screenshots/Part_14_3.png)
![logs_4](/screenshots/Part_14_4.png)
![logs_5](/screenshots/Part_14_5.png)
![logs_6](/screenshots/Part_14_6.png)


### Ищем время входа последнего пользователя:

![logs_7](/screenshots/Part_14_7.png)
![logs_7](/screenshots/Part_14_8.png)


* Последний заход: `18 августа в 13:14:22`
* Имя пользователя: `anon`
* Метод: `tty1`

![logs_8](/screenshots/Part_14_9.png)

### Перезапускаем `sshd`:
![logs_9](/screenshots/Part_14_10.png)

### Ищем логи перезапуска службы:
![logs_10](/screenshots/Part_14_11.png)

## Part 15. Using the CRON job scheduler

### Запускаем `crontab`, в случае первого запуска необходимо будет выбрать необходимый текстовый редактор


![cron_1](/screenshots/Part_15_1.png)

### В получившемся окне создаем необходимую задачу с периодом в две минуты:
![cron_2](/screenshots/Part_15_2.png)

### В логах находим исполнение команды uptime раз в две минуты

![cron_3](/screenshots/Part_15_3.png)

### Список задач для cron

![cron_4](/screenshots/Part_15_4.png)

### Очищаем список задач и проверяем чтобы он был пуст

![cron_4](/screenshots/Part_15_5.png)