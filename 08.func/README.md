# Függvények

(2021. 01. 15.)

Mittelholcz Iván

---

## Függvény definíciója

```py
def fuggvenynev(param1, param2, ..., paramX):
    <utasitas1>
    <utasitas2>
    ...
    return <value>
```

- a `def` kulcsszó jelenti, hogy itt egy függvény definíciója következik
- a függvény neve bármilyen érvényes változónév lehet: betű, alulvonás, szám (de számmal nem kezdődhet)
- a paraméterek nevei érvényes változónevek lehetnek és csak a függvényben érvényesek (külső változók el lesznek "takarva")
- utasítások: bármilyen érvényes python utasítás lehet egy függvényben
- a `return` opcionális, ha nincs, akkor is van, és visszatérési érték `None` lesz

## Függvény hívása

Ha kíváncsiak vagyunk az eredményre:

```py
valtozo = fuggvenynev(param1, param2, ..., paramX)
```

Ha csak a mellékhatás miatt hívjuk:

```py
fuggvenynev(param1, param2, ..., paramX)
```

- a paraméterek lehetnek változók de közvetlen értékek is
- ha változók, akkor nem kell hogy azonos nevűek legyenek a függvény definíciójában lévőkkel

## Alapértelmezett paraméterek

Definíció:

```py
def fuggvenynev(param1, param2, ... defparam1=val1, defparam2=val2, ...):
```

Hívás:

```py
# pozíció szerint
fuggvenynev(param1, param2)
fuggvenynev(param1, param2, val1)
fuggvenynev(param1, param2, val1, val2)
# vagy nev szerint (csak a pozíció szerintiek után)
fuggvenynev(param1, param2, defparam2=val2)
# rossz: fuggvenynev(defparam2=val2, param1, param2)
```

## First class citizen

- átadható más függvénynek paraméterként
- lehet függvény visszatérési értéke
- változónak lehet értékül adni

Példa paraméterként átadásra:

```py
d = {'a': 3, 'b': 2, 'c': 7}

def get_value(item):
    return item[1]

sorted(d.items(), key=get_value)
sorted(d.items(), key=get_value, reverse=True)
```

## Lambda-függvények

```py
lambda param1, param2, ... : return_value
```

- rövid (egy soros), névtelen függvek
- általában egyszer használjuk, más függvény paramétereként
- ha nagyon szeretnénk többször használni, akkor eltárolhatjuk egy változóban (de inkább ne)
- nincs `return`, de a `:` utáni kifejezés kiértékelődik és rendes visszatérési érték adódik vissza

Példa (`sorted()`, még egyszerűbben):

```py
d = {'a': 3, 'b': 2, 'c': 7}

sorted(d.items(), key=lambda x: x[1])
```

## Feladatok

- Készítsetek függvényekből álló programot, ami szógyakoriságot számol:
  - legyen benne egy függvény, ami tetszőleges szöveget fogad és egy szótárat ad vissza, amiben a szavak gyakorisásga van
  - legyen benne egy függvény, ami egy gyakorisági szótárat fogad és `(szó, előfordulás)` tuple-ök listáját adja vissza előfordulás szerint csökkenő sorrendbe rendezve
  - legyen egy függvény, ami a kiírást intézi
- Készítsetek egy függvényt, ami egy tetszőleges sorozatot és egy igaz/hamissal visszatérő tetszőleges függvényt fogad. Térjen vissza azzal a legnagyobb elemmel, amire igaz a függvény
