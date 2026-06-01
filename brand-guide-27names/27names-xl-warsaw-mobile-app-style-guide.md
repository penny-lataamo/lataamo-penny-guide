# 27 Names XL Warsaw — tapahtumasovelluksen tyyliohje

Tämä ohje on tarkoitettu sovelluksen kehittäjälle, joka tekee XL Warsaw -tapahtumaan 27 Names -tyyliset visuaaliset muokkaukset olemassa olevaan mobiili-/tapahtumasovellukseen.

Referenssitemplate: https://penny-lataamo.github.io/lataamo-penny-guide/brand-guide-27names/

## 1. Tavoite

Tee tapahtumasovelluksesta 27 Names XL Warsaw -tapahtumaan sopiva erikoisversio ilman, että sovelluksen käytettävyys tai perusrakenne muuttuu.

Tyyli on:

- rohkea mutta selkeä
- tapahtumamainen / premium / kansainvälinen
- siniseen tapahtuma-atmosfääriin nojaava
- magenta/plum-vetoinen toimintojen ja korostusten osalta
- pehmeästi pyöristetty, moderni mobiili-UI

Älä tee sovelluksesta liian koristeellista. Brändivärien tehtävä on ohjata käyttäjää, ei täyttää jokaista pintaa.

## 2. Pääväripaletti

Käytä näitä värejä sovelluksen tapahtumakohtaisina design tokeneina.

| Token | Hex | Käyttö |
|---|---:|---|
| `xl-plum` | `#6F0B69` | pääasiallinen tumma brändisävy, primary action, aktiiviset tilat, otsikkokorostukset |
| `xl-magenta` | `#E10F78` | CTA:t, aktiiviset badget, charttien päädata, tärkeät nostot |
| `xl-pink` | `#FF7CBE` | pehmeät highlightit, hoverit, gradientin valopisteet, secondary visual accents |
| `xl-blue` | `#3258D4` | XL Warsaw -tapahtuman lavamainen / atmosfäärinen sininen, isot heropinnat ja taustat |
| `xl-ink` | `#111139` | tumma teksti-/korttipohja, hero-cardit, bottom FAB, dark surfaces |
| `xl-white` | `#FFFFFF` | kortit, tekstikontrasti tummilla pinnoilla |
| `xl-bg-warm` | `#F5F1ED` | vaalea yleistausta, jos appissa tarvitaan neutraalia taustaa |
| `xl-soft-pink` | `#FFF0F8` | vaaleat ikonitaustat, input-pintojen korostus, empty state |
| `xl-line` | `#E8E0E4` | reunukset ja dividerit vaaleassa moodissa |

### CSS-tokenit

```css
:root {
  --xl-plum: #6F0B69;
  --xl-magenta: #E10F78;
  --xl-pink: #FF7CBE;
  --xl-blue: #3258D4;
  --xl-ink: #111139;

  --xl-gradient: linear-gradient(
    135deg,
    #6F0B69 0%,
    #E10F78 39%,
    #FF7CBE 67%,
    #3258D4 100%
  );

  --xl-bg: #F5F1ED;
  --xl-surface: #FFFFFF;
  --xl-surface-soft: #FFF0F8;
  --xl-line: #E8E0E4;
  --xl-muted: #6B6167;
}
```

## 3. Värien käyttölogiikka

### Ensisijaiset toimintoelementit

Käytä gradienttia tai plum/magenta-väriä näissä:

- pää-CTA: “Enter event app”, “Save session”, “Share route”
- aktiivinen tab / valittu tila
- aktiivinen bottom navigation -ikoni
- tärkeä status-badge
- progressin täyttö
- charttien tärkein datasarja

Suositus:

```css
.button-primary {
  background: var(--xl-gradient);
  color: #fff;
  border: 0;
}
```

### Isot tapahtumapinnat

Käytä `xl-blue`-väriä isoihin tapahtumallisiin pintoihin:

- event hero
- “Warsaw moments” / venue / city -kortit
- kirjautumis- tai onboarding-näkymän taustakorostus
- tapahtumakohtaiset bannerit

Älä käytä sinistä jokaisessa napissa. Sininen on enemmän tapahtuma-atmosfääri kuin normaali UI action color.

### Vaaleat käyttöliittymäpinnat

Perusnäkymissä käytetään rauhallisia pintoja:

