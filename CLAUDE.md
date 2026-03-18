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
## CHANGELOG.md Format
## [DATUM] - Kurzbeschreibung
### Hinzugefügt
- domain.com: was wurde blockiert
### Behoben
- domain.com: was wurde gefixt
## Kritische Regeln – NIEMALS blockieren
- Live-Ticker und Live-Blogs
- Artikel-Toolbar (Anhören, Merken, Teilen)
- Bildunterschriften und Fotocredits
- Audio-Player im Artikel
- Den eigentlichen Artikeltext
## Immer entfernen – auf jeder Seite
Diese Elemente sind grundsätzlich Noise und sollen auf jeder Seite blockiert werden,
egal ob explizit erwähnt oder nicht:
- **Kommentare-Buttons und -Links** – z. B. „12 Comments", „Zur Diskussion", auch
  wenn sie im Artikelkopf/Byline erscheinen (nicht zu verwechseln mit der
  Artikel-Toolbar Teilen/Merken – die bleibt)
- **„Follow topics / Follow authors"-Widgets** – Zephr-basierte oder ähnliche
  Abonnement-/Folgen-Boxen unter dem Artikel
## Selektoren-Regeln
- CSS-Hash-Klassen (.css-abc123) vermeiden
- Positionale Selektoren (nth-of-type) vermeiden
- Inline-style-Attribute als Selector vermeiden
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
