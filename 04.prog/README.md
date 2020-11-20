# Algoritmus, implementálás, futtatás

(2020. 11. 17.)

Mittelholcz Iván

---

## 1. Mi a programozás?

- Algoritmus implementálása egy programozási nyelven.
    - Mi az algoritmus? Megengedett műveleteket tartalmazó eljárás, ami megold egy problémát.
        - I/O: általában nem tekintjük az algoritmus részének
        - megengedett műveletek: összetett feladat felbontása egyszerűbbekre, egészen addig, amíg olyan egyszerű feladatokhoz nem jutunk, amiknek már tudjuk a megoldását (a nyelv tartalmazza, pl. összehasonlítás)
    - Mi egy programozási nyelv? Írható az embernek, és elég egyértelmű, hogy lefordítható legyen gépi nyelvre.
- Summa: probléma -> algoritmus -> nyelv kiválasztása -> implementálás -> futtatás: probléma megoldva

## 2. Hogyan futtatunk egy programot linux-környezetben?

- előfeltétel: fordítás vs. értelmezés
- értelmezés: van egy program (az értelmező), ami az utasításokat beolvassa, és lefordítja gépi nyelvre
- futtatás: `interpreter fájl`, pl. `bash myscript.sh`, vagy `python3 myscript.py`
- első szkriptjeink megírása és futtatása

## 3. Mi történik a gépben, ha futtatunk egy programot?

- program a háttértáron (merevlemez)
- beolvasás a memóriába
    - kód (utasítások)
    - adatok
- kód futtatása: az adatokon a processzor elvégzi az utasításokat
- kilépés a programból, a memória felszabadíthatóvá válik
