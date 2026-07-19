# Лабораторная работа. Развертывание коммутируемой сети с резервными каналами
Топология
![](cpt.png)

№ Часть 1:	Создание сети и настройка основных параметров устройства
№№ Шаг 1:	Создайте сеть согласно топологии.

![](cpt1.png)

##Шаг 2:	Выполните инициализацию и перезагрузку коммутаторов.

```
Switch#eras
Switch#erase start
Switch#erase startup-config 
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
Switch#reload
```
##Шаг 3:	Настройте базовые параметры каждого коммутатора.

a.	Отключите поиск DNS.
b.	Присвойте имена устройствам в соответствии с топологией.
c.	Назначьте class в качестве зашифрованного пароля доступа к привилегированному режиму.
d.	Назначьте cisco в качестве паролей консоли и VTY и активируйте вход для консоли и VTY каналов.
e.	Настройте logging synchronous для консольного канала.
f.	Настройте баннерное сообщение дня (MOTD) для предупреждения пользователей о запрете несанкционированного доступа.
g.	Задайте IP-адрес, указанный в таблице адресации для VLAN 1 на всех коммутаторах.
h.	Скопируйте текущую конфигурацию в файл загрузочной конфигурации.

###S1
```
Switch>enable
Switch#no ip domai
Switch#conf t
Switch(config)#no ip domain-lookup
Switch(config)#hostname S1
S1(config)#enable secret class
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#logging synchronous
S1(config-line)#banner motd
S1(config-line)#banner motd # Unauthorized access denied #
S1(config)#interf 
S1(config)#interface 
S1(config)#interface vlan 1
S1(config-if)#ip address 192.168.1.1 255.255.255.0
S1(config-if)#end
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#copy running
S1#copy running-config start
S1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
```
###S2