```css
.app-screen {
  background: #F5F1ED;
}

.card,
.input,
.list-item {
  background: #FFFFFF;
  border: 1px solid #E8E0E4;
}
```

### Dark mode / tummat pinnat

Jos sovelluksessa on dark mode tai tumma event landing -näkymä:

```css
[data-theme="dark"] {
  --xl-bg: #100E11;
  --xl-surface: #19161A;
  --xl-surface-soft: #291024;
  --xl-ink: #F8F3F6;
  --xl-muted: #C9BDC4;
  --xl-line: rgba(255,255,255,.12);
  --xl-action: #E10F78;
  --xl-action-hover: #FF7CBE;
}
```

Tummalla pohjalla magenta toimii pääactionina paremmin kuin plum, koska plum voi jäädä liian matalakontrastiseksi.

## 4. Typografia

Käytä modernia system-sansia. Template käyttää tätä font stackia:

```css
font-family: Inter, Montserrat, ui-sans-serif, system-ui, -apple-system,
  BlinkMacSystemFont, "Segoe UI", sans-serif;
```

### Painot ja hierarkia

- isot otsikot: `font-weight: 850–950`, tiukka kirjainväli
- korttiotsikot: `font-weight: 850–900`
- body copy: `font-weight: 500–650`
- labelit ja badge-tekstit: uppercase, pieni koko, vahva paino

Esimerkki:

```css
.screen-title {
  font-size: 30px;
  line-height: 1.05;
  letter-spacing: -0.055em;
  font-weight: 900;
}

.label,
.badge {
  font-size: 12px;
  font-weight: 850;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
```

## 5. Muodot, radiukset ja varjot

27 Names XL Warsaw -tyylissä UI on pehmeä, mutta ei “leikkisä”. Käytä reiluja radiuksia korteissa ja puhelinmaisissa elementeissä.

| Elementti | Radius |
|---|---:|
| app/screen shell | `28–34px` |
| isot kortit | `20–24px` |
| pienet kortit / list itemit | `16–18px` |
| inputit | `18–22px` |
| badge / pill / CTA capsule | `999px` |
| avatar | `50%` |

Varjot saavat olla pehmeitä ja hieman värillisiä:

```css
.card-elevated {
  box-shadow: 0 16px 38px rgba(17, 17, 17, 0.10);
}

.phone-preview {
  box-shadow:
    0 34px 80px rgba(17, 17, 17, 0.20),
    0 10px 28px rgba(55, 16, 75, 0.14);
}
```

## 6. App-näkymien soveltaminen

### 6.1 Login / onboarding

Käytä selkeää, premium-henkistä kirjautumisnäkymää.

- logo / event mark yläosaan
- otsikko: “Your XL Warsaw experience starts here” tms.
- inputit valkoisina/vaaleina kortteina
- pääpainike gradientilla
- social/email vaihtoehdot neutraaleina valkoisina listapainikkeina

```css
.login-button {
  min-height: 56px;
  border-radius: 19px;
  background: var(--xl-gradient);
  color: #fff;
  font-weight: 900;
}
```

### 6.2 Home / dashboard

Dashboardin pitäisi tuntua tapahtuman omalta näkymältä, ei geneeriseltä hallintapaneelilta.

Käytä sisältöteemoja kuten:

- Inspiration track
- Warsaw moments
- Next up
- My route
- Meetings
- Venue / city / after-hours

Pääkortti voi olla tumma:

```css
.hero-event-card {
  background:
    radial-gradient(circle at 76% 24%, rgba(255, 124, 190, .40), transparent 24%),
    #111139;
  color: #fff;
  border-radius: 24px;
}
```

### 6.3 Profile / event pass

Profiilin voi käsitellä tapahtumapassina.

Sisällöt:

- käyttäjä / delegate
- event access code
- country/location: Warsaw
- concierge/helpdesk
- omat sessiot / tallennetut kiinnostukset

Käytä avatarissa tai event pass -symbolissa gradienttia.

### 6.4 Bottom navigation

Bottom navin tulee olla hillitty. Aktiivinen ikoni/labeli käyttää plum/magenta-väriä.

```css
.bottom-nav-item {
  color: #C9C1C6;
}

.bottom-nav-item.active {
  color: var(--xl-plum);
}
```

Tummassa moodissa aktiivinen voi olla `#E10F78`.

## 7. Komponenttikohtaiset ohjeet

### Napit

Primary:

