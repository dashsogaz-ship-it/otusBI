#Лабораторная работа - Внедрение маршрутизации между виртуальными локальными сетями 

#Часть 1. Создание сети и настройка основных параметров устройства

№№ Шаг 1. Создайте сеть согласно топологии.
![](cpt3.png)


![](cpt1.png)


##Шаг 1. Создайте сеть согласно топологии.

a.	Подключитесь к маршрутизатору с помощью консоли и активируйте привилегированный режим EXEC.
Откройте окно конфигурации
b.	Войдите в режим конфигурации.
c.	Назначьте маршрутизатору имя устройства.
d.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
e.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
f.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
g.	Установите cisco в качестве пароля виртуального терминала и активируйте вход.
h.	Зашифруйте открытые пароли.
i.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
j.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
k.	Настройте на маршрутизаторе время.


```
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#no ip domain-loo
R1(config)#no ip domain-lookup 
R1(config)#enable secret class
R1(config)#line cons 0
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#line vty 0 4
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#service password-en
R1(config)#service password-encryption 
R1(config)#banner motd #Attention! Unauthorized access prohibited! #
R1(config)#
R1#copy run
R1#copy running-config start
R1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#clock ?
  set  Set the time and date
R1#clock set 16:24:00 
R1#clock set 16:24:00 ?
  <1-31>  Day of the month
  MONTH   Month of the year
R1#clock set 16:24:00 Jun 21 2026
R1#show clo
R1#show clock 
16:24:6.963 UTC Sun Jun 21 2026
```
##Шаг 3. Настройте базовые параметры каждого коммутатора.

a.	Присвойте коммутатору имя устройства.
b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
e.	Установите cisco в качестве пароля виртуального терминала и активируйте вход.
f.	Зашифруйте открытые пароли.
g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
h.	Настройте на коммутаторах время.
i.	Сохранение текущей конфигурации в качестве начальной.

###S1
```
Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#no ip domain-lo
S1(config)#no ip domain-lookup 
S1(config)#enable secret class
S1(config)#line cons 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#line vty 0 4
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#service password-encry
S1(config)#service password-encryption 
S1(config)#banne motd #Attention! Unauthorized access prohibited #
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console
S1#clock set 16:35:00 Jun 21 2026
S1#copy runni
S1#copy running-config star
S1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
S1#
```
###S2

```
Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S2
S2(config)#enable secret class
S2(config)#no ip domain-loo
S2(config)#no ip domain-lookup 
S2(config)#line cons 0
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
S2(config)#line vty 0 4
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
S2(config)#service password-enc
S2(config)#service password-encryption 
S2(config)#banner motd # Attention! Unauthorized access prohibited! #
S2(config)#end
S2#
%SYS-5-CONFIG_I: Configured from console by console

S2#clock set 16:41:00 jun 21 2026
S2#copy run
S2#copy running-config sta
S2#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
```
##Шаг 4. Настройте узлы ПК.

![](cpt2.png)

#Часть 2. Создание сетей VLAN и назначение портов коммутатора

##Шаг 1. Создайте сети VLAN на коммутаторах.
a.	Создайте и назовите необходимые VLAN на каждом коммутаторе из таблицы выше.
Откройте окно конфигурации
b.	Настройте интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации. 
c.	Назначьте все неиспользуемые порты коммутатора VLAN Parking_Lot, настройте их для статического режима доступа и административно деактивируйте их.
Примечание. Команда interface range полезна для выполнения этой задачи с минимальным количеством команд.
##
S1

###a.
```
S1(config)#vlan 10
S1(config-vlan)#exit
S1(config)#vlan 20
S1(config-vlan)#name sales
S1(config-vlan)#exit
S1(config)#vlan 30
S1(config-vlan)#name operations
S1(config-vlan)#exit
S1(config)#vlan 999
S1(config-vlan)#name parking_lot
S1(config-vlan)#exit
S1(config)#vlan 1000
S1(config-vlan)#exit
S1(config)#int v  10
S1(config-if)#
%LINK-5-CHANGED: Interface Vlan10, changed state to up
```
###b.
```
S1(config-if)#int v  10
S1(config-if)#ip add 192.168.10.11 255.255.255.0
S1(config-if)#no shut
S1(config)#ip default-gateway 192.168.10.1
```
###c.
```
S1(config)#int r f0/2-4, f0/7-24, g0/1-2
S1(config-if-range)#sw m a
S1(config-if-range)#sw a v 999
S1(config-if-range)#shut
%LINK-5-CHANGED: Interface FastEthernet0/2, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/7, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/8, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/9, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/10, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/11, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/12, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/13, changed state to administratively down
LINK-5-CHANGED: Interface FastEthernet0/14, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/15, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/16, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/17, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/18, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/19, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/20, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/21, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/22, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/23, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/24, changed state to administratively down
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to administratively down

```

##S2

a.
```
S2>enable
Password: 
S2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
S2(config)#vlan 10
S2(config-vlan)#^Z
S2#
%SYS-5-CONFIG_I: Configured from console by console

S2#
S2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
S2(config)#vlan 20
S2(config-vlan)#vlan 30
S2(config-vlan)#name operations
S2(config-vlan)#vlan 999
S2(config-vlan)#name Parking_Lot
S2(config-vlan)#vlan 1000
S2(config-vlan)#do sh v
% Ambiguous command: "sh v"
S2(config-vlan)#exit
```
b.
```
S2(config)#int v 10
S2(config-if)#
%LINK-5-CHANGED: Interface Vlan10, changed state to up

S2(config-if)#ip address 192.168.10.12 255.255.255.0
S2(config-if)#no shut
S2(config-if)#exit
S2(config)#ip deaf
S2(config)#ip defau
S2(config)#ip default-gateway 192.168.10.1
S2(config)#exit
```
c.
```
S2(config)#int range f0/2-17, f0/19-24, g0/1-2
S2(config-if-range)#switch
S2(config-if-range)#switchport mode access
S2(config-if-range)#sw access vlan 999
S2(config-if-range)#shut
```
## Шаг 2. Назначьте сети VLAN соответствующим интерфейсам коммутатора.
a.	Назначьте используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настройте их для режима статического доступа.
b.	Убедитесь, что VLAN назначены на правильные интерфейсы.

a.
```
S2(config)#int f0/18
S2(config-if)#sw mode access
S2(config-if)#sw a v 30
S2(config-if)#exit

S1(config)#int fastEthernet 0/6
S1(config-if)#switch
S1(config-if)#switchport mod
S1(config-if)#switchport mode acc
S1(config-if)#switchport mode access 
S1(config-if)#sw access vl 20
```


b.![](cpt4.png)


