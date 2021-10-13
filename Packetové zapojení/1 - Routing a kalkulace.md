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
**`- pakliže je toto tvrzení opravdu pravdIvé zjistíme tak, že šipečky směrem ke switchi svítí zeleně`**

