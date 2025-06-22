# Router-on-a-stick
### Router R1 Configuration
```cisco
!
hostname R1
!
interface FastEthernet0/0
 no ip address
!
interface FastEthernet0/0.4
 encapsulation dot1Q 4
 ip address 192.168.1.5 255.255.255.248
!
interface FastEthernet0/0.5
 encapsulation dot1Q 5
 ip address 192.168.1.9 255.255.255.248
!
interface FastEthernet0/0.6
 encapsulation dot1Q 6
 ip address 192.168.1.13 255.255.255.248
!
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.17 255.255.255.240
!
! DHCP Pools
ip dhcp excluded-address 192.168.1.5 192.168.1.5
ip dhcp excluded-address 192.168.1.9 192.168.1.9
ip dhcp excluded-address 192.168.1.13 192.168.1.13
ip dhcp excluded-address 192.168.1.17 192.168.1.17

ip dhcp pool VLAN4_POOL
 network 192.168.1.0 255.255.255.248
 default-router 192.168.1.5
!
ip dhcp pool VLAN5_POOL
 network 192.168.1.8 255.255.255.248
 default-router 192.168.1.9
!
ip dhcp pool VLAN6_POOL
 network 192.168.1.12 255.255.255.248
 default-router 192.168.1.13
!
ip dhcp pool VLAN10_POOL
 network 192.168.1.16 255.255.255.240
 default-router 192.168.1.17
!
end
###Switch S1 Configuration
```cisco 
hostname S1
!
vlan 4
name Users_VLAN4
!
vlan 5
name Users_VLAN5
!
vlan 6
name Users_VLAN6
!
vlan 10
name Users_VLAN10
!
! Port connected to R1 (Trunk Port)
interface Ethernet3/0
 switchport mode trunk
!
! Ports for VLAN 4
interface Ethernet0/1
 switchport mode access
 switchport access vlan 4
!
interface Ethernet0/2
 switchport mode access
 switchport access vlan 4
!
! Ports for VLAN 5
interface Ethernet0/3
 switchport mode access
 switchport access vlan 5
!
interface Ethernet1/0
 switchport mode access
 switchport access vlan 5
!
! Ports for VLAN 6
interface Ethernet1/1
 switchport mode access
 switchport access vlan 6
!
interface Ethernet1/2
 switchport mode access
 switchport access vlan 6
!
! Ports for VLAN 10
interface Ethernet2/0
 switchport mode access
 switchport access vlan 10
!
interface Ethernet2/1
 switchport mode access
 switchport access vlan 10
!
interface Ethernet2/2
 switchport mode access
 switchport access vlan 10
!
interface Ethernet2/3
 switchport mode access
 switchport access vlan 10
!
end
