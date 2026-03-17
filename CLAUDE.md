# noise-killer – Arbeitsanweisungen
## Was diese Liste ist
uBlock Origin Filterliste zur Entschlackung von Nachrichtenseiten.
Ziel: Inline-Eigenwerbung, Artikel-Empfehlungen, Footer, Newsletter-Boxen,
Kommentarbereiche und Social-Bars entfernen – ohne Inhalt zu beschädigen.
## Datei
`ublock-filters-consolidated.txt` – das ist die einzige Filterliste.
## Workflow bei neuen URLs
1. URL im Browser öffnen
2. DOM analysieren – welches CSS-Element ist störend?
3. Selector so präzise wie nötig formulieren
4. Testen ob der Selector funktioniert und nichts Wichtiges blockiert
5. Eintrag in ublock-filters-consolidated.txt einfügen, alphabetisch nach Domain
6. Kommentar darüber: `! Hinzugefügt: DATUM`
7. Bei Bugs: BUGFIX-Kommentar wie bereits in der Liste vorhanden
8. CHANGELOG.md aktualisieren
9. git add, commit, push zu main
10. GitHub Release erstellen mit:
    `gh release create vX.Y --title "vX.Y - DATUM" --notes "CHANGELOG-INHALT"`

    Versionierung:
    - Erste Version = v1.0
    - Normale Ergänzungen (1-3 Domains) = Patch +0.1 (v1.1, v1.2...)
    - Viele Änderungen auf einmal = Minor +1.0 (v2.0, v3.0...)
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
## Selektoren-Regeln
- CSS-Hash-Klassen (.css-abc123) vermeiden
- Positionale Selektoren (nth-of-type) vermeiden
- Inline-style-Attribute als Selector vermeiden
