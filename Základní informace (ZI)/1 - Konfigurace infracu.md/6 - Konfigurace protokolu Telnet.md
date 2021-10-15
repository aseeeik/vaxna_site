# Konfigurace Telnet protokolu na Routeru nebo Switchi

- otevřeme libovolný router nebo switch

- budeme postupovat následovně :

#### Prvně nakonfigurujeme Vlan1
```
> en
> conf t
> int vlan1
> ip address 192.168.0.100 255.255.255.0
> no shutdown
> end
```

#### Poté se přesuneme na konfiguraci protokolu TELNET (= NEZABEZPECENY PROTOKOL, JE MOZNE VYSTOPOVAT HESLO)

```
> en
> conf t
> hostname <JMENO>
> line vty 0 5 (max = 15)
> password <HESLO>
> login
> exit
```