```css
.button-primary {
  background: var(--xl-gradient);
  color: #fff;
  border: 0;
  border-radius: 999px;
  font-weight: 850;
}
```

Secondary:

```css
.button-secondary {
  background: #fff;
  color: #111139;
  border: 1px solid #E8E0E4;
  border-radius: 999px;
}
```

Ghost:

```css
.button-ghost {
  background: transparent;
  color: var(--xl-plum);
  border: 0;
}
```

### Badget

```css
.badge-primary {
  background: var(--xl-gradient);
  color: #fff;
}

.badge-ready {
  background: #FFF0F8;
  color: #6F0B69;
}

.badge-review {
  background: rgba(50, 88, 212, .10);
  color: #3258D4;
}
```

### Kortit

```css
.card {
  background: #fff;
  border: 1px solid #E8E0E4;
  border-radius: 20px;
  box-shadow: 0 10px 24px rgba(17, 17, 17, .05);
}

.highlight-card-magenta {
  background: linear-gradient(135deg, #6F0B69, #E10F78);
  color: #fff;
}

.highlight-card-blue {
  background: linear-gradient(135deg, #3258D4, #6C8BFF);
  color: #fff;
}
```

### Inputit

```css
.input {
  min-height: 56px;
  padding: 0 18px;
  border-radius: 20px;
  border: 1.5px solid #E8E0E4;
  background: #fff;
  color: #111111;
}

.input:focus {
  border-color: var(--xl-plum);
  box-shadow: 0 0 0 4px rgba(111, 11, 105, .12);
  outline: none;
}
```

### List itemit

```css
.list-item {
  min-height: 64px;
  padding: 12px;
  border-radius: 18px;
  background: #fff;
  border: 1px solid #E8E0E4;
}

.list-icon {
  width: 42px;
  height: 42px;
  border-radius: 14px;
  background: #FFF0F8;
  color: #6F0B69;
}
```

### Chartit ja datavisualisointi

- päädatasarja: `#E10F78`
- vertailu / toinen datasarja: `#FF7CBE` tai `#3258D4`
- gridit: matalakontrastiset harmaat/linjat
- älä käytä liikaa eri värejä samassa chartissa

```css
.chart-primary {
  stroke: #E10F78;
}

.chart-secondary {
  stroke: #FF7CBE;
}

.chart-support {
  stroke: #3258D4;
}
```

## 8. Kuvien ja brändiassetien käyttö

Käytä 27 Names -merkkiä pienissä brändipisteissä:

- top bar / app header
- login-näkymä
- loader
- event pass / avatar placeholder

Älä täytä jokaista korttia logolla. Logo toimii paremmin, kun se näkyy harvoissa mutta selkeissä paikoissa.

Jos käytössä on XL Warsaw -bannerikuva, käytä sitä:

- event landing / welcome -kortissa
- onboardingissa
- tapahtuman “about / info” -näkymässä

Pidä bannerin ympärillä reilu border radius ja pehmeä varjo.

```css
.event-banner {
  border-radius: 24px;
  overflow: hidden;
  border: 1px solid rgba(255, 124, 190, .38);
  box-shadow:
    0 22px 48px rgba(50, 88, 212, .16),
    0 16px 38px rgba(225, 15, 120, .12);
}
```

## 9. Sisältö- ja label-ohjeet

Tapahtumakohtainen käyttöliittymä saa tuntua henkilökohtaiselta ja tapahtuman omalta.

Suositeltuja termejä:

- “XL Warsaw”
- “Inspiration track”
- “Warsaw moments”
- “My route”
- “Next up”
- “Meetings”
- “Venue”
- “Concierge”
- “Event pass”
- “Access code”

Vältä geneerisiä hallintatermejä, jos tapahtumatermi on mahdollinen:

| Geneerinen | Parempi XL Warsaw -kontekstissa |
|---|---|
| Report | Route / session / highlight |
| User profile | Event pass / delegate profile |
| Dashboard | My XL Warsaw / Today |
| Notification | Next up / action needed |
| Support | Concierge |

## 10. Accessibility ja kontrasti

Pakolliset tarkistukset:

- valkoisen tekstin kontrasti gradientti- ja sinipinnoilla riittävä
- pienet badge-tekstit vähintään 11–12 px ja vahva font weight
- focus state näkyy kaikissa napeissa, inputeissa ja valinnoissa
- väri ei saa olla ainoa statuksen ilmaisin: käytä myös tekstiä/ikonia
- dark mode -näkymässä plum ei yksin riitä action-väriksi; käytä magentaa/pinkkiä

