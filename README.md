# Gyakorló

Gyakorló oldal 3. osztályosoknak: matek, nyelvtan és környezetismeret, kérdés-felelet formában, pontokkal és jelvényekkel. Egyetlen `index.html`, build nélkül. Csak belépve használható; a pontok és jelvények a laszlobiri közös backendjébe mentődnek, gyerekprofilonként.

- **Matek (számok és műveletek 200-ig, mérések):** számok 200-ig, helyi érték, számegyenes, számszomszédok és kerekítés, összeadás-kivonás, szorzás-osztás, szöveges feladatok, mérések (tömeg, hossz), pénz és visszajáró. A feladatok generáltak, minden kör új számokkal.
- **Mini játékok:** 50 pontonként a kör végén felváltva akasztófa vagy szókereső (10×10-es tábla, 5–6 elrejtett szó) ajánlódik fel, elfogadható vagy elvethető. A szavak az anyagból valók. Siker +10 pont, az első győzelem jelvényt ad.
- **Nyelvtan:** j vagy ly?, szófajok, mondatfajták, ABC-sorrend.
- **Környezetismeret:** az élet feltételei (élő és élettelen, életfeltételek, táplálkozás), állatcsoportok vegyesen, valamint külön az emlősök, madarak, hüllők, kétéltűek és a rovarok (bogarak): testtakaró, belső vagy külső váz, testfelépítés, szaporodás, kicsinyek, fejlődés.
- **Vegyes kör:** 10 kérdés az összes témából.
- Egy kör 10 véletlenszerű kérdés, 4 (vagy 2–3) válaszlehetőséggel, azonnali visszajelzéssel és magyarázattal.
- Jutalom: 10 pont minden jó válaszért, +50 pont hibátlan körért (csak a befejezett kör számít), szintek (1–9+), napi sorozat és 11 jelvény.
- Offline működik, telepíthető a kezdőképernyőre (PWA). A gyerek tableten telepített appként használd: böngészőfülben a Safari egy hét használat nélkül törölheti a párosítást.

## Gyerekprofilok, szülői nézet, gyerek mód

- **Szülő**: Google-belépéssel (`https://laszlobiri.com/belepes/`). A kezdőképernyőn „Ki gyakorol?”: a gyerek kiválasztása; a „Szülői nézet”-ben gyerekprofil létrehozása és törlése, a gyerekek eredményei, a gyerek tabletek listája és párosítása.
- **Gyerekprofil**: csak becenév, egy ikon és egy színtéma. A gyereknek nincs fiókja.
- **Színtéma**: a gyerek maga választja a kezdőképernyőn („Színem”), a saját tabletjén is (offline is, a kimenő soron át): palakék (alap) vagy rózsaszín (`#ebcddb`, `#e6abc0`, `#d77ca2`, `#3c3737`, `#261d1b`). A téma a gyerek saját nézeteiben él (kezdőképernyő, kör, eredmény, jelvények, minijátékok), a szülő telefonján és a gyerek tabletjén is; a „Ki gyakorol?” és a szülői nézet palakék marad. A rózsaszín téma a tokenek felülírásával készül az oldal saját CSS-ében (`data-theme="rose"`), a központi `tokens.css` változatlan; a laszlobiri jel színei nem változnak.
- **Eredmények**: csak a befejezett kör és a megnyert minijáték mentődik (`results`, `pupil_badges`). A pont, a szint, a napi sorozat és a témánkénti legjobb ezekből számolódik. Offline is működik: a laszlobiri.com/lib/v1/outbox.js kimenő sorból visszatérő hálózatnál elmegy.
- **Gyerek mód** (a gyerek saját tabletje): a szülő a „Szülői nézet” → „Párosító kód kérése” gombbal 10 percig érvényes kódot kap, a tableten a `gyakorlas.laszlobiri.com/#parositas` oldalon beírja, és megad egy 4 jegyű PIN-t. A tablet egy névtelen eszközfiókkal (laszlobiri.com/lib/v1/device.js) csak a hozzá rendelt gyerekprofilokat éri el, a bevásárlólistát és a többi oldalt nem. Kilépés: „Szülő” → PIN. Visszavonás: a szülői nézet „Visszavonás” gombja.
- **Hibás feladat jelentése**: a kérdésnél a „⚑” gomb → „Rossz a megoldás” / „Hibás a kérdés” / „Más baj van”. A kérdés pillanatképe (téma, kérdés, válaszok, helyes és megjelölt válasz, magyarázat) a `question_reports` táblába kerül, szabad szöveg nélkül, offline is. A szülői nézet „Jelentett feladatok” részében látszik; „Javítva” / „Elvetés”, és „Szövegként másolás” a javításhoz (a gyerek neve nélkül). Az `APP_VERSION` a jelentésben a `sw.js` verziójával egyezzen.
- A régi, belépés nélküli pontok (`gyakorlo.v1`) nem kerülnek át: az első indításkor törlődnek.
- Terv és adatbázis: a laszlobiri-com repó `docs/backend-terv.md` és `supabase/` mappája.

## Fejlesztés

- A tokenek a központi design systemből töltődnek: `https://laszlobiri.com/design-system/tokens.css`. Helyi `tokens.css` másolat nincs, és a `sw.js` előre mentett listájába sem kerül.
- Palakék (slate) téma; a gyerek saját nézeteiben választható rózsaszín (`data-theme="rose"`, lásd fent).
- A `sw.js`-ben minden kiadásnál emeld a gyorsítótár verzióját (`gyakorlo-vN`), és vele együtt az `index.html` `APP_VERSION`-ját (ez kerül a hibajelentésekbe). A service worker a Supabase-kéréseket és a belépőoldalt nem kezeli és nem menti el.
- Új feladattípus: a `GEN` objektumba egy generátor (`prompt`, `text`, `choices`, `correct`, `explain`, opcionálisan `key` a körön belüli ismétlés kizárására), és egy sor a `TOPICS` listába. A környezetismereti tartalom adatai a `GR` (állatcsoportok), `FACTS` és `CLUES` objektumokban vannak.
- A feladatgenerátorok ellenőrzése (minden módosítás után): témánként 3000 generált kérdés; a helyes válasz a lehetőségek között van, a lehetőségek egyediek, és egy feladatban legfeljebb egy kérdőjel áll. A `window.__gyakorlo` (`GEN`, `TOPICS`, `makeQuestion`) a böngészőből elérhető ehhez.
- Tananyag bővítése: tankönyvfotók alapján, saját feladatokkal (a tankönyv szövege nem kerül a nyilvános repóba).

## Publikálás

GitHub Pages (`main` / root), egyéni domain: `gyakorlas.laszlobiri.com` (a `CNAME` fájl tartalmazza).
DNS: `CNAME` rekord, host `gyakorlas`, érték `lbiri84.github.io`.
