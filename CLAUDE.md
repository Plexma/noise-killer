# noise-killer – Arbeitsanweisungen
## Was diese Liste ist
Adblock-Filterliste zur Entschlackung von Nachrichtenseiten.
Kompatibel mit uBlock Origin, AdBlock Plus, AdGuard und Brave.
Ziel: Inline-Eigenwerbung, Artikel-Empfehlungen, Footer, Newsletter-Boxen,
Kommentarbereiche und Social-Bars entfernen – ohne Inhalt zu beschädigen.

## Datei
`noise-killer.txt` – das ist die einzige Filterliste.

## Workflow bei neuen URLs
1. URL im Browser öffnen
2. DOM analysieren – welches CSS-Element ist störend?
3. Selector so präzise wie nötig formulieren
4. Testen ob der Selector funktioniert und nichts Wichtiges blockiert
5. Eintrag in noise-killer.txt einfügen, alphabetisch nach Domain
6. Kommentar darüber: `! Hinzugefügt: DATUM`
7. Bei Bugs: BUGFIX-Kommentar wie bereits in der Liste vorhanden
8. CHANGELOG.md aktualisieren
9. README.md aktualisieren – Tabelle „Unterstützte Seiten" synchron halten (bei jeder Änderung, auch Bugfixes)
10. git add, commit, push zu main
11. GitHub Release erstellen mit:
    `gh release create vX.Y.Z --title "vX.Y.Z - DATUM" --notes "CHANGELOG-INHALT"`

    Die `--notes` müssen immer mit der CHANGELOG-Überschrift beginnen:
    ```
    ## [DATUM] - Kurzbeschreibung

    ### Hinzugefügt / Behoben
    - domain.com: was wurde geändert
    ```
    Beispiel: `--notes "## [2026-03-17] - Deutschlandfunk hinzugefügt\n\n### Hinzugefügt\n- ..."`

    Versionierung (Semantic Versioning):
    - Patch +0.0.1 = Bugfixes an bestehenden Filtern (v1.0.1, v1.0.2...)
    - Minor +0.1.0 = Neue Domain hinzugefügt (v1.1.0, v1.2.0...)
    - Major +1.0.0 = Mehrere Domains gleichzeitig oder umfangreiche Überarbeitungen (v2.0.0, v3.0.0...)
    - Aktuelle Versionsnummer immer aus dem letzten Git-Tag lesen: `git describe --tags --abbrev=0`

## Schreibweise und Formatierung von Domains
In CHANGELOG.md, Release Notes und Kommentaren in noise-killer.txt gilt:
- Domains immer **ohne „www."** – also `gamestar.de`, nicht `www.gamestar.de`
- Domains in Listeneinträgen immer **fettgedruckt** – also `- **gamestar.de**: …`
- Die Domain-Präfixe in den Filterregeln selbst (`www.gamestar.de##selector`) bleiben
  unverändert – dort ist `www.` Teil der technischen Syntax

## CHANGELOG.md Format
```
## [DATUM] - Kurzbeschreibung
### Hinzugefügt
- **domain.com**: was wurde blockiert
### Behoben
- **domain.com**: was wurde gefixt
```

## Kritische Regeln – NIEMALS blockieren
- Live-Ticker und Live-Blogs
- Artikel-Toolbar (Anhören, Merken, Teilen)
- Bildunterschriften und Fotocredits
- Audio-Player im Artikel
- Den eigentlichen Artikeltext
- Artikel-Pagination (nächste/vorherige Seite bei mehrseitigen Artikeln)
- Inhaltsverzeichnis innerhalb eines Artikels

## Immer entfernen – auf jeder Seite
Diese Elemente sind grundsätzlich Noise und sollen auf jeder Seite blockiert werden,
egal ob explizit erwähnt oder nicht:

- **Kommentare-Buttons und -Links** – z. B. „12 Comments", „Zur Diskussion", „zu den
  Kommentaren", auch wenn sie im Artikelkopf/Byline erscheinen (nicht zu verwechseln
  mit der Artikel-Toolbar Teilen/Merken – die bleibt)
- **Kommentarsektionen** – der gesamte Kommentarbereich am Artikelende
- **„Follow topics / Follow authors"-Widgets** – Zephr-basierte oder ähnliche
  Abonnement-/Folgen-Boxen unter dem Artikel
- **Author-Bio-Boxen** – Autorenvorstellung mit Foto und Beschreibungstext unter dem
  Artikel (nicht: Autorenname/Byline in der Artikelüberschrift – die bleibt)
- **Artikel-Empfehlungs-Boxen** – „Auch spannend", „Mehr zum Thema", „Ähnliche
  Artikel", Recirculation-Boxen, Outbrain- und Taboola-Widgets
- **Affiliate-Werbung jeder Art** – Produkt-Slider mit Preisen und Shop-Buttons,
  Affiliate-Button-Gruppen, WP-Block-Affiliate-Widgets, Preisvergleichs-Boxen
- **Eigenwerbungs-Popups und -Banner** – Abo-Werbe-Overlays, Inactivity-Popups
  („Hat noch mehr für dich!"), Plus-Mitgliedschafts-Banner
- **Newsletter-Boxen** – Anmeldeformulare für E-Mail-Newsletter
- **Social-Share-Bars** – floating oder statische Teilen-Buttons (nicht: die
  Artikel-Toolbar, die bleibt)
- **Tag-Listen am Artikelende** – Schlagwort-/Themen-Tags
- **Footer** – der gesamte Seiten-Footer
- **Sendungshinweise** – „Dieses Thema im Programm: Sender | Sendung | Datum"

## Selektoren-Regeln
- CSS-Hash-Klassen (`.css-abc123`) vermeiden – sie ändern sich bei jedem Deploy
- Positionale Selektoren (`nth-of-type`) vermeiden
- Inline-style-Attribute als Selector vermeiden
- Vor dem Schreiben eines `:has()`-Selectors im DOM verifizieren, welches Tag den
  Text tatsächlich enthält – oft ist es ein `div` oder `span`, nicht das erwartete
  `h2`/`h3`
- **`:has-text()` mit Umlauten (ä, ö, ü, ß) ist unzuverlässig** und wird von einigen
  Engines nicht korrekt ausgewertet. Stattdessen: einen reinen CSS-Selector suchen,
  der das Element eindeutig identifiziert (z. B. eine exklusive CSS-Klasse)

## Engine-Unterschiede: uBlock Origin vs. Brave (adblock-rust)
Bekanntes Problem (aufgetreten 2026-03-18, spiegel.de Mobile-Leerraum):
- **uBlock Origin** (IronFox, Firefox, Chrome-Extension) setzt einen MutationObserver –
  Elemente die per JS nachträglich ins DOM eingefügt werden, werden noch erwischt.
- **Brave Shields** (adblock-rust) injiziert Cosmetic-Filter nur einmal beim Seitenaufbau –
  dynamisch hinzugefügte Attribute (z. B. `data-advertisement`) können zu spät kommen.
- **Lösung**: Bei Selektoren die auf JS-gesetzte Attribute zielen (`[data-advertisement~="…"]`)
  immer einen zweiten, CSS-klassen-basierten Fallback-Selector ergänzen, der direkt auf
  die Klasse trifft, die den unerwünschten Effekt erzeugt (z. B. `[class~="sm:min-h-632"]`).
  Klassen-Selektoren sind robuster, weil sie im statischen HTML stehen.
