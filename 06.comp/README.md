# Összetett adattípusok

(2020. 11. 27.)

Mittelholcz Iván

---

## 1. Karakterláncok (*string*)

- lehetséges értékek: ~
- jelölés: `'valami'` vagy `"valami"`
- műveletek: `+ <string>`, `* <int>`, `<`, `<=` `>`, `>=`

### 1.1. Karakterláncok indexelése, szeletelése

- `s[i]`: `s` karakterlánc `i`-edik karaktere
- `s[:i]`: `i`-edik karakterig az összes, `i` már nem
- `s[i:]`: `i`-edik karaktertől az összes, `i` is
- `s[i:j]`: `i`-edik karaktertől a `j`-edikig, `i`-edik benne van `j`-edik már nincs

### 1.2. Karakterláncok metódusai

- `s.upper()`: nagybetűsít
- `s.lower()`: kisbetűsít
- `s.endswith(suffix)`: igaz, suffixszel végződik a string
- `s.startswith(prefix)`: igaz, prefixszel kezdődik a string
- `s.isdigit()`: igaz, ha `s` csak számjegyeket tartalmaz
- `s.isalpha()`: igaz, ha `s` csak betűket tartalmaz
- `s.isspace()`: igaz, ha `s` csak szóközjellegű karaktereket tartalmaz
- `s.strip()`: levágja a string elején és végén lévő szóközjellegű karaktereket
  - a `s.strip(karakterek)` levágja szóközök helyett a felsorolt karaktereket vágja le
  - az `lstrip()`, és az `rstrip()` csak a bal- ill. jobboldaliakat vágja le
- `s.split(delimiter)`: felszeleteli a stringet delimiterek mentén, a szeletek listáját adja vissza
  - a `s.split()` a szóközjellegű karaktereket mentén darabol
- `s.replace(mit, mire)`: lecseréli a stringben az elsőként megadott paraméter előfordulásait a második paraméterre

További metódusok: <https://docs.python.org/3/library/stdtypes.html#string-methods>

## 2. Rendezett sorozatok (*tuple*)

- objektumreferenciák rendezett sorozata
  - nem magukat az objektumokat tárol, hanem objektumokra való hivatkozásokat
  - nem változtatható (*immutable*)
- jelölés: `(x1, x2, ...)`
- indexelhető (`t[i]`) és szeletelhető (`t[i:j]`, ill. `t[i:j:k]`) a *string*ekhez hasonlóan
- kapcsolódó függvények: `tuple()`, `len()`, `min()`, `max()`, `sum()`, `all()`, `any()`, `sorted()`
- műveletek: `+`, `*`, `in`, `not in`
- metódusok: `t.index(x)`, `t.count(x)`

## 3. Listák (*list*)

- ugyan az, mint a *tuple*, csak változtatható (*mutable*)
- jelölés: `[x1, x2, ...]`
- kapcsolódó függvények: `list()`
- további műveletek: `l[i] = x`, `l[i:j] = [...]`, `del l[i]`, `del l[i:j]`
- további metódusok: `l.append(x)`, `l.pop()`, `l.insert(x)`, `l.remove(x)`, `l.sort()`

## 4. Halmazok (*set*)

- objektumreferenciák halmaza
  - minden értéket csak egyszer tárol
  - sorrend nem számít
  - változtatható (*mutable*)
- jelölés: `{x1, x2, ...}`
- nem indexelhető!
- kapcsolódó függvények: `set()`, `len()`, `min()`, `max()`, `sum()`, `all()`, `any()`, `sorted()`
- műveletek: `in`, `not in`, `s1 | s2`, `s1 & s2`, `s1 - s2`, `<`, `<=`, `>`,  `>=`
- metódusok: `s.add(x)`, `s.remove(x)`, `s.discard(x)`, `s.pop()`

## 5. Szótárak (*dict*)

- Kulcs-érték párok halmaza
  - minden kulcsnak egyedinek kell lennie
  - a kulcsoknak változtathatatlanoknak kell lenniök
  - sorrend nem számít
  - maga a szótár változtatható (*mutable*)
- jelölés: `{k1: v1, k2: v2, ...}`
- indexelhető kulccsal, de nem sorszámmal: `d[k]`
- nem szeletelhető!
- kapcsolódó függvények: `dict()`, `len()`, `min()`, `max()`, `sum()`, `all()`, `any()`, `sorted()`
- műveletek: `key in d`, `key not in d`, `d[k] = v`, `del d[k]`
- metódusok: `d.get(k)`, `d.keys()`, `d.values()`, `d.items()`
