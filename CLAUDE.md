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
