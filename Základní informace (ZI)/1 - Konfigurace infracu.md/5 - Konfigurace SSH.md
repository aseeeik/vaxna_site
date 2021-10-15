# Konfigurace SSH protokolu na Switchi / Routeru

- otevřeme libovolný switch nebo router

- budeme postupovat následovně :

#### Prvně nakonfigurujeme Vlan1
```> en
> conf t
> int vlan1
> ip address 192.168.0.50 255.255.255.0
> no shutdown
> end
```

#### Poté se přesuneme na konfiguraci protokolu SSH

```> en
> hostname <JMENO>
> ip domain-name CISCO
> username <JMENO> password <HESLO>
> crypto key generate rsa
> 512 (nebo 1024)
> ip ssh ver 2
> line vty 0 5 (max = 15)
> transport input ssh
> login local
> logging synchronous
> exit
> service password-encryption
```