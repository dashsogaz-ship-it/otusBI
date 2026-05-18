# Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах

##Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
###Шаг 2. Настройте коммутатор.
```
Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#line vty 0 4
S1(config-line)#password cisco
S1(config-line)#login
S1(config)#line cons 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config)#enable secret class
S1(config-line)#
S1(config-line)#exit
S1(config-if)#sdm prefer dual-ipv4-and-ipv6 default
Changes to the running SDM preferences have been stored, but cannot take effect until the next reload.
Use 'show sdm prefer' to see what SDM preference is currently active.
S1(config)#end
S1#
%SYS-5-CONFIG_I: Configured from console by console

 S1#reload
S1(config)#interface v1
S1(config)#ipv6 unicast-routing 
S1(config)#interf v 1
S1(config-if)#ipv6 address 2001:db8:acad:1::b/64
S1(config-if)#ipv6 address fe80::B link-local
S1(config-if)#no shutdown
 ```
###Шаг 1. Настройте маршрутизатор.

```
Router(config)#hostname R1
R1(config)#line vty 0 4
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#line cons 0
R1(config-line)#exit
R1(config)#line cons 0
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#enable secret class
R1(config)#
```



