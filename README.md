# noise-killer

> Einfach nur der relevante Content. Nicht der Lärm drumherum und mittendrin.

Das eigentliche Problem moderner Nachrichtenseiten ist längst nicht mehr klassische Werbung – dafür gibt es unzählige zuverlässige Blocker. Ein großes Problem ist mittlerweile die **redaktionelle Eigenwerbung mitten im Artikeltext**: Boxen, die den Lesefluss unterbrechen und auf andere Artikel verweisen, „Mehr lesen"-Empfehlungen, Newsletter-Anmeldeformulare, die plötzlich auftauchen, und Kommentarsektionen, nach denen niemand gefragt hat. Die redaktionelle Eigenwerbung trifft sogar zahlende Kunden und hat nicht selten überhaupt nichts mit dem eigentlichen Thema des Artikels zu tun, sondern ist willkürlich. Das nervt – besonders auf Mobile, wo all das die Seiten endlos lang macht und man aufgrund dieser ganzen Unterbrechungen viel mehr scrollen muss, als eigentlich nötig ist.

**noise-killer** ist eine Adblock-Filterliste, die genau diesen Lärm beseitigt. Entstanden aus dem Wunsch, Nachrichtenartikel einfach ungestört lesen zu können, wurde die Liste mit der Zeit um weitere störende Elemente und auch abseits von reinen Nachrichtenseiten erweitert – Footer, Social-Bars, Teaser –, die auf Seiten nichts verloren haben, wenn man nur den Content möchte. Dabei gilt: Seiten werden entschlackt, nicht kaputt gemacht. Bilder, Videos, Audio-Player und alle anderen Medieninhalte, die zum Artikel gehören, bleiben selbstverständlich unangetastet – genau wie der gesamte Artikeltext und alle Funktionen.

Kompatibel mit **uBlock Origin**, **AdBlock Plus**, **AdGuard** und **Brave** – jeweils auf Desktop und Mobile. Grundsätzlich funktioniert die Liste mit jedem Browser oder Adblocker, der das Adblock-Filterlistenformat (ABP-Syntax) verarbeiten kann.

> Hobbyprojekt, gepflegt per Vibe Coding mit [Claude](https://claude.ai).

---

## Was wird blockiert?

- Inline-Eigenwerbung und redaktionelle Werbeboxen
- „Mehr zum Thema"- und Artikel-Empfehlungen
- Newsletter-Anmeldeboxen im Artikel
- Kommentarbereiche
- Social-Share-Leisten
- Footer

## Was bleibt immer sichtbar?

- Der eigentliche Artikeltext
- Bilder, Videos und alle Medieninhalte, die zum Artikel gehören
- Bildunterschriften und Fotocredits
- Artikel-Toolbar (Anhören, Merken, Teilen)
- Audio-Player im Artikel
- Live-Ticker und Live-Blogs

---

## Unterstützte Seiten

**Legende:** 📰 Artikelempfehlungen · 📬 Newsletter-Box · 💬 Kommentare · 🔗 Social-/Share-Leiste · 🦶 Footer · 📢 Eigenwerbung/Teaser · 🛍️ Affiliate/Shop-Links · 🪧 Banner/Overlays

| Seite | Was entfernt wird |
|---|---|
| amazon.de | 🦶 |
| arstechnica.com | 📢 🦶 |
| buffed.de | 💬 🔗 📢 🦶 |
| computerbase.de | 📢 📬 🦶 |
| de.ifixit.com | 🪧 |
| de.wikipedia.org / de.m.wikipedia.org | 🦶 |
| derstandard.de | 💬 📢 🦶 |
| deutschlandfunk.de | 🦶 |
| dhl.de | 🪧 🦶 |
| faz.net | 📰 📢 🦶 |
| gamestar.de | 📢 🦶 |
| golem.de | 💬 📬 📢 🦶 |
| handelsblatt.com | 📰 📢 🦶 |
| heise.de | 📰 📬 📢 🦶 |
| hsreplay.net | 🦶 |
| ifun.de / iphone-ticker.de | 📬 🦶 |
| imgur.com | 📰 |
| lto.de | 📰 📢 🦶 |
| macrumors.com | 🦶 |
| my.dpd.de | 📢 🦶 |
| mydealz.de | 🪧 🦶 |
| myhermes.de | 🦶 |
| n-tv.de | 📢 🦶 |
| ndr.de | 🔗 📢 🦶 |
| pcgameshardware.de | 💬 🛍️ 📢 🦶 |
| spiegel.de | 📰 🦶 |
| sportschau.de | 📢 🦶 |
| stadt-bremerhaven.de | 💬 🛍️ 📢 🦶 |
| steamdb.info | 🦶 |
| sueddeutsche.de | 📰 📬 📢 🦶 |
| sz-magazin.sueddeutsche.de | 📰 🦶 |
| t-online.de | 📰 📢 |
| tagesschau.de | 💬 📢 🦶 |
| tagesspiegel.de | 📢 🦶 |
| tarnkappe.info | 📬 📢 🦶 |
| taz.de | 🪧 🦶 |
| theverge.com | 💬 📰 📬 📢 🦶 |
| tomsguide.com | 💬 📬 🛍️ 🦶 |
| tracker.gg | 📢 🦶 |
| transfermarkt.de | 📢 🦶 |
| wowhead.com | 📢 🦶 |
| zdfheute.de | 📰 🔗 🦶 |
| zeit.de | 💬 📢 🦶 |

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
