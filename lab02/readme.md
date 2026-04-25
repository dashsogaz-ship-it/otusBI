№ Лабораторная работа. Просмотр таблицы MAC-адресов коммутатора 


№№ Часть 1. Создание и настройка сети

#Шаг 1. Подключите сеть в соответствии с топологией.

![](1CPT.png)




#Шаг 3. Выполните инициализацию и перезагрузку коммутаторов.
```
'''S1#erase startup-config 
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
S1#reload
System configuration has been modified. Save? [yes/no]:no
Proceed with reload? [confirm]
C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)
Cisco WS-C2960-24TT (RC32300) processor (revision C0) with 21039K bytes of memory.
2960-24TT starting...
```
#Шаг 4. Настройте базовые параметры каждого коммутатора.
S1
```
Switch>enable
switch#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#int v 1
S1(config-if)#ip address 192.168.1.11 255.255.255.0
S1(config-if)#no shutdown

S1(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up
S1(config)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login
S1(config)#enable secret class
S1(config)#
```
S2
```
Switch>enable
Switch#conf
Switch#configure term
Switch#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S2
S2(config)#int v 1
S2(config-if)#ip addr
S2(config-if)#ip address 192.168.1.12 255.255.255.0
S2(config-if)#
S2(config-if)#no shutdown
S2(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up
S2(config)#line vty 0 15
S2(config-line)#password cisco
S2(config-line)#login
S2(config)#enable secret class
S2(config)#
```
