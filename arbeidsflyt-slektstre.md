# Arbeidsflyt — slektstreet

Kort oppskrift for å halde ved like det interaktive slektstreet. Skriven for meg sjølv,
så eg ikkje treng hugse alt utanåt.

---

## Kva prosjektet er

Eit interaktivt slektstre (oversynsvifte) som ligg på GitHub Pages. Det består av
**fire ting** i same repositorium:

| Fil / mappe | Rolle |
|---|---|
| `slektstre.html` | Visninga (vifta, søket, panelet). Rører eg nesten aldri. |
| `slektstre-data.json` | **All data**: personar, kjelder, forteljingar, bilet-lister. Det er her eg redigerer innhald. |
| `kjeldegrunnlag-slektstre.md` | Den forteljande kjeldekritikken — kvifor ein plass er gul, kva som er prøvd. |
| `bileteslekt/` | Mappe med alle bilet-filene. |

Prinsippet: **data (JSON) er skilt frå visning (HTML).** Eg endrar innhald i JSON-en;
HTML-en les frå henne. Eit feil komma i JSON-en øydelegg ikkje sida — nettlesaren seier
ifrå, i staden for at treet forsvinn.

---

## Lenka til treet

`https://BRUKARNAMN.github.io/slektstre/slektstre.html`

(Fila heiter `slektstre.html`, ikkje `index.html`, difor må `/slektstre.html` stå bak.
Vil eg ha rein lenke, kan eg døype fila om til `index.html` i repoet — men det hastar ikkje.)

---

## Kjeldekritikk-fargane (det viktigaste prinsippet)

- **Grøn** = dokumentert i primærkjelde (direkte belegg).
- **Lilla** = opplyst av familien.
- **Gul** = sannsynleg / sekundærspor, ikkje endeleg prova.
- **Grå** = open / ukjend.

Regel: **heller ei tom rute enn feil person.** Set aldri grøn utan direkte primærkjelde.

---

## Slik legg eg til bilete på ein person

1. **Klargjer biletet.** Helst maks ~1600 px breitt, komprimert til nokre hundre kB.
   (Kan gjere det sjølv, eller be Claude om det ved å laste opp originalen.)
2. **Last biletet opp i `bileteslekt`-mappa på GitHub:** inn i repoet → klikk mappa
   `bileteslekt` → **Add file → Upload files** → dra fila inn → **Commit changes**.
3. **Legg biletet til i JSON-en.** Kvar person har ei liste under `media`. Opna
   `slektstre-data.json` → blyant (**Edit**) → finn personen sin ID → legg til eit objekt
   i lista. Døme (person 2, Agnar):

   ```json
   "2": [
    { "type": "image", "src": "bileteslekt/person-2.jpg",     "cap": "Agnar på Store Skagastølstind." },
    { "type": "image", "src": "bileteslekt/agnar-fjelltur.jpg", "cap": "Agnar på fjelltur." }
   ]
   ```
   Rekkjefølgja i lista = rekkjefølgja ein blar i. Hugs komma mellom objekta.
4. **Commit changes** (heilt nedst — lett å gløyme).

## Slik legg eg til video (same mønster)

Lag ei mappe `video` i repoet, last opp filmfila (helst kort `.mp4`), og legg til:
```json
{ "type": "video", "src": "video/agnar-intervju.mp4", "cap": "Intervju, 1999." }
```
Kan òg ha `"poster": "bileteslekt/…jpg"` for stillbilete før avspeling.
NB: film er tungt. Korte klipp går fint; lange intervju bør heller liggje på ei
videoteneste og lenkjast til.

## Slik endrar eg tekst på ein person

Opna `slektstre-data.json` → blyant → finn personen → endra `notes`, `place`, `work`,
eller `cap` → **Commit changes**.

---

## Når noko ikkje viser (feilsøking)

**Endringa vises ikkje etter oppdatering:** det er nesten alltid mellomlagring.
- Hard oppdatering: **Ctrl+Shift+R**.
- Eller opna sida i **inkognito-vindauge** (Ctrl+Shift+N) — ingen buffer der.
- Eller vent 5–10 min; GitHub brukar litt tid på å publisere.

**Sjekk kva sida faktisk les:** opna
`https://BRUKARNAMN.github.io/slektstre/slektstre-data.json` og søk (Ctrl+F) etter det
nye. Får eg treff, er JSON-en rett, og det står berre på buffer.

**Bilete er tomt:** då stemmer ikkje filnamnet.
- Sjekk at fila i `bileteslekt` heiter *nøyaktig* det same som `src` i JSON-en.
- Vanleg felle: nedlasting la til «(1)» i namnet — `agnar-hav (1).jpg` ≠ `agnar-hav.jpg`.
- Store/små bokstavar tel på GitHub.

**«(1)» bak filnamn:** kjem av at nettlesaren la til tal fordi fila alt låg i
Nedlastingar. Rydd i Nedlastingar-mappa, eller døyp om fila i repoet.

---

## Redigere JSON utan krøll

Enklaste veg (unngår nedlasting-krøll): rediger **direkte i GitHub** — opna fila →
blyant (**Edit**) → gjer endringa → **Commit changes**.

Skal eg lime inn ein heilt ny versjon: opna den nye fila i Notisblokk (høgreklikk →
Opne med → Notisblokk), Ctrl+A, Ctrl+C. Så i GitHub: blyant → Ctrl+A → slett → Ctrl+V →
Commit.

---

## Arbeidsdeling med Claude

- Eg kan laste opp bilete i samtalen; Claude klargjer dei (storleik, retning) og skriv
  dei ferdige `media`-oppføringane, og gir meg filene + oppdatert JSON tilbake.
- Claude kan **ikkje** laste opp til GitHub for meg — det steget gjer eg alltid sjølv.
- Ved mange bilete på ein gong: be Claude samle dei i éi **zip-fil**, så slepp eg å
  laste opp fil for fil.

---

## Personvern — hugse dette

Repoet er **offentleg**. Alt der kan kven som helst lese, inkludert JSON-en med alle
notata. For eldre ledd er det uproblematisk. Men når eg legg inn foto eller intervju med
**levande** slektningar, er offentleg publisering ei sjølvstendig avgjerd:
- gjere repoet privat, eller
- skilje eit ope «historisk» tre frå eit privat «levande» eitt.
Tenk gjennom dette *før* eg legg inn levande folk, ikkje etter.
