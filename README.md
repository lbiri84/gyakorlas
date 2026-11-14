# Gyakorló

Gyakorló oldal 3. osztályosoknak: matek, nyelvtan és környezetismeret, kérdés-felelet formában, pontokkal és jelvényekkel. Egyetlen `index.html`, build nélkül. Nincs fiók, semmit nem küld sehová: a pontok és jelvények csak a készülék böngészőjében (localStorage) vannak.

- **Matek (számok és műveletek 200-ig, mérések):** számok 200-ig, helyi érték, számegyenes, számszomszédok és kerekítés, összeadás-kivonás, szorzás-osztás, szöveges feladatok, mérések (tömeg, hossz), pénz és visszajáró. A feladatok generáltak, minden kör új számokkal.
- **Nyelvtan:** j vagy ly?, szófajok, mondatfajták, ABC-sorrend.
- **Környezetismeret:** az élet feltételei (élő és élettelen, életfeltételek, táplálkozás), állatcsoportok vegyesen, valamint külön az emlősök, madarak, hüllők, kétéltűek és a rovarok (bogarak): testtakaró, belső vagy külső váz, testfelépítés, szaporodás, kicsinyek, fejlődés.
- **Vegyes kör:** 10 kérdés az összes témából.
- Egy kör 10 véletlenszerű kérdés, 4 (vagy 2–3) válaszlehetőséggel, azonnali visszajelzéssel és magyarázattal.
- Jutalom: 10 pont minden jó válaszért, +50 pont hibátlan körért, szintek (1–9+), napi sorozat és 9 jelvény.
- Offline működik, telepíthető a kezdőképernyőre (PWA).

## Fejlesztés

- A tokenek a központi design systemből töltődnek: `https://laszlobiri.com/design-system/tokens.css`. Helyi `tokens.css` másolat nincs, és a `sw.js` előre mentett listájába sem kerül.
- Mindig a palakék (slate) téma.
- A `sw.js`-ben minden kiadásnál emeld a gyorsítótár verzióját (`gyakorlo-vN`).
- Új feladattípus: a `GEN` objektumba egy generátor (`prompt`, `text`, `choices`, `correct`, `explain`, opcionálisan `key` a körön belüli ismétlés kizárására), és egy sor a `TOPICS` listába. A környezetismereti tartalom adatai a `GR` (állatcsoportok), `FACTS` és `CLUES` objektumokban vannak.
- A feladatgenerátorokat külön ellenőriztem: témánként 3000 generált kérdésre a helyes válasz egyezik a kiszámolt értékkel, és a válaszlehetőségek egyediek.

## Publikálás

GitHub Pages (`main` / root), egyéni domain: `gyakorlas.laszlobiri.com` (a `CNAME` fájl tartalmazza).
DNS: `CNAME` rekord, host `gyakorlas`, érték `lbiri84.github.io`.
