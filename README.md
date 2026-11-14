# Gyakorló

Gyakorló oldal 3. osztályosoknak: matek, nyelvtan és környezetismeret, kérdés-felelet formában, pontokkal és jelvényekkel. Egyetlen `index.html`, build nélkül. Csak belépve használható; a pontok és jelvények a laszlobiri közös backendjébe mentődnek, gyerekprofilonként.

- **Matek (számok és műveletek 200-ig, mérések):** számok 200-ig, helyi érték, számegyenes, számszomszédok és kerekítés, összeadás-kivonás, szorzás-osztás, szöveges feladatok, mérések (tömeg, hossz), pénz és visszajáró. A feladatok generáltak, minden kör új számokkal.
- **Mini játékok:** 50 pontonként a kör végén felváltva akasztófa vagy szókereső (10×10-es tábla, 5–6 elrejtett szó) ajánlódik fel, elfogadható vagy elvethető. A szavak az anyagból valók. Siker +10 pont, az első győzelem jelvényt ad.
- **Nyelvtan:** j vagy ly?, szófajok, mondatfajták, ABC-sorrend.
- **Környezetismeret:** az élet feltételei (élő és élettelen, életfeltételek, táplálkozás), állatcsoportok vegyesen, valamint külön az emlősök, madarak, hüllők, kétéltűek és a rovarok (bogarak): testtakaró, belső vagy külső váz, testfelépítés, szaporodás, kicsinyek, fejlődés.
- **Vegyes kör:** 10 kérdés az összes témából.
- Egy kör 10 véletlenszerű kérdés, 4 (vagy 2–3) válaszlehetőséggel, azonnali visszajelzéssel és magyarázattal.
- Jutalom: 10 pont minden jó válaszért, +50 pont hibátlan körért, szintek (1–9+), napi sorozat és 9 jelvény.
- Offline működik, telepíthető a kezdőképernyőre (PWA). A gyerek tableten telepített appként használd: böngészőfülben a Safari egy hét használat nélkül törölheti a párosítást.

## Gyerekprofilok, szülői nézet, gyerek mód

- **Szülő**: Google-belépéssel (`https://laszlobiri.com/belepes/`). A kezdőképernyőn „Ki gyakorol?”: a gyerek kiválasztása; a „Szülői nézet”-ben gyerekprofil létrehozása és törlése, a gyerekek eredményei, a gyerek tabletek listája és párosítása.
- **Gyerekprofil**: csak becenév és egy ikon. A gyereknek nincs fiókja.
- **Eredmények**: csak a befejezett kör és a megnyert minijáték mentődik (`results`, `pupil_badges`). A pont, a szint, a napi sorozat és a témánkénti legjobb ezekből számolódik. Offline is működik: a laszlobiri.com/lib/v1/outbox.js kimenő sorból visszatérő hálózatnál elmegy.
- **Gyerek mód** (a gyerek saját tabletje): a szülő a „Szülői nézet” → „Párosító kód kérése” gombbal 10 percig érvényes kódot kap, a tableten a `gyakorlas.laszlobiri.com/#parositas` oldalon beírja, és megad egy 4 jegyű PIN-t. A tablet egy névtelen eszközfiókkal (laszlobiri.com/lib/v1/device.js) csak a hozzá rendelt gyerekprofilokat éri el, a bevásárlólistát és a többi oldalt nem. Kilépés: „Szülő” → PIN. Visszavonás: a szülői nézet „Visszavonás” gombja.
- A régi, belépés nélküli pontok (`gyakorlo.v1`) nem kerülnek át: az első indításkor törlődnek.
- Terv és adatbázis: a laszlobiri-com repó `docs/backend-terv.md` és `supabase/` mappája.

## Fejlesztés

- A tokenek a központi design systemből töltődnek: `https://laszlobiri.com/design-system/tokens.css`. Helyi `tokens.css` másolat nincs, és a `sw.js` előre mentett listájába sem kerül.
- Mindig a palakék (slate) téma.
- A `sw.js`-ben minden kiadásnál emeld a gyorsítótár verzióját (`gyakorlo-vN`). A service worker a Supabase-kéréseket és a belépőoldalt nem kezeli és nem menti el.
- Új feladattípus: a `GEN` objektumba egy generátor (`prompt`, `text`, `choices`, `correct`, `explain`, opcionálisan `key` a körön belüli ismétlés kizárására), és egy sor a `TOPICS` listába. A környezetismereti tartalom adatai a `GR` (állatcsoportok), `FACTS` és `CLUES` objektumokban vannak.
- A feladatgenerátorokat külön ellenőriztem: témánként 3000 generált kérdésre a helyes válasz egyezik a kiszámolt értékkel, és a válaszlehetőségek egyediek.

## Publikálás

GitHub Pages (`main` / root), egyéni domain: `gyakorlas.laszlobiri.com` (a `CNAME` fájl tartalmazza).
DNS: `CNAME` rekord, host `gyakorlas`, érték `lbiri84.github.io`.
