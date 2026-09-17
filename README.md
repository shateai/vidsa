# 🎬 Vidsa — Playbook pro tvorbu krátkých videí

> **Repo dokumentuje, JAK tvoříme krátká vertikální videa** (YouTube Shorts / Instagram Reels / TikTok).
> Je to náš společný manuál: písemný sourcem of truth, ke kterému se vždy vrátíme.

**Kdo je kdo:**
- 👤 **Šéf projektu** (člověk) — zadává témata, schvaluje scénáře a finální videa, publikuje.
- 🤖 **AI agent** — research, scénáře, voiceover, vizuály, střih, titulky, export. Postupně buduje i plnou automatizaci (viz [Roadmapa](#-roadmapa-automatizace)).

---

## 🧭 Jak spolu pracujeme (základní smyčka)

```
1. ZADÁNÍ      →  šéf pošle téma / nápad / odkaz
2. RESEARCH    →  agent zjistí, co o tématu lidi zajímá
3. SCENÁŘ      →  agent navrhne hook + scénář (podle šablony níže)
4. SCHVÁLENÍ   →  šéf okomentuje / upraví / schválí ✅
5. VÝROBA      →  agent: vizuály + hlas + titulky + střih
6. KONTROLA    →  checklist před exportem (níže)
7. EXPORT      →  finální MP4 dle specifikace výstupu
8. PUBLIKACE   →  šéf publikuje, agent doporučí popisek + hashtagy
9. ANALÝZA     →  po 48–72 h: co říkají data? co uděláme jinak?
```

> 🔁 Krok 9 krmí krok 1. Učíme se z každého videa — retence a komentáře říkají, jaké hooky a témata fungují.

### ⭐ Zlaté pravidlo review smyčky

**Na stole je vždy JEN JEDNA animace.** Agent představí jednu krátkou animaci (~5 s) a počká. Šéf pak říká:
- **„zlepši X"** → agent upraví, převede, ukáže znovu (dokud není ✓)
- **„další"** → animace schválena, archivuje se a agent staví další segment

Žádné hromady variant dopředu. Iterujeme na jednom kusu, dokud není prémium.

---

## 📐 Specifikace výstupu

| Parametr | Hodnota |
|---|---|
| Rozlišení | **1080 × 1920** (9:16, vertikální) |
| FPS | 30 (60 jen u akčních/dynamických záběrů) |
| Kodek | H.264 (video) + AAC (audio, 192 kbps) |
| Délka | **25–40 s** ideál, max 60 s |
| Titulky | **Vždy** vypálené do obrazu (≈ 85 % lidí sleduje bez zvuku) |
| Bezpečné zóny | Text nikdy do horních ~12 % a dolních ~18 % obrazu (překrývá ho UI TikToku/Shorts) |

```
┌─────────────────┐
│  ⚠️ horních 12 % │ ← username / UI platformy
│                 │
│   HLAVNÍ TEXT   │ ← sem patří titulky a klíčové prvky
│      TADY       │
│                 │
│ dolních 18 % ⚠️ │ ← popisek, tlačítka, hudba
└─────────────────┘
```

---

## 🧱 Anatomie krátkého videa

| Segment | Čas | Účel | Pravidlo |
|---|---|---|---|
| 🪝 **Hook** | 0–2 s | Zastavit scroll | První věta MUSÍ vytvořit napětí, otázku nebo šok. Žádné „ahoj, v dnešním videu…" |
| 💎 **Value** | 2–35 s | Doručit obsah | 3–5 krátkých vět. Každá 1–2 s změna záběru. Jedna myšlenka = jedna věta |
| 🎯 **CTA / Loop** | poslední 2–3 s | Akce nebo sledování dál | Buď výzva („sleduj pro část 2"), nebo věta, která hladce naváže na začátek (loop = víc zobrazení) |

### Typy hooků, které používáme
1. **Otázka** — „Víš, proč 90 % lidí dělá X špatně?"
2. **Šok / číslo** — „Tuhle chybu dělá 8 z 10 lidí každý den."
3. **Negace** — „Přestaň dělat X. Hned."
4. **Příslib** — „Za 30 sekund se naučíš, jak X."
5. **Curiosity gap** — „Nikdo ti neřekne, že za X stojí tohle…"

### Pravidla scénáře
- ✅ Píšeme, jak se mluví (mluvená čeština, krátké věty do 12 slov)
- ✅ Aktivní slovesa, konkrétní příklady, čísla
- ❌ Žádné úvody, oslovení, zdvořilosti, marketingové fráze
- ⏱️ Tempo čtení: **~2,3–2,7 slova/sekundu** (35 s videa ≈ 85–95 slov)

---

## ✍️ Šablona scénáře

Každý scénář vzniká v této tabulce (ukládá se do `videos/RRRR-MM-DD-nazev/scenar.md`):

| # | Čas | Voiceover (co se říká) | On-screen text (titulek) | Vizuál (co je vidět) |
|---|---|---|---|---|
| 1 | 0–2 s | „Přestaň srát čas X…" | PŘESTAŇ DĚLAT X | Rychlý zoom na překvapivý vizuál |
| 2 | 2–8 s | … | … | … |
| 3 | 8–15 s | … | … | … |
| 4 | 15–25 s | … | … | … |
| 5 | 25–35 s | „…a proto X. Sleduj pro víc." | SLEDUJ PRO ČÁST 2 | Logo / CTA obrazovka |

> Pravidlo: **On-screen text ≠ diktování.** Titulek je zkratka nebo důraz, ne opis voiceoveru.

---

## 🎙️ Krok: Voiceover (TTS)

- Stabilní **jeden hlas pro celý kanál** = rozpoznatelnost (volíme jednou, měníme jen výjimečně).
- Přirozené pauzy mezi větami (0,2–0,4 s), u hooku důraznější intonace.
- Vygenerovaný audio uložíme jako `voice.mp3` do složky videa.

## 🖼️ Krok: Vizuál

- **Každých 1–2 s změna záběru** — statický záběr déle než 3 s = únik diváků.
- Mix zdrojů: b-roll, AI-generované obrázky, motion grafika, velké textové karty.
- Konzistentní barevnost a fonty celého kanálu (viz Style guide níže).

## 💬 Krok: Titulky

- 1–3 slova na řádek, **bold, vysoký kontrast**, stín/obrys pro čitelnost.
- Pozice: střed, ~60–70 % výšky obrazu (v bezpečné zóně).
- Synchronizace slovo-od-slova nebo bloky po 1–3 slovech.

## 🎞️ Krok: Střih & export

Referenční exportní příkaz (náš standard):

```bash
ffmpeg -framerate 30 -i frames/%04d.png -i voice.mp3 \
  -vf "scale=1080:1920" \
  -c:v libx264 -pix_fmt yuv420p -crf 18 -r 30 \
  -c:a aac -b:a 192k -shortest \
  output.mp4
```

## 🚀 Krok: Publikace

| Prvek | Pravidlo |
|---|---|
| Popisek | 1–2 věty, otázka na konci zvyšuje komentáře |
| Hashtagy | 3–5: mix 1–2 velkých + 2–3 niche relevantních |
| Pořadí platform | TikTok → Reels → Shorts |
| Timing | 2× týdně minimum; ideál fixní dny a časy |
| Cover | Vždy nastavit ručně — velký text, čitelný v malém náhledu |

---

## ✅ Checklisty

### Před exportem
- [ ] Hook v prvních 2 s je silný a slyšitelný hned od 0:00
- [ ] Žádný text v horních 12 % / dolních 18 % obrazu
- [ ] Titulky čitelné i na malém displeji (test na telefonu)
- [ ] Zvuk čistý, hlas bez šumu, hlasitost vyrovnaná
- [ ] Délka 25–40 s
- [ ] Konec buď loopuje, nebo má CTA

### Před publikací
- [ ] Název souboru: `RRRR-MM-DD-nazev.mp4` (bez diakritiky)
- [ ] Popisek + hashtagy připraveny
- [ ] Cover nastaven
- [ ] Video zkontrolováno celé na telefonu

---

## 🎨 Style guide (výchozí)

- **Fonty:** 1 bold sans-serif pro titulky (např. Montserrat ExtraBold / Inter Black), nic jiného
- **Barvy:** max 3 — tmavé pozadí, bílá text, 1 akcentní barva pro důrazy
- **Tón:** přímý, energický, žádné vykecávání; mluvíme k jednomu divákovi („ty")

---

## 🏭 Výrobní pipeline: HyperFrames

Videa skládáme z **předpřipravených segmentů** — každý segment je samostatná [HyperFrames](https://github.com/heygen-com/hyperframes) kompozice (HTML + GSAP), která se renderuje do MP4 deterministicky, snímek po snímku. Stejný vstup = identický výstup.

### Proč tenhle model

- 🎨 **Vždy stejný styl** — segmenty sdílí paletu, fonty a motion jazyk, takže výsledek vypadá konzistentně
- 🧩 **Kombinovatelnost** — segmenty na sebe navazují čistými cuty (whip-out → cut), takže je můžeme řadit jako lego
- 🤖 **Agent-friendly** — kompozice je HTML; agent umí segment vytvořit, zvalidovat i vyrenderovat sám
- 🔁 **Opakovatelnost** — `npm run check` (lint + runtime + layout + motion + kontrast) před každým renderem

### Struktura repa

```
vidsa/
├── README.md                        ← tento playbook (zdroj pravdy)
└── pipeline/
    ├── package.json                 ← HyperFrames tooling (Node 22+, FFmpeg)
    └── goat-start-v1/               ← SEGMENT #1: Hook start (5,5 s) ✅
        ├── index.html               ← kompozice (HTML + GSAP timeline)
        ├── assets/
        │   ├── fonts/               ← Anton + Archivo (plná čeština)
        │   ├── sfx/                 ← zvuková knihovna (syntetizovaná)
        │   └── gsap.min.js
        ├── preview/goat-start-v1.mp4← vyrenderovaný náhled
        └── README.md                ← dokumentace segmentu (beat mapa, pravidla)
```

### Knihovna segmentů

| Segment | Délka | Účel | Stav |
|---|---|---|---|
| `goat-start-v1` | 5,5 s | Hook: dopad → MESSI slam → GOAT? pečeť → taktika → payoff → whip-out | ✅ hotovo |
| `stat-compare` | — | Srovnání dvou hráčů side-by-side (statistiky) | 🔜 navrženo |
| `proof-reveal` | — | Rozkrytí důkazu č. N (velké číslo + fakt) | 🔜 navrženo |
| `quote-card` | — | Citát / výrok s kinetickou typografií | 🔜 navrženo |
| `rank-reveal` | — | Odhalení pořadí (countdown 5→1) | 🔜 navrženo |
| `outro-follow` | — | CTA konec: follow + náhled dalšího dílu | 🔜 navrženo |

### Prostředí (poznámky pro agenty)

- Node 22+ a FFmpeg jsou potřeba pro render; `npx hyperframes render` stáhne headless Chrome sám
- V sandboxu: renderovat s `TMPDIR` ve workspace a `--frames-cache-dir=off` (malý `/tmp`)
- Detailní pravidla psaní kompozic: `pipeline/goat-start-v1/README.md` → „Pravidla pro nové segmenty"

---

## 🗺️ Roadmapa automatizace

| Fáze | Co | Stav |
|---|---|---|
| **0** | Playbook + proces (toto repo) | ✅ hotovo |
| **1** | HyperFrames pipeline + knihovna segmentů, první videa „na půl automat" | 🔄 **probíhá** — 1/6 segmentů hotovo |
| **2** | Celé video jedním příkazem: scénář → segmenty → TTS → MP4 | 🔜 |
| **3** | Auto-titulky (whisper), knihovna b-rollu, batch rendering | 🔜 |
| **4** | Plná automatizace: nápady → videa v limitu, scheduler, analýza výkonu | 🔮 |

---

## 🤝 Pravidla pro tohle repo

- Agent commituje přímo do `main`, každá změna má popisný commit message.
- Nové video = nová složka ve `videos/`, nikdy nepřepisujeme stará videa.
- Změna tohoto playbooku = vždy samostatný commit, ať je vidět, jak se proces vyvíjí.

---
*Vytvořeno 2026-09-17 · lead: @shateai + AI agent · Fáze 0/4*
