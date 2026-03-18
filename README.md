# noise-killer

> Lies den Artikel. Nicht den Lärm drumherum.

Das eigentliche Problem moderner Nachrichtenseiten ist längst nicht mehr klassische Werbung – dafür gibt es zuverlässige Blocker. Das Problem ist die **redaktionelle Eigenwerbung mitten im Artikeltext**: Boxen, die den Lesefluss unterbrechen und auf andere Artikel verweisen, „Mehr lesen"-Empfehlungen, Newsletter-Anmeldeformulare, die plötzlich auftauchen, und Kommentarsektionen, die niemand gefragt hat. Das nervt – besonders auf Mobile, wo all das die Seiten endlos lang macht.

**noise-killer** ist eine Adblock-Filterliste, die genau diesen Lärm beseitigt. Entstanden aus dem Wunsch, Nachrichtenartikel einfach ungestört lesen zu können, wurde die Liste mit der Zeit um weitere störende Elemente erweitert – Footer, Social-Bars, Teaser –, die auf Seiten nichts verloren haben, wenn man nur den Inhalt möchte. Dabei gilt: Seiten werden entschlackt, nicht kaputt gemacht. Artikeltext, Bildunterschriften, Audio-Player und Funktionen bleiben vollständig erhalten.

Kompatibel mit **uBlock Origin**, **AdBlock Plus**, **AdGuard** und **Brave**.

> Hobbyprojekt, gepflegt per Vibe Coding mit [Claude](https://claude.ai).

---

## Was wird blockiert?

- Inline-Eigenwerbung und redaktionelle Werbeboxen
- „Mehr zum Thema"- und Artikel-Empfehlungen
- Newsletter-Anmeldebox im Artikel
- Kommentarbereiche
- Social-Share-Leisten
- Footer

## Was bleibt immer sichtbar?

- Der eigentliche Artikeltext
- Bildunterschriften und Fotocredits
- Artikel-Toolbar (Anhören, Merken, Teilen)
- Audio-Player im Artikel
- Live-Ticker und Live-Blogs

---

## Unterstützte Seiten

| Site | Was blockiert wird |
|---|---|
| arstechnica.com | Footer, Seitenrauschen |
| de.ifixit.com | Campaign-Banner |
| de.wikipedia.org / de.m.wikipedia.org | Footer |
| faz.net | Empfehlungen, Sidebar, Footer |
| golem.de | Kommentare, Newsletter, Teaser, Footer |
| handelsblatt.com | Teaser, Empfehlungen, Footer |
| heise.de | Ads, Teaser, Newsletter, Empfehlungen, Footer |
| n-tv.de | Aside, Footer |
| ndr.de | Teaser, Social-Box, Footer |
| spiegel.de | Empfehlungen, Verwandte Artikel, Footer |
| sueddeutsche.de | Newsletter, Teaser, Empfehlungen, Footer |
| sz-magazin.sueddeutsche.de | Related, Footer |
| taz.de | Paywall-Overlay, Footer |
| t-online.de | Schlagzeilen-Ticker, Empfehlungen |
| tagesschau.de | Aside, Video-Teaser, Kommentare-Button, Footer |
| tagesspiegel.de | Aside, Footer |
| zeit.de | Kommentare, Teaser, Footer |
| zdfheute.de | Mehr-zum-Thema, Tag-Links, Footer |
| computerbase.de | Ads, Aside, Newsletter, Footer |
| gamestar.de | Teaser, Footer |
| pcgameshardware.de | Kommentare, Shop-Links, Karussell, Footer |
| buffed.de | Kommentare, Social, Aside, Footer |
| stadt-bremerhaven.de | Autor, Sidebar, Kommentare, Affiliate, Footer |
| tarnkappe.info | Newsletter-Modal, Sidebar, Footer |
| derstandard.de | Kommentare, Aside, Footer |
| deutschlandfunk.de | Footer |
| macrumors.com | Footer |
| theverge.com | Recirc, Footer |
| tomsguide.com | Kommentare, Newsletter, Affiliate-Disclaimer, Footer |
| tracker.gg | Upsell-Boxen, Footer |
| wowhead.com | Autor-Bio, Footer |
| imgur.com | Bottom-Recirc |
| amazon.de | Footer-Navigation |
| my.dpd.de | Pakettracking-Seitenelemente, Footer |
| dhl.de | Werbestreifen, Footer |
| myhermes.de | Footer |
| mydealz.de | Sticky-Bar, Footer |
| transfermarkt.de | Werbeklicks, Footer |
| hsreplay.net | Footer |
| steamdb.info | Footer |
| sportschau.de | Teaser, Aside, Footer |
| lto.de | Job-Widget, Teaser, Toolbar, Footer |
| ifun.de / iphone-ticker.de | Newsletter-Form, Footer |

---

## Installation

### uBlock Origin
1. [uBlock Origin](https://ublockorigin.com/) installieren
2. Dashboard öffnen → **Filterlisten** → ganz unten: **Eigene**
3. URL eintragen, **Jetzt aktualisieren** klicken

### AdBlock Plus
1. [AdBlock Plus](https://adblockplus.org/) installieren
2. Optionen → **Erweitert** → **Eigene Filterlisten** → URL eintragen

### AdGuard
1. [AdGuard](https://adguard.com/) installieren
2. Einstellungen → **Filter** → **Eigene** → URL eintragen

### Brave
1. `brave://settings/shields/filters` öffnen
2. URL unter **Eigene Filterlisten** eintragen

**URL für alle:**
```
https://raw.githubusercontent.com/Plexma/noise-killer/main/noise-killer.txt
```

---

## Mithelfen

Neue Domain? Kaputten Filter entdeckt? Pull Requests sind willkommen.
Bitte Selektoren so spezifisch wie nötig formulieren und CSS-Hash-Klassen sowie positionale Selektoren vermeiden.
