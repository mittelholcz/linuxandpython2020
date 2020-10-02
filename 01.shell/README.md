# A parancssor használatának alapjai (2. rész)

(2020. 10. 02. - 2. óra)

Mittelholcz Iván

---

## 1. Írás, olvasás, átirányítás

Képernyőre (*standard output*, *stdout*) írás:

```sh
echo 'Helló shell!'
```

stdout átirányítása fájlba:

```sh
echo 'Helló shell!' >tmp/a.txt
echo 'Helló shell!' >tmp/a.txt
echo 'Helló másik!' >tmp/b.txt
```

Fájl olvasása:

```sh
less tmp/a.txt
less tmp/b.txt
```

- kilépés: `q`
- kersés: `/`

Kimenet átirányítása hozzáfűzéssel:

```sh
echo 'Új mondat.' >>tmp/a.txt
```

stdin másolása stdout-ra:

```sh
cat
```

stdin átirányítása fájlra:

```sh
cat <tmp/a.txt
```

Fájlok összefűzése (*concatenation*):

```sh
cat tmp/a.txt tmp/b.txt
```

Csatorna (*pipe*):

A `|` karakterrel lehet egy parancs kimenetét átadni a következő parancsnak bemenetként.

```sh
ls | wc
```

`wc`: Sorok, szavak és karakterek számolása.

- `-l`: sorok
- `-w`: szavak
- `-c`: karakterek

### Összefoglalás

- `command <filename`: fájl → stdin
- `command >filename`: stdout → fájl (felülír)
- `command >>filename`: stdout → fájl (appendál)
- `command 2>filename`: stderr → fájl
- `command1 | command2`: 1. parancs stdout → 2. parancs stdin

Speciális fájl a `/dev/null`, ami minden adatot "elnyel". Pl. a `command 2>/dev/null` minden hibaüzenetet eltüntet, csak a "rendes" kimenet lesz olvasható.

## 2. Stringmanipuláció

### Keresés

`grep <kifejezés>`: Fájl vagy a stdin szűrése, a kifejezést tartalmazó sorokra.

- `-i`: ignore case
- `-v`: fordított működés - a nem illeszkedő sorokat átengedi, az illeszkedőket kiszűri
- `-r <könyvtár>`: rekurzívan keres a könyvtár minden alkönyvtárjában
- `-f <fájl>`: nem kell kifejezést megadni, helyette a megadott fájlból olvassa ki a keresett kifejezéseket (egy sor = egy kifejezés)

### Csere

`sed "s/mit/mire/g"`: Kifejezés keresése és cseréje fájlban vagy stdin-en.

### Rendezés

`sort`: Sorok ábécé szerinti rendezése.

- `-n`: numerikus rendezés (a default lexikális helyett, pl. 10 > 9)
- `-r`: fordított sorrend

### Egyelés

`uniq`: Dupla sorok szűrése. Csak az egymást követő azonos sorokat egyeli, ezért előtte szükséges lehet rendezni.

- `-c`: a sorok elé írja, hány darab volt belőlük

### Feladat

Csináljunk szógyakorisági listát a tmp könyvtárunkban lévő fájlokból.

- segítség: sortörést a `\n` karktersorozattal lehet helyettesíteni

### 3. Ajánlott irodalom

- Software Carpentry: [The Unix Shell](http://swcarpentry.github.io/shell-novice/)- kezdőknek is jó tutorial
- [Bash dokumentáció](https://www.gnu.org/software/bash/manual/) - nagyon részletes, de ha tudjátok mit kerestek, hasznos lehet