Focus-esimerkki:

```css
:focus-visible {
  outline: 4px solid rgba(225, 15, 120, .24);
  outline-offset: 3px;
}
```

## 11. Mobiilikäytettävyys

Tämä tyyli on ensisijaisesti mobiilisovellusta varten. Tarkista ainakin 390 px leveydellä.

Säännöt:

- älä tee top barista liian korkeaa
- pidä pää-CTA peukaloystävällisenä: min. 44–48 px korkeus
- älä käytä vaakaskrollia tavallisissa listoissa tai taulukoissa
- listat korttimaisiksi kapealla ruudulla
- hero-kuva tai banneri ei saa viedä koko ensimmäistä näkymää
- bottom navissa max 4–5 päätasoa

## 12. Nopea toteutuslista devaajalle

1. Lisää tapahtumakohtaiset CSS-tokenit `xl-*`-prefiksillä.
2. Vaihda sovelluksen primary/action-värit `#6F0B69` / `#E10F78` -linjaan.
3. Lisää gradientti vain pää-CTA:hin, aktiivisiin elementteihin ja tärkeimpiin korostuksiin.
4. Käytä `#3258D4`-sinistä event heroissa, bannerikorteissa ja Warsaw/city/venue-momenteissa.
5. Päivitä login/onboarding, dashboard ja event pass/profile -näkymät tapahtumakielelle.
6. Lisää 27 Names -merkki top bariin, login-näkymään ja loaderiin, ei jokaiseen korttiin.
7. Tarkista kontrasti, focus state ja 390 px mobiilinäkymä.
8. Varmista, että peruskomponentit säilyvät: napit, inputit, tabit, listat, kortit, chartit, empty state, modal, loader ja bottom nav.

## 13. Minimi-CSS, jos muutokset tehdään nopeasti olemassa olevaan appiin

```css
:root {
  --event-primary: #6F0B69;
  --event-primary-strong: #E10F78;
  --event-accent: #FF7CBE;
  --event-blue: #3258D4;
  --event-ink: #111139;
  --event-soft: #FFF0F8;
  --event-gradient: linear-gradient(135deg, #6F0B69 0%, #E10F78 39%, #FF7CBE 67%, #3258D4 100%);
}

.event-xl-warsaw .button-primary,
.event-xl-warsaw .cta-primary {
  background: var(--event-gradient);
  color: #fff;
  border: 0;
}

.event-xl-warsaw .active,
.event-xl-warsaw .bottom-nav-item.active {
  color: var(--event-primary);
}

.event-xl-warsaw .event-card-dark {
  background: var(--event-ink);
  color: #fff;
}

.event-xl-warsaw .event-card-blue {
  background: linear-gradient(135deg, #3258D4, #6C8BFF);
  color: #fff;
}

.event-xl-warsaw .badge,
.event-xl-warsaw .list-icon {
  background: var(--event-soft);
  color: var(--event-primary);
}

.event-xl-warsaw input:focus,
.event-xl-warsaw select:focus,
.event-xl-warsaw textarea:focus {
  border-color: var(--event-primary);
  box-shadow: 0 0 0 4px rgba(111, 11, 105, .12);
  outline: none;
}
```

## 14. Laadunvarmistus ennen julkaisua

Hyväksy muutos vasta kun nämä täyttyvät:

- [ ] Sovelluksen tärkeimmät näkymät näyttävät XL Warsaw -tapahtuman omilta, eivät geneeriseltä appilta.
- [ ] Primary CTA erottuu selvästi.
- [ ] Tekstit ovat luettavia sekä vaaleilla että tummilla pinnoilla.
- [ ] Bottom navigation toimii ilman visuaalista ylikuormaa.
- [ ] Logo/merkki näkyy selkeästi mutta ei toistu liikaa.
- [ ] 390 px mobiilinäkymässä ei ole rikkinäisiä leveys-, skrolli- tai header-ongelmia.
- [ ] Kaikki interaktiiviset elementit ovat vähintään 44 px korkeita tai muuten helposti painettavia.

---

Lähdereferenssi: Lataamon 27 Names XL Warsaw mobile template  
https://penny-lataamo.github.io/lataamo-penny-guide/brand-guide-27names/
