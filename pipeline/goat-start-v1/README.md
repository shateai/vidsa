# 🎬 Segment: `goat-start-v1` — Hook start (5,5 s)

> **První segment v naší knihovně.** Univerzální „start" pro listy typu *GOAT CHECK / PROOF / DÍL 01*.
> Stav: ✅ **hotovo, otestováno, check prošel** (`npm run check` — 0 chyb, kontrast WCAG AA).

**Preview:** `preview/goat-start-v1.mp4` (1080×1920 · 30 fps · 5,5 s · se zvukem)

---

## Beat mapa

| Čas | Co se děje | Zvuk |
|---|---|---|
| 0.00 | Pozadí in (vinětace + tečky + strižené čáry hřiště), speed-lines burst | crowd atmosféra (pod textem) |
| 0.13–0.52 | ⚽ Míč letí zleva dole do středu kompozice | riser (sweep nahoru) |
| **0.52** | 💥 **DOPAD** — flash, 2 shockwave ringy, 12 jisker, screen shake | **impact** (sub boom + crack) |
| 0.56–1.06 | **MESSI** písmena slam-in (back.out), RGB split chroma | (dohrává impact) |
| 0.78–1.16 | Badge `GOAT CHECK · DÍL 01` typewriter reveal + blikající kurzor | — |
| 1.32–1.62 | Pečeť **GOAT?** náraz (scale 2.7→1) + glow flash + mini shake | thud |
| 1.50–1.96 | 👑 Koruna padá zhora (bounce.out) | — |
| 1.96–2.30 | *Hold beat* — čtenářská pauza (retence) | — |
| 2.32–2.64 | Hero skupina slide-up, místo taktické vrstvě | — |
| 2.35–3.25 | Pasová linie se kreslí (dashoffset) + svítící dot letí po křivce | — |
| 2.45 / 2.70 / 2.95 | Chipsy popují: **8× Zlatý míč · 850+ gólů · 45+ trofejí** | 3× tick (rytmus) |
| 3.55–3.85 | Exit wipe: hero odletí vlevo, taktika scale-out | — |
| **3.82–4.72** | 🎯 **Payoff:** „**5** DŮKAZŮ." + „45 SEKUND" + zlatá linka | pop (boom) |
| 4.95–5.29 | Whip-out: blur + slide + flash → **čistý cut pro další segment** | whip + impact (soft) |

## Proč to funguje (respektuje náš playbook)

- **Hook do 2 s:** míč letí v 0.13, dopad v 0.52, MESSI slam dokončen v ~1.1 s
- **Změna záběru každou 1–2 s:** 5 fází za 5,5 s (dopad → badge → pečeť → taktika → payoff)
- **Bezpečné zóny:** žádný text v horních 12 % / dolních 18 %
- **Loop-ready:** whip-out na konci = čistý cut k dalšímu segmentu

## Specifikace

| Parametr | Hodnota |
|---|---|
| Rozlišení | 1080×1920 (9:16) |
| FPS | 30 |
| Délka | 5,5 s (timeline locked přes `tl.set({}, {}, 5.5)`) |
| Fonty | Anton (display) + Archivo Variable (support) — `assets/fonts/` |
| Paleta | pozadí `#060a08` → `#0d2417`, limetka `#c6ff4a`, zlatá `#ffc93c`, bílá `#f8fff2` |

## Zvuková knihovna (syntetizovaná, `assets/sfx/`)

| Soubor | Charakter | Použití v segmentu |
|---|---|---|
| `riser.wav` (0.45 s) | noise sweep 400→3800 Hz | přílet míče |
| `impact.wav` (0.9 s) | sub boom + noise crack | dopad míče, konec whip-outu |
| `thud.wav` (0.3 s) | krátký tlumený úder | náraz pečeti |
| `tick.wav` (0.12 s) | vysoký klik | rytmus chipsů |
| `pop.wav` (0.5 s) | payoff boom | payoff text |
| `whip.wav` (0.35 s) | sweep dolů | whip-out přechod |
| `crowd.wav` (6 s) | Stadium air (lowpass šum + AM) | podtext celého segmentu |

> Všechny SFX jsou deterministicky syntetizované (numpy, seed) — žádné autorské práva, můžeme je sdílet mezi všemi segmenty.

## Jak renderovat

```bash
cd pipeline/goat-start-v1
npm run check                                # lint + runtime + layout + motion + kontrast
TMPDIR=~/hf-tmp npx hyperframes render --output preview/preview.mp4 --frames-cache-dir=off
```

> `TMPDIR` a `--frames-cache-dir=off` kvůli malému `/tmp` v našem sandboxu.

## Co se dá ladit bez rozbíjení

- **Texty:** `#badgeText`, `#stampText`, chipsy (data v HTML), `#payBig`, `#paySub`
- **Časy:** vše je v GSAP timeline s absolutními pozicemi (3. argument) — přesouvat celé bloky
- **Barvy:** paleta je v CSS proměnných-like konstantách — hledat hex kódy uvedené výše
- **Dopad:** pozice `IMPACT = { x: 540, y: 890 }` + elementy `#ball`, `#ring1/2`, `.spark`

## Pravidla pro nové segmenty (naučené z tohoto)

1. Každý vstupující element **musí mít baseline** `tl.set(sel, { opacity: 0 }, 0)` — jinak cold-seek render ukáže element dřív
2. Cílový stav fromTo tweenů **vždy explicitně** `opacity: 1`
3. Druhý fromTo téhož elementu → `immediateRender: false`
4. `data-duration` audia = délka souboru, ne krácení — krátí se až renderem
5. Každý `<audio>` potřebuje `id` (jinak tichý)
6. Po každé změně: `npm run check` — musí projít na 0 chyb
