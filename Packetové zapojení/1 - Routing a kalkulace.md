# Příprava na sítě


![Schéma zapojení](https://cdn.discordapp.com/attachments/893822214854574090/893823577957224488/bcg.png)

> *- vložíme dva routery označené jako **2911**, ke kterým je potřeba přidat modul **HWIC-2T**, který přidáme po rozkliknutí routeru, v záložce **Physical,** prvně musíme vypnout proud switche!*
> *- poté vložíme switche 2960 a následně PC*

*`- k zapojení mezi R1 & R2 využíváme Serial DTE, který je 9 v pořadí z leva`*

# Rozpoložení sítě
## Schéma sítě

![je značně vidět, že máme 3 sítě](https://cdn.discordapp.com/attachments/893822214854574090/893824440012529694/unknown.png)

# Rozpoložení sítě
## Kalkulace hlavní sítě (červená) a ostatních sítí (k ní připojených) zelená a fialová

*`- každá síť musí mít svůj daný rozsah a je potřeba ke každé sítí přiřadit jinou IP adresu (viz. obr. č. 3)`*

[Stránka pro rozpočítávání sítě](https://www.calculator.net/ip-subnet-calculator.html)

![obr. č. 3](https://cdn.discordapp.com/attachments/893822214854574090/893824951860232232/unknown.png)


# Konfigurace **ČERVENÉHO SEKTORU** našeho schéma

![obr. schéma](https://cdn.discordapp.com/attachments/893822214854574090/893830525826007080/unknown.png)



- budeme postupovat následovně : 

> - Otevřeme libovolný router, v našem případě levý
> - V kategorii CLI se nás router zeptá, zda chceme začít s konfigurací,** zvolíme možnost "no" či "n"** a zmáčkneme enter
> - následovně pokračujeme **"en"** a poté **"conf t"**
> - poté se přesuneme do interfacu serialu, v našem případě se bude jednat o **interface serial 0/3/0**, budeme psát :** "int s0/3/0"** a potvrdíme
> - IP adresu přiřadíme pomocí **"ip address X.X.X.X Y.Y.Y.Y"** v našem případě  **"ip address 10.10.10.1 255.255.255.252"**, akci opět potvrdíme
> - následně napíšeme **"no shutdown"** pro aktivaci portu
> - nyní napíšeme **exit** abychom opustili daný interface a přesuneme se k interfacu gigabyte 0/0 pomocí **"int g0/0"**
> - v interfacu budeme pokračovat s přiřazením IP adresy jako minule, v našem případě "**ip address 143.93.15.1 255.255.255.240**", následně potvrdíme
> - následně opět napíšeme **"no shutdown"** pro aktivaci portu
> - napíšeme **exit**
> - v neposlední řadě (pro jistotu) se dostaneme čistě do configu (ověříme pomocí jasně viditelného **Router(config)#**) a nastavíme Defaultní gateway pomocí** ip default-gateway ** *a to ip adresu našeho rozsahu na s0/3/0,* čili **ip default-gateway 10.10.10.3**

```Veškeré tyto akce provedeme i na druhém routeru, ovšem serial se změní na 10.10.10.2 a g0/0 na 173.11.33.1```

```V této fázi máme červený sektor částečně hotový```
**`
- pakliže je toto tvrzení opravdu pravdIvé zjistíme tak, že šipečky směrem ke switchi svítí zeleně`**

# Konfigurace **ZELENÉHO** a **FIALOVÉHO SEKTORU** našeho schéma

> **ZELENÝ SEKTOR**
> - otevřeme počítač, otevřeme záložku **Desktop** a následně ***"!P Configuration"***, poté přiřadíme potřebné informace pomocí obrázku níže (obr. č. 5)

![č. 5](https://cdn.discordapp.com/attachments/893822214854574090/893832306459021392/unknown.png)

> - Poté otevřeme Switch a dostaneme se do configurace terminálu (pomocí **en** a následně** conf t**, ověříme pomocí viditelného **Switch(config)#** na začátku řádku) a nastavíme **defaultní gateway** naší sítě (V našem případě) **IP adresa portu G0/0 na routeru R1** pomocí **ip default-gateway 143.93.15.1**

``` V této fázi máme zelený sektor hotový a nyní ho budeme využívat na zkoušení spojení s R1, R2 a finálním PC ve fialovém sektoru```

# Fialový sektor

- otevřeme počítač, otevřeme záložku **Desktop** a následně ***"IP Configuration"***, poté přiřadíme potřebné informace pomocí obrázku níže (obr. č. 6)

![č. 6](https://cdn.discordapp.com/attachments/893822214854574090/893833668026568714/unknown.png)

> - Poté otevřeme Switch a dostaneme se do configurace terminálu (pomocí **en** a následně** conf t**, ověříme pomocí viditelného **Switch(config)#** na začátku řádku) a nastavíme **defaultní gateway** naší sítě (V našem případě) **IP adresa portu G0/0 na routeru R2** pomocí **ip default-gateway 173.11.33.1**

``` V této fázi máme fialový sektor hotový a nyní ho budeme využívat na zkoušení spojení s R1, R2 a finálním PC v zeleném sektoru```

# Routing

- tento krok je ve finále nejlehčí, budeme potřebovat napsat pouze dva příkazy ke každému routeru

- SPOLEČNÝ PŘIKAZ PRO OBA ROUTERY

``` ip route 0.0.0.0 0.0.0.0 s0/3/0```

> **Pro router R1 využijeme příkazy**
```
ip route 0.0.0.0 0.0.0.0 s0/3/0
ip route 173.11.33.0 255.255.255.240 s0/3/0
```

> **Pro router R2 využijeme příkazy**
```
ip route 0.0.0.0 0.0.0.0 s0/3/0
ip route 143.93.15.0 255.255.255.240 s0/3/0
```

# Finále

> - v této fázi máme kompletně vyhráno, pakliže nám funguje spojení, vše ověříme pomocí **CMD terminálu** na každém PC
> - budeme pingovat adresy **10.10.10.1 & 10.10.10.2 & 143.93.15.8 & 173.11.33.12**
> - pakliže se nám vše vrátí v této podobě *(viz. obr. č. 7)* , máme úspěšně hotovo

![č.7](https://cdn.discordapp.com/attachments/893822214854574090/893835823336812544/unknown.png)