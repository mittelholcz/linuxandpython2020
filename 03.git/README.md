# Git

Mit csinál?

- Egy könyvátárról (*repositopry*) készít pillanatfelvételeket (*commit*-okat).

Mire jó ez?

1. Régebbi állapotokat visszaállítani.
2. Másokkal való munkát megkönnyíteni.

## Milyen parancsokat kell ismerni alapfokon?

- `git status`: A legfontosabb parancs. Megmutatja, hogy
  - mik az új fájlok a könyvtárban, amiket hozzá kell (lehet) adni a repóhoz,
  - mik a megváltoztatott fájlok, amik változásait hozzá kell (lehet) adni a repóhoz
- `git add filename`: az új, vagy megváltozott fájlt adja hozzá az *Index*-hez (v. *Stage*-hez)
  - Mi az az *Index* (v. *Stage*)? Ez a *commitok* "előszobája", itt várhatják be egymást az összetartozó változások, hogy ugyanannak a *commitnak* a részei legyenek. Azok a változások, amiket nem adunk az *Index*-hez, nem lesznek a készülő *pillanatfelvétel* részei.

  A `git add`-nek a `filename` helyett az `--all` kapcsolót is meg lehet adni, ekkor az összes megváltozott és új fájl bekerül az *Index*-be.
- `git reset filename`: Ez a `git add` ellentéte, az adott fájlt kiveszi az *Index*-ből, így az nem lesz a *commit* része, de egyébként a fájlt nem módosítja, az eddigi változtatások megmaradnak.
- `git checkout filename`: Fájl eredeti állapotának visszaállítása, eddigi módosítások elvetése.

  A `git reset --hard` parancs az összes *Index*-ben lévő fájlt eltávolítja és mindent visszaállít az eredeti állapotba (utolsó *commit*).
- `git commit -m'commit message'`: Új pillanatfelvétel készítése az előző *commit* plusz az *Index*-ben lévő változtatások alapján.
- `git log`: Az eddigi pillanatfelvételek listája. Mutatja a *commit* egyedi ID-ját is és a *commit*-hoz tartozó üzenetet is (*commit message*)
- `git checkout commit_ID`: Régebbi pillanatfelvétel "betöltése". Elég az ID első 7-8 karakterét bemásolni a `git log`-ból, nem kell az egész ID.

## Ágak

A *Git* a pillanatfelvételeket egy gráf csomópontjaiként képzeli el. Ennek alapja, hogy egy új *commit* = előző *commit* + változások (*Index*). Ezért minden *commit*-nak van (legalább) egy szülő *commit*-ja, kivéve persze a legelső *commit*-ot. Egy pillanatfelvételnek több *gyereke* is lehet, ha ugyanahhoz a *commit*-hoz különböző változtatásokat készítünk és mentünk el új pillanatfelvételekként.

A *repository* *commit*-jai így ágakba (*branch*-ekbe) szerveződnek. Egy-egy *branch* neve mindig a hozzá tartozó ág utolsó / legújabb *commit*-jára mutató címke.

- `git branch`: listázza a repó ágait (lokálisan). Színezés és csillag jelöli az aktuális ágat (azt az ágat, amiben a repó most van).

  A `git branch -a` parancs nem csak a lokális, hanem a távoli ágakat is mutatja (l. később).
- `git checkout -b branch_name`: Új ág létrehozása `branch_name` néven.

Kép az ágakról: ![ágak](https://i2.wp.com/digitalvarys.com/wp-content/uploads/2019/06/GIT-Branchand-its-Operations.png?fit=1921%2C1057&ssl=1)

Mint a képen látható, nem csak több gyereke lehet egy *commit*-nak, hanem több szülője is.

## Távoli munka, munka másokkal

- `git clone user@host:/path/to/repo`: Távoli repó másolása aktuális gépre.
- `git push távoli_gép fejlesztési_ág`: Saját, új *commit*-ok másolása a távoli gépre.
