# Zabezpečení Routeru či Switche pomocí hesla

- otevřeme libovolné zařízení (Switch / Router)

- budeme postupovat následovně :

```
> en
> conf t
> enable secret <HESLO>    \    
                            |---- Bezpečnější varianta možnost secret
> enable password <CISCO>  /
> exit
```