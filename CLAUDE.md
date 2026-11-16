# Gyakorló: szabályok a feladatokhoz

## A tananyag forrása: a tankönyv és a munkafüzet fejezetei (2026-11-15 óta)

- A feladatok a tankönyv és a munkafüzet fejezeteihez igazodnak. Minden fejezet egy külön téma (kategória) az appban, a fejezet címével.
- Csak a két könyv szövegét és képeit használjuk: a kérdések és a magyarázatok a könyv mondatai, új tartalmat nem találunk ki. Ahol a könyv nem adja meg a megoldást (pl. „Beszéljétek meg!”), vagy egy kép többféleképpen érthető, azt a szülőnek jelezni kell, és csak egyértelmű feladat kerülhet be.
- A kérdés szövege nem árulhatja el a választ (pl. „köszöntik a nyarat” → nyáron; „dió” → diófa). Ahol a könyv képpel kérdez, és a szöveges változat így túl könnyű lenne, az a feladat kimarad.
- A rossz válaszlehetőség soha ne legyen másképp is igaz (pl. tejet a juh is ad, ezért a „tehén – tej” párnál a juh nem lehet rossz válasz).
- A forrás a szülő Google Drive-jában van: `Gyakorlás/<tantárgy>/<sorszám> - <fejezet címe> - tankönyv.pdf` és `... - munkafüzet.pdf`. A PDF-ek és a könyvek szövege tömegesen nem kerül a repóba.
- A tanmenet (`CURRICULUM`): tantárgyanként a könyv témakörei és fejezetei a tartalomjegyzék szerint (fejezetkód, név, tankönyvi oldalak, a fejezet témái). A szülő a szülői nézetben tantárgyanként bepipálja, mi legyen elérhető (`chapter_access`, a háztartásban közös); ami nincs bepipálva, az a gyereknek nem látszik, a vegyes körben sem. Új fejezet témáját mindig a `CURRICULUM` megfelelő fejezetéhez kell rendelni.
- A forráskönyvek egészben is lehetnek a Drive-on (pl. `Matematika - tankönyv - 3.pdf`); a Drive-ról legfeljebb 10 MB tölthető le, a nagyobbakból csak a felismert szöveg olvasható ki, ezért a képekhez 10 MB alatti darabok kellenek.
- Új fejezet: az adatai a közös `chapGen` készítőbe kerülnek (`KM` feleletválasztós, `KF` igaz-hamis, `KB` rögzített lehetőségek, `KP` párok mindkét irányban), és egy új sor a `TOPICS`-ba.
- Állapot: a **Környezetismeret** (11–18. fejezet) és a **Matek** 1–6. témaköre (a munkafüzet I. kötete) már így készül; a matek 7–13. témakörének feladataihoz a munkafüzet II. kötete kell. A **Nyelvtan** később kerül át ugyanerre.
- Matek: a feladattípus és a megfogalmazás a könyvből jön, a számok a fejezet számkörén belül véletlenek (a szülő jóváhagyásával). A ragozott számokhoz (pl. „37-tel”, „16-ot”, „a 63-nál”) a `Nvel`, `Nt`, `Nhoz`, `Nnal`, `Ntol`, `Nbol`, `Nan` és az `az()` segédfüggvény kell, kézzel írt rag nem.

## Írás és ellenőrzés

- A „·” csak a szorzás jele; felsorolásban és elválasztóként vessző kell.
- Minden változás előtt és után: a generált feladatok ellenőrzése témánként (a helyes válasz a lehetőségek között, nincs ismétlődő lehetőség, legfeljebb egy „?”), és a böngészős füstpróba (a `laszlobiri-com` repóban: `npm run test:smoke`).
- Kiadáskor az `APP_VERSION` (index.html) és a `CACHE` (sw.js) együtt nő.
- A gyerekekről csak becenevet és eredményt tárolunk; a gyerekek valódi neve nem kerül a repóba.
- Élesítés (merge a `main`-re) csak a szülő „mehet élesbe” jóváhagyása után.
