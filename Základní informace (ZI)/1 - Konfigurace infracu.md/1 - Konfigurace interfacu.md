# Konfigurace vybraného Interfacu na Switchi / Routeru

- otevřeme libovolné zařízení (Switch / Router)

- budeme postupovat následně : 

```
> en
> conf t
> int g0/0 (vybraný interface (v našem případě Gigabyte0/0 (zkr. G0/0)))
> ip address 192.168.0.5 255.255.255.0
> no shutdown (Pro zapnutí interfacu)
> Obdržíme message o zapnutí daného portu
> exit
```

