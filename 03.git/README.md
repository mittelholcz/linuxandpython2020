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

Tipikus munkamenet:

1. Fejlesztünk, azaz különböző fájlokat hozunk létre, szerkesztünk és törlünk.
1. Ellenőrizzük, hogy milyen változások vannak a repó eddigi állapotához képest.

   ```txt
   git status
   ```
1. Az összetartozó változásokat hozzáadjuk az *Index*-hez és új kommitot készítünk.

   ```txt
   git add file1 file2 ...
   git commit -m 'rövid leírás'
   ```
1. A 2. és 3. lépést ismételgetjük, amíg a `git status` kimenetében azt nem olvassuk, hogy `nothing to commit, working tree clean`

## Ágak

A *Git* a pillanatfelvételeket egy gráf csomópontjaiként képzeli el. Ennek alapja, hogy egy új *commit* = előző *commit* + változások (*Index*). Ezért minden *commit*-nak van (legalább) egy szülő *commit*-ja, kivéve persze a legelső *commit*-ot. Egy pillanatfelvételnek több *gyereke* is lehet, ha ugyanahhoz a *commit*-hoz különböző változtatásokat készítünk és mentünk el új pillanatfelvételekként.

A *repository* *commit*-jai így ágakba (*branch*-ekbe) szerveződnek. Egy-egy *branch* neve mindig a hozzá tartozó ág utolsó / legújabb *commit*-jára mutató címke.

Az alapértelmezett ág neve *master*. Ezt nem kell külön létrehozni, üres repó első *commit*-ja automatikusan a *master branch*-be kerül.

Kép az ágakról: ![ágak](https://i2.wp.com/digitalvarys.com/wp-content/uploads/2019/06/GIT-Branchand-its-Operations.png?fit=1921%2C1057&ssl=1)

Mint a képen látható, nem csak több gyereke lehet egy *commit*-nak, hanem több szülője is. A szokott munkamenet úgy néz ki, hogy a *master* ágban van a közös kódbázis, és ún. fejlesztési ágakban (*feature branch*-ekben) folyik egy-egy új *feature* fejlesztése. Ha egy *feature* elkészült, akkor a benne lévő változtatásokat visszaolvasztjuk a *master* ágba. Ilyenkor *master* utolsó *commit*-jához egyszerre adódik hozzá a *feature branch* összes változása.

Parancsok:

- `git branch`: Listázza a repó ágait. Színezés és csillag jelöli az aktuális ágat (azt az ágat, amiben a repó most van). Alapértelmezetten csak a lokális ágakat mutatja, de `-a` vagy `--all` kapcsolóval a távoliakat is (l. később).
- `git branch branch_name`: Új elágazás az aktuális *commit* helyén. Ez csak létrehoz egy új ágat, de nem vált át az új ágra. Ha ezután készítünk új pillanatfelvételt, akkor az az eddigi ághoz fog tartozni.
- `git checkout branch_name`: Váltás az új ágra. Ha ezután készítünk új pillanatfelvételt, akkor az már az új ághoz fog tartozni.
- A fenti két parancsot lehet rövidíteni a `git checkout -b branch_name` utasítással. Ez létrehoz `branch_name` néven egy új ágat, és rögtön át is vált rá.
- `git merge branch_name`: Az aktuális ágba olvasztja a *branch_name* ágat.
- `git branch -d branch_name`: Ág törlése.

Tipikus munkamenet:

1. Létrehozunk egy új ágat az adott fejlesztéshez és váltunk az új ágra.

   ```txt
   git checkout new_branch
   ```
1. Fejlesztünk és kommitolunk ebbe a fejlesztési ágba, amíg el nem érjük a kívánt eredményt.
1. Ha készen vagyunk, visszaváltunk a master ágra, és a fejlesztési ágat visszaolvasztjuk (merge) a master-ágba, hogy ott is meglegyenek az újdonságok.

   ```txt
   git checkout master
   git merge new_branch
   ```
1. A végén töröljük a feleslegessé vált ágat.

   ```txt
   git branch -d new_branch
   ```

## Konfliktusok

Ha szerencsénk van, akkor az ajánlott munkamenet 3. lépését (*merge*) úgy tudjuk végrehajtani, hogy időközben a *master* ágban nem történt semmilyen változás azóta, hogy elágaztattuk az új *branch*-et. Ekkor a *merge* során nem lehet a két ág között ütközés, a Git simán átmásolja a változásokat a *master*-be. Ez az ún. *Fast-forward merge*. Nem keletkezik újabb kommit, a Git a fejlesztési ágból jövő kommitot beteszi a *history* végére, legújabb kommitként.

Ha kevésbé van szerencsénk, akkor történt már változás a *master* ágban (valaki kommitolt valamit), de az nincs ütközésben a mi kommitunkkal. Ekkor a *merge* automatikusan új kommitot fog létrehozni. Megnyílik az alapértelmezett szövegszerkesztő, benne szerkeszthetjük az alapértelmezett *commit message*-et (nem feltétlenül kell).

Ha egyáltalán nincs szerencsénk, akkor olyan változás is történt a *master* ágban, ami konfliktusban van a mi változtatásunkkal (konkrétan ugyanannak a fájlnak ugyanabban a sorában van nem ugyanolyan változás). Ekkor a *merge* listázza a konfliktusos fájlokat és hibaüzenettel elszáll (*Automatic merge failed; fix conflicts and then commit the result.*). Ha megnyitjuk a konfliktusos fájlt, akkor látjuk, hogy a Git megjelölte az általa feloldani nem tudott konfliktust:

```txt
<<<<<<< HEAD
Aktuális branch-ben lévő változat.
=======
A beolvasztani kívánt branch-ben lévő változat.
>>>>>>> brach_name
```

Megjegyzés: A 'HEAD' mindig az aktuális helyünket jelöli a history-ban, azaz azt a kommitot, ami épp *checkout*-olva van (l. később), ez általában az aktuális ág utolsó kommit-ja.

Egy szerkesztőben oldjuk fel a konfliktusokat: töröljük a `<<<<<<<`, `=======` és `>>>>>>>` sorokat és a nem kívánt változatot (vagy törölhetjük mindkét változatot és írhatunk egy öszvért/újat). Utána a szokásos `git add`-dal és `git commit`-tal véglegesíthetjük az összefésülést és a konfliktus feloldását, a `git log --graph`-fal pedig ellenőrizhetjük az összefésülést.
A `git merge` paranccsal nem csak a *master* ágba lehet más ágat beolvasztani, hanem bármelyik ágba bármit. Egy *feature-branch*-ben való fejlesztés során is lehet olyan ötletünk, amit külön ágban szeretnénk kipróbálni. Ekkor az aktuális fejlesztési ágat ágaztatjuk el, és ha sikeresnek bizonyult a kísérlet, abba is olvasztunk vissza. Az is előfordulhat, hogy fejlesztünk egy külön ágban, miközben *master* ágban olyan változás történt, amire szükségünk lenne a további fejlesztés során. Ekkor a fejlesztési ágból adjuk ki a `git merge master` parancsot, hogy aktualizáljuk a saját águnkat a *master*-ben lévő újdonságokkal.

A *merge* alkalmazásának lehetséges alternatívája a *git rebase* parancs, de egyelőre inkább kerüljük a használatát.

## Távoli munka, munka másokkal

- `git clone user@host:/path/to/repo`: Távoli repó másolása aktuális gépre.
- `git push távoli_gép fejlesztési_ág`: Saját, új *commit*-ok másolása a távoli gépre.
