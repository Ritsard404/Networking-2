# Networking-2

Configuration Scripts

			Switch 1 Configuration

S1(config)#hostname S1
S1(config)#vlan 10
S1(config-vlan)#name IT
S1(config-vlan)#vlan 20
S1(config-vlan)#name HR
S1(config-vlan)#int range fa0/3-4
S1(config-if-range)#switchport mode access
S1(config-if-range)#switchport access vlan 10
S1(config-if-range)#int range fa0/4-5
S1(config-if-range)#switchport mode access
S1(config-if-range)#switchport access vlan 20
S1(config-if-range)#int range fa0/2-3
S1(config-if-range)#switchport mode access
S1(config-if-range)#switchport access vlan 10
S1(config-if-range)#int fa0/1
S1(config-if)#switchport trunk allowed vlan 10,20
S1(config-if)#swtichport mode trunk

S1(config)#service password-encryption
S1(config)#line con 0
S1(config-line)#password quirante
S1(config-line)#login
S1(config-line)#exit
S1(config)#enable secret quirante
S1(config)#line vty 0 4
S1(config-line)#password quirante
S1(config-line)#login
S1(config-line)#exit

	Router 1 Configuration
hostname R1
R1(config)#int fa0/0.10
R1(config-subif)#encapsulation dot1q 10
R1(config-subif)#ip add 192.168.0.1 255.255.255.0
R1(config-subif)#int fa0/0.20
R1(config-subif)#encapsulation dot1q 20
R1(config-subif)#ip add 192.168.5.1 255.255.255.0

R1(config)#ip access-list standard IT
R1(config-std-nacl)#permit 192.168.4.0 0.0.0.255
R1(config-std-nacl)#exit
R1(config)#ip access-list standard HR
R1(config-std-nacl)#permit 192.168.3.0 0.0.0.255

R1(config)#int fa0/0.10
R1(config-subif)#ip access-group IT out
R1(config-subif)#
R1(config-subif)#int fa0/0.20
R1(config-subif)#ip access-group HR out
R1(config-subif)#exit
R1(config)#

R1(config)#router rip
R1(config-router)#version 2
R1(config-router)#network 192.168.0.0
R1(config-router)#network 192.168.1.0
R1(config-router)#network 192.168.2.0
R1(config-router)#network 192.168.3.0
R1(config-router)#network 192.168.4.0
R1(config-router)#network 192.168.5.0


R1(config)#service password-encryption
R1(config)#line con 0
R1(config-line)#password quirante
R1(config-line)#login
R1(config-line)#exit
R1(config)#enable secret quirante
R1(config)#line vty 0 4
R1(config-line)#password quirante
R1(config-line)#login
R1(config-line)#exit

		Router 2 Configuration
R2(config)#int fa0/0
R2(config-if)#ip add 192.168.3.1 255.255.255.0
R2(config)#int se0/0/0
R2(config-if)#ip add 192.168.1.2 255.255.255.0
R2(config-if)#int se0/0/1
R2(config-if)#ip add 192.168.2.1 255.255.255.0

R2(config)#int fa0/0
R2(config-if)#ip access-group HR out
R2(config-if)#int se0/0/0

R2(config)#ip access-list standard HR
R2(config-std-nacl)#permit 192.168.5.0 0.0.0.255
R2(config-std-nacl)#do wr

R2(config)#int fa0/0
R2(config-if)#ip access-group HR out
R2(config-if)#int se0/0/0

R2(config)#router rip 
R2(config-router)#version 2
R2(config-router)#network 192.168.0.0
R2(config-router)#network 192.168.1.0
R2(config-router)#network 192.168.2.0
R2(config-router)#network 192.168.3.0
R2(config-router)#network 192.168.4.0
R2(config-router)#network 192.168.5.0

R2(config)#service password-encryption
R2(config)#line con 0
R2(config-line)#password quirante
R2(config-line)#login
R2(config-line)#exit
R2(config)#enable secret quirante
R2(config)#line vty 0 4
R2(config-line)#password quirante
R2(config-line)#login
R2(config-line)#exit
R2(config)#do wr

		Router 3 Configuration
R3(config)#int fa0/0
R3(config-if)#ip add 192.168.4.1 255.255.255.0
R3(config-if)#no sh

R3(config)#ip access-list standard IT
R3(config-std-nacl)#permit 192.168.0.0 0.0.0.255
R3(config-std-nacl)#exit

R2(config)#ip access-list standard IT
R2(config-std-nacl)#permit 192.168.0.0 0.0.0.255
R2(config-std-nacl)#do wr

R2(config-std-nacl)#int fa0/0
R2(config-if)#ip access-group IT out

R3(config)#int se0/0/1
R3(config-if)#ip add 192.168.2.2 255.255.255.0
R3(config-if)#no sh

R3(config)#router rip
R3(config-router)#version 2
R3(config-router)#network 192.168.0.0
R3(config-router)#network 192.168.1.0
R3(config-router)#network 192.168.2.0
R3(config-router)#network 192.168.3.0
R3(config-router)#network 192.168.4.0
R3(config-router)#network 192.168.5.0

R3(config)#service password-encryption
R3(config)#line con 0
R3(config-line)#password quirante
R3(config-line)#login
R3(config-line)#exit
R3(config)#enable secret quirante
R3(config)#line vty 0 4
R3(config-line)#password quirante 
R3(config-line)#login
R3(config-line)#exit
R3(config)#do wr
