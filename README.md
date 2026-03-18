# noise-killer

> Lies den Artikel. Nicht den Lärm drumherum.

**noise-killer** ist eine Adblock-Filterliste, die auf Nachrichtenseiten und anderen Websites alles entfernt, was nicht zum eigentlichen Inhalt gehört – Empfehlungsboxen, Newsletter-Banner, Kommentarsektionen, Social-Bars und Seitenfooter.

Der Artikeltext, Bildunterschriften und Multimedia-Inhalte bleiben dabei vollständig erhalten.

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
