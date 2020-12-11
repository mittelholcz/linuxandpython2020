# Vezérlési szerkezetek

(2019. 12. 11.)

Mittelholcz Iván

---

## Bevezető

1. szekvencia
1. elágazás
1. ciklus

## 1. Szekvencia

Utasítások egymásutánja:

```py
utasitas1()
utasitas2()
```

## 2. Elágazás

Feltétel teljesülése esetén az egyik, nem teljesülése esetén egy másik utasítás fut le:

```py
if ch in 'aeiou':
    print('mgh')
else:
    print('msh')
```

Az `else` ág opcionális (ha a feltétel nem teljesül, nem történik semmi):

```py
if uj_fizetes > 147000:
    allast_valtok()
```

Lehet kettőnél több ágat is bevezetni (`elif`):

```py
if ch in 'aeiou':
    print('mgh')
elif ch in 'bcdfghjklmnpqrstvwxyz':
    print('msh')
else:
    print('nem betű')
```

## 3. Ciklus

Ugyan azt az utasítás sokszor hajtjuk végre:

- amíg egy feltétel teljesül: `while`
- egy gyűjteményes adattípus minden elemére: `for`

### 3.1. *while*-ciklus

Álláskeresés:

```py
while fizetes < 200000:
    allast_keresek()
```

Számok kiírása:

```py
x = 0
while x < 10:
    x += 1
    print(x)
```

### 3.2. *for*-ciklus

Lista / tuple / halmaz bejárása:

```py
for i in container:
    print(i)
```

Szótár kulcsainak bejárása:

```py
for key in mydict:
    print(key, mydict[key])
```

Szótár kulcs-érték párjainak bejárása:

```py
for k, v in mydict.items():
    print(k, v)
```

### 3.3. *continue*, *break*

`continue`: Ugrás a ciklus következő lépésére

```py
for word in 'alma alma piros alma'.split():
    if word.startswith('a'):
        continue
    print(word)
```

`break`: kilépés a ciklusból

```py
for word in 'alma alma piros alma'.split():
    if word == 'piros':
        break
    print(word)
```

## Feladatok

1. Legyen egy számokat tartalmazó listánk. Adjuk össze az elemeit!
1. Legyen egy számokat tartalmazó listánk. Mennyi a számok átlaga?
1. Legyen egy szavakat tartalmazó listánk. Mekkora az átlagos szóhossz?

---

1. Legyen egy szavakat tartalmazó listánk. Hány szó kezdődik 'a'-val?
1. Legyen egy szavakat tartalmazó listánk. Hány szó kezdődik magánhangzóval?

---

1. Legyen egy szavakat tartalmazó listánk. Mely szavak kezdődnek 'a'-val?
1. Legyen egy szavakat tartalmazó listánk. Mely szavak kezdődnek magánhangzóval?

---

1. Legyen egy szövegünk. Melyik a leghosszabb szava?
1. Legyen egy szövegünk. Melyik a legtöbbféle betűt tartalmazó szava?
1. Legyen egy szövegünk. Melyik a leghosszabb, magánhangzóval kezdődő szó?

### További feladatok

- Legyen egy egész számokat tartalmazó listánk. Növeljük meg a lista minden elemét eggyel!
- Legyen egy szövegünk. Számoljunk szógyakoriságot. Az eredményt tároljuk egy szótárban (`{szó: előfordulás}`).
  - Próbáljuk meg kiiratni a szótár elemeit gyakoriság szerint csökkenő sorrendben!
  - Írjuk ki a relatív gyakoriságot!
