# Routing sítí

- otevřeme libovolný router a budeme postupovat následovně

## Příkladový formát

```> ip route <CILOVA ADRESA> <MASKA> <NEXT_HOP>
```

## Pro routing mezi připojenými switchmi k sobě použijeme

```> ip route 0.0.0.0 0.0.0.0 s0/3/0 (= int. pro příklad, interface připojený a vedený k danému routeru / routerům)
```

## Příkladový formát 3 sítí

### Máme 3 sítě, každá z nich má svojí adresu, 2 routery máme připojené k sobě, postupujeme následovně :

`Jedna síť má adresu 10.10.10.0 255.255.255.0 a je připojena na náš router (R1) v int. G0/2, pro náš router použijime tyto příklady`

- Router R1 je spojen seriovým kabelem na portu s0/3/0 k portu s0/3/0 na routeru R2

- v tomto případě jsou již infracy nastaveny dříve
```
> en
> conf t
> ip route 0.0.0.0 0.0.0.0 s0/3/0
```

`V druhém routeru máme nastavenou adresu síťě na portu g0/2 následovně : 30.30.30.0 255.255.255.0`

- dopíšeme pouze jeden příkaz

```> ip route 30.30.30.0 255.255.255.0 s0/3/0```

- ve finále celý postup vypadá takto : 

```
> en
> conf t
> ip route 0.0.0.0 0.0.0.0 s0/3/0
> ip route 30.30.30.0 255.255.255.0 s0/3/0
```



#### PROČ? Jeho cesta je vedena přes s0/3/0, kde máme již R2.

`Konfigurace z R2, budeme routovat naší adresu sítě (10.10.10.0 255.255.255.0) routeru R2, aby zjistil cestu a nevracel se u R1`

- může to znít komplikovaně, ale komplikované to není

- ve finále celý postup z R2 vypadá následovně : 

```
> en
> conf t
> ip route 0.0.0.0 0.0.0.0 s0/3/0
> ip route 10.10.10.0 255.255.255.0 s0/3/0
```

#### Proč IP adresa síťě končí na .0? Protože zadáváme celou síť a né konkrétni přiřazenou adresu končící (v našem případě) 1-254.