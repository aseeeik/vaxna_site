# Nastavení banneru na Routeru či Switchi

- otevřeme libovolné zařízení (Switch / Router)

- budeme postupovat následovně :


> _*Znak (v našem případě 7 se bere jako ignorovaný a jako začátek a konec textu, je doporučeno využít znak / písmeno / číslici, která nebude v textu využita)*_

```
> en
> conf t
> banner motd 7 TEXT 7
> exit
```

- nebo

```
> en
> conf t
> banner motd 7
> TEXT
> 7
> exit
```