# noise-killer

**uBlock Origin Filterliste** zur Entschlackung deutschsprachiger Nachrichtenseiten und anderer Webseiten.

Ziel: Den Artikeltext in den Vordergrund stellen – und alles wegräumen, was nur vom Lesen ablenkt.

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
| www.faz.net | Empfehlungen, Sidebar, Footer |
| www.golem.de | Kommentare, Newsletter, Teaser, Footer |
| www.handelsblatt.com | Teaser, Empfehlungen, Footer |
| www.heise.de | Ads, Teaser, Newsletter, Empfehlungen, Footer |
| www.n-tv.de | Aside, Footer |
| www.ndr.de | Teaser, Social-Box, Footer |
| www.spiegel.de | Empfehlungen, Verwandte Artikel, Footer |
| www.sueddeutsche.de | Newsletter, Teaser, Empfehlungen, Footer |
| sz-magazin.sueddeutsche.de | Related, Footer |
| taz.de | Paywall-Overlay, Footer |
| www.t-online.de | Schlagzeilen-Ticker, Empfehlungen |
| www.tagesschau.de | Aside, Video-Teaser, Footer |
| www.tagesspiegel.de | Aside, Footer |
| www.zeit.de | Kommentare, Teaser, Footer |
| www.zdfheute.de | Mehr-zum-Thema, Tag-Links, Footer |
| www.computerbase.de | Ads, Aside, Newsletter, Footer |
| www.gamestar.de | Teaser, Footer |
| www.pcgameshardware.de | Kommentare, Shop-Links, Karussell, Footer |
| www.buffed.de | Kommentare, Social, Aside, Footer |
| stadt-bremerhaven.de | Autor, Sidebar, Kommentare, Affiliate, Footer |
| tarnkappe.info | Newsletter-Modal, Sidebar, Footer |
| www.derstandard.de | Kommentare, Aside, Footer |
| www.macrumors.com | Footer |
| www.theverge.com | Recirc, Footer |
| www.tomsguide.com | Kommentare, Newsletter, Affiliate-Disclaimer, Footer |
| tracker.gg | Upsell-Boxen, Footer |
| www.wowhead.com | Autor-Bio, Footer |
| imgur.com | Bottom-Recirc |
| www.amazon.de | Footer-Navigation |
| my.dpd.de | Pakettracking-Seitenelemente, Footer |
| www.dhl.de | Werbestreifen, Footer |
| www.myhermes.de | Footer |
| www.mydealz.de | Sticky-Bar, Footer |
| www.transfermarkt.de | Werbeklicks, Footer |
| hsreplay.net | Footer |
| steamdb.info | Footer |
| www.sportschau.de | Teaser, Aside, Footer |
| www.lto.de | Job-Widget, Teaser, Toolbar, Footer |
| www.ifun.de / www.iphone-ticker.de | Newsletter-Form, Footer |

---

## Installation

1. [uBlock Origin](https://ublockorigin.com/) installieren (Chrome, Firefox, Edge)
2. uBlock Origin öffnen → Zahnrad → **Filterlisten** → ganz unten: **Eigene**
3. Folgende URL in das Textfeld eintragen:

```
https://raw.githubusercontent.com/Plexma/noise-killer/main/noise-killer.txt
```

4. **Jetzt aktualisieren** klicken – fertig.

---

## Mithelfen

Neue Domain? Kaputten Filter entdeckt? Pull Requests sind willkommen.
Bitte Selektoren so spezifisch wie nötig formulieren und CSS-Hash-Klassen sowie positionale Selektoren vermeiden.
