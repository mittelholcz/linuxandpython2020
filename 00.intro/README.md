# A parancssor használatának alapjai

(2020. 09. 25. - 1. óra)

Mittelholcz Iván

---

## 1. Alapfogalmak

Kernel (rendszermag): erőforrások kezelése, absztrakció

- feladatütemezés (folyamatok hozzáférése a CPU-hoz)
- memória (RAM) kezelés
- fájlrendszer
- stb.

Alkalmazások:

- külön programok
- a kernelen keresztül férnek hozzá a gép erőforrásaihoz

Shell (rendszerhéj): karakteres felhasználói felület alkalmazások futtatására

- maga is alkalmazás, több féle van, cserélhető
- mostanában Linux-ok többségén és OS X-en a bash az alapértelmezett
- programozási nyelv is

## 2. Történelem

- 1969: UNIX oprendszer. Kezdetben hozzávágják mindenkihez, aki gépet vesz, aztán rájönnek, hogy a szoftver is lehet üzlet → zárt lesz.
- 1983: GNU (GNU's Not Unix). UNIX-szerű, de nem tartalmaz UNIX-ból származó kódot (mindent újraimplementálnak nulláról). Open source. Kernel nincs, minden más van (C fordító, debugger és library, shell, make, TeX, ablak kezelő, stb.).
- 1991: Linux kernel.
- Azóta:
  - __UNIX-like__ (*nix): olyan rendszerek, amik *hasonlóan néznek ki*, mint a UNIX (GNU/Linux, BSD, OS X, stb.)
  - __GNU/Linux__: Linux kernel + GNU eszközök + mindenféle más. Röviden ezt nevezik Linux-nak.
  - __Linux disztribúció__: *GNU/Linux* + csomagkezelő, grafikus felület, egyéb programok

## 3. Parancsok

Hogy néz ki egy parancs?

```sh
ls # sima parancs
ls -l # parncs "kapcsolóval"
ls /home # argumentum / paraméter
ls -al *rc # wildcard
```

Kapcsolók:

- opcionálisak vagy kötelezőek
- rövidítettek vagy hosszúak (pl. `-a` vagy `--all`)
- össze nem vontak vagy összevontak (pl. `-a -l` vagy `-al`) -- ez csak a rövidítettekre működik!
- értéktelenek vagy értékesek esetleg opcionálisan értékesek (pl. az `ls --color` ugyan az, mint az `ls --color=always`, de nem ugyanaz, mint a `ls --color=never`).

## 4. Információk

```sh
<parancs> -h
<parancs> --help
man <parancs>
```

`man`:

- kilépés: `q`
- keresés: `/`

## 5. Fájlkezelés

A könyvtárak, fájlok közötti szeparátor a perjel (`/`), nem pedig a backslash (`\`), mint windows-ban!

Minden felhasználónak van egy ún. *home* könyvtára, ami a `/home/<felhasználónév>` útvonalon érhető el.

Alapvető parancsok:

- `ls`: könyvtár tartalmának listázása (*list*)
- `mkdir <könyvtár>`: könyvtár létrehozása (*make directory*)
- `rmdir <könyvtár>`: könyvtár törlése (csak üres könyvtárra, *remove directory*)
- `cp <honnan> <hova>`: fájl/könyvtár másolása (*copy*)
- `mv <mit> <mire>`: fájl/könyvtár átnevezése/mozgatása (*move*)
- `rm <fájl>`: törlés (*remove*)
- `pwd`: aktuális könyvtár kiírása
- `cd <hova>`: aktuális könyvtár váltása (*change directory*)
- `ln -s <mit> <hova>`: egy *link*-et hoz létre, amin keresztül szintén elérhető lesz a fájl/könyvtár (*symbolic link*)
- `touch <fájl>`: üres fájl létrehozása

Kiemelt könyvárak rövidítései:

- `.`: jelenlegi könyvtár
- `..`: szülő könyvtár
- `/`: gyökér könyvtár
- `~`: a felhasználó *home* könyvtára

*Wild card* vagy *joker* karakterek:

- `?` egy tetszőleges karakter helyett állhat
- `*` bárhány bármi helyett állhat
- `[chars]`: a szögletes zárójelben megadott karakterek valamelyike helyett állhat, tartomány is használható (pl. `[A-Z]` egy nagybetűt helyettesíthet)

Egy fájlt / könyvtárat meg lehet adni abszolút és relatív módon is:

- *abszolút*: a gyökértől
- *relatív*: az aktuális könyvtártól

### 6. Feladatok

1. Hozzunk létre a *home*-unkban egy `tmp/` könyvtárat!
1. Hozzunk létre a `tmp`-n belül egy `src/` könyvtárat, amiben kettő .txt és egy .py fájl van.
1. Másoljuk át a .txt fájlokat a `tmp/` könyvtárba.
1. Töröljük ki az `src/` könyvátrat.


### 7. Ajánlott irodalom

- Software Carpentry: [The Unix Shell](http://swcarpentry.github.io/shell-novice/)- kezdőknek is jó tutorial
- [Bash dokumentáció](https://www.gnu.org/software/bash/manual/) - nagyon részletes, de ha tudjátok mit kerestek, hasznos lehet
