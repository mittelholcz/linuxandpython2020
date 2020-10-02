# Reguláris kifejezések

(2019. 10. 02. - 3. óra)

Mittelholcz Iván

---

## 1. Reguláris kifejezések elmélete

*ábécé*: karakterek nem üres, véges halmaza

*string*: az ábécé karaktereiből álló véges sorozat

*üres string*: nulla hosszúságú string

*Kleene-csillag* (v. lezárt): az ábécé feletti összes string halmaza

*nyelv*: Kleene-lezárt egy részhalmaza

*reguláris kifejezés*: stringek egy halmazát határozza meg (egy *reguláris nyelvet*), tartalmazhat literális karaktereket ill. az alábbi műveleteket.

Műveletek:

- Konkatenáció: *R1* és *R2* reguláris kifejezés, ekkor *R1R2* is regularis
  kifejezés és *R1R2* = {*ab* : *a* eleme *R1* és *b* eleme *R2*}.
- Unió: *R1* és *R2* reguláris kifejezés, ekkor *R1 unió R2* is regularis
  kifejezés és *R1 unió R2* = {*a* : *a* eleme *R1* vagy *a* eleme *R2*}.
- Kleene csillag: *R* reguláris kifejezés, ekkor *R\** is reguláris
  kifejezés, mely tartalmazza az üres stringet és *R* elemeinek tetszőleges
  konkatenációját.

## 2. Megvalósítás

Több szabványos "nyelvjárás" létezik (de ezeken túl az egyes programok is
működhetnek különbözőképpen):

- *basic* (BRE): kerek és kapcsos zárójelek eszképelve, nincs `+`, `?` és `|`
- *extended* (ERE): ezt fogjuk tanulni
- *perl-kompatibilis* (PCRE): lustaság és sok minden más (Python-ban is
ilyesmi van)

A *grep* és a *sed* alapból a BRE-t használják.

- *sed -r* vagy *sed -E*: kiterjesztett regularis kifejezések (ERE)
  használata - *grep -E* vagy *egrep*: kiterjesztett regularis kifejezések
  (ERE) használata - *grep -P*: PCRE használata

### Szintaxis

Pozícióra (nulla karakterre) illesztés:

- `^`: string / sor elejére illeszkedik
- `$`: string / sor végére illeszkedik

Egy karakterre illesztés:

- `.`: bármilyen karakterre illeszkedik
- különleges karakterre azt iszképelve lehet illeszteni, pl. `\.` illeszkedik a *.*-ra.
- `x`: literális karakter, saját magára illeszkedik
- `[ ]`: a zárójelen belül felsorolt karakterek valamelyikére illeszkedik, pl. `[ab]` illeszkedik az `a` vagy a `b` karakterre, másra nem.
  - Megadható tartomány is, pl `[a-z]` illeszkedik az ASCII kisbetűkre, `[0-9]` pedig a számjegyekre.
  - Ha a kötőjelet is be akarjuk venni a felsorolt karakterek közé, akkor a felsorolás elejére vagy végére kell írni.
  - A szögletes zárójelen belül más karakterek elveszítik speciális jelentésüket, pl. `[.]` egy literális pontra illeszkedik, nem pedig bármire.
- `[^ ]` illeszkedik a zárójelen belül fel nem sorolt karakterek valamelyikére. Megadható tartomány is, pl. `[^A-Z0-9]` illeszkedik minden karakterre, ami nem ASCII nagybetű és nem is számjegy.

Változó hosszúságú illesztések (mindig mohó):

- `|`: Alternáció, az előtte vagy az utána következő regex valamelyikére illeszkedik, pl. `abcd|xyz` illeszkedik *abcd*-re és *xyz*-re is. Alternációt lehatárolni zárójellel lehet, pl. `ab(cd|xy)z` illeszkedik az `abcdz` és az `abxyz` stringekre.
- `()`: A zárójelen belüli kifejezés megnevezett csoport lesz, amire később hivatkozni lehet. Általában egymásba ágyazhatók, de nem fedhetnek át. A `(a.(.a))` illeszkedik pl. az *abba* stringre. Zárójelre hivatkozni backslash-sel lehet: `\(` és `\)`
- `\n`: Hivatkozás egy csoportra. Pl. `(a.(.a)) \2 \1` illeszkedik az *abba ba abba* stringre.
- `?`: nulla vagy egy az előző karakterből / csoportból
- `*`: nulla vagy bármennyi az előző karakterből / csoportból
- `+`: legalább egy az előző karakterből / csoportból
- `{m,n}`: minimum *m*, maximum *n* darab az előző karakterből / csoportból.
  - `{m,}` alakban csak a minimumot is megadhatjuk (a maximum ekkor bármennyi lehet, hasonlóan a `*`-hoz).
  - `{,n}` alakban csak a maximumot is megadhatjuk (a minimum ekkor nulla, hasonlóan a `*`-hoz)
  - `{m}`

Műveletek precedenciája: *csillag > konkatenáció > alternáció*

Különleges karakterek:

- `\n`: új sor (new line)
- `\t`: TAB
- `\s`: whitespace karakterek
- `\S`: nem whitespace karakterek
- `\w`: szóalkotó karakterek (számjegyek, betűk és alulvonás)
- `\W`: nem szóalkotó karakterek

Egy-egy reguláris nyelv általában sokféleképpen megadhatók regexekkel (pl. `a+` = `aa*`), nincs igazán jó egyszerűsítő módszer, ezért érdemes jól megírni a regexeket!

### Gyakorlatok

- Hány szó kezdődik *a*-val egy listában?
- Hány szó kezdődik *a*-val folyó szövegben?
- Hány három betűs szó van a szövegben?
- Hány zárójelpár van a szövegben?
- Írjunk *grep* parancsot, ami alkalmas egy szövegben található szóismétlések szűrésére!
- Írjunk *sed* parancsot, ami a bemenetének minden szavát megismételteti! (pl. *Hát maga megbolondult?* $\to$ *Hát Hát maga maga megbolondult megbolondult?*)
- Készítsünk megint szógyakorisági listát egy szövegből, de most dobjuk ki a punktuációkat is, azaz az 'alma', az 'alma!' és az 'alma)' egyaránt az 'alma' type gyakoriságát növelje!
- Hogyan tudnánk kiszűrni a gyakorisági listából a funkciószavakat, ha volna egy listánk róluk?
