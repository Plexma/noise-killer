## [2026-08-17] - Wöchentlicher Rotations-Audit Bucket 5 (theverge.com, zeit.de)

### Behoben
- **theverge.com**: Affiliate-Produkt-Slider ("Partner Content From...") wird direkt in den Artikel-Flow injiziert – bisher ungeblockt.
- **zeit.de**: Outbrain-Leseempfehlungen-Widget (`#outbrain`) und Google-Preferred-Source-Eigenwerbebanner (`aside.zps-widget`) waren ungeblockt.

Hinweis: **transfermarkt.de** (ebenfalls Bucket 5) konnte diese Woche nicht geprüft werden – CloudFront blockiert Zugriffe aus dieser Umgebung mit 403. Erneuter Check in einer künftigen Rotation nötig. tomsguide.com, wiwo.de, wowhead.com und zdfheute.de wurden geprüft und sind sauber (nur harmlose tote Selektoren ohne Auswirkung notiert).

## [2026-08-11] - tracker.gg: Eigenwerbung auf Startseite und Profilseite

### Hinzugefügt
- **tracker.gg**: Mobile-App-Promo-Banner auf der Startseite (`div.mobile-promo`) war ungeblockt.
- **tracker.gg**: Vollbild-Overlay-Popup "Stop missing out on potential insights!" (Desktop-App-Werbung) auf Profilseiten war ungeblockt. Auf den Teleport-Backdrop mit Overwolf-Download-Link gescoped, um andere Modals im selben Portal (z. B. Login) nicht zu treffen.
- **tracker.gg**: Inline-Promo-Karte "Check out our desktop app!" auf Profilseiten (`a.profile-hint`) war ungeblockt.

## [2026-08-08] - Vollaudit aller Domains: Startseite + Artikel

Vollständiger Audit aller 55 Domains. Neu gegenüber früheren Audits: **jede Domain wurde auf Startseite UND Artikelseite geprüft** – bisher lag der Fokus auf Artikelseiten. Genau dort lagen die schwersten Fehler: mehrere Selektoren, die auf Artikeln sauber greifen, haben auf der Startseite den kompletten Inhalt versteckt. Zusätzlich wurde jeder Selektor per DOM-Query gegen eine echte Browser-Engine geprüft (437 reine CSS-Selektoren, 0 Syntaxfehler).

### Behoben – Overblocking (versteckter Inhalt)
- **tomsguide.com**: `div > ul` ersatzlos entfernt. Auf der Startseite traf die Regel jede Artikel-Widget-Liste (u. a. 3152px, 2392px, 1547px) – die Startseite blieb praktisch leer. Auf Artikeln traf sie als einziges sichtbares Element die Sprungnavigation ("Specs Compared | Design | Displays | …"), also das Inhaltsverzeichnis. Die Regel hat nur Inhalt blockiert.
- **heise.de**: `div[data-module-name="TeasersModule"]` traf auf der Startseite 38 Module – praktisch die komplette Startseite (IT, Wissenschaft & Forschung, Mobiles, Entertainment, Wirtschaft, Netzpolitik, Journal, c't, iX, Mac & i, Make, Foto, Autos, Telepolis). Auf den Artikel-Layout-Container gescoped (`div.a-layout`), dort weiterhin genau 1 Treffer.
- **heise.de**: `footer` traf auf der Startseite 165 Elemente, 164 davon die Meta-Zeile jedes Teasers ("vor 6 Stunden | bestenlisten"). Auf `footer:not(.ho-text-muted)` präzisiert – Zeitstempel und Quelle sind wieder sichtbar.
- **sueddeutsche.de**: `div[data-test]` ersatzlos entfernt – die Regel traf auf beiden Seitentypen ausschließlich die Site-Navigation (Produktwechsler, Ressort-Navigation, Menü-Dialog).
- **sueddeutsche.de**: `footer` traf auf der Startseite 115 Elemente, 114 davon die Teaser-Zeile "SZ Plus | Von <Autor> | Artikel <Länge>"; auf Artikeln zusätzlich die Byline samt "Artikel merken"-Toolbar. Auf `footer:not(article footer)` präzisiert.
- **n-tv.de**: `aside` traf auf der Startseite 12 Elemente – nur eines ist die gemeinte Video-Sidebar, die übrigen 11 sind News-Spalten mit echten Artikel-Teasern (zusammen ~16.000px). Auf `aside:has([class*="widget-teaser-default"])` eingegrenzt.
- **n-tv.de**: `section[class*="widget-teaser"]` traf auch den **Ukraine-Liveticker** – Live-Ticker dürfen nie geblockt werden. Liveticker-Variante ausgeschlossen.
- **t-online.de**: `[data-testid="StageLayout.StreamItem"]:has(> article)` traf auf der Startseite 78 Nachrichten-Einträge. Auf Artikeln lagen alle 10 Treffer ohnehin in `Page.PageStages`, das bereits geblockt wird – die Regel war dort redundant und wurde entfernt.
- **faz.net**: `footer` traf auf der Startseite 109 Elemente, 108 davon die Zeile mit dem Autorennamen jedes Teasers. Auf `footer:not([class])` plus `footer.meta2` aufgeteilt – Startseite 1 Treffer, Artikel unverändert 2.
- **tagesspiegel.de**: `footer` ersatzlos entfernt – auf der Startseite 97 Teaser-Bylines ("Von <Autor> | 0 Kommentare"), auf Artikeln nur 1 Treffer, der bereits von `#sitefooter-container` abgedeckt ist.
- **lto.de**: `.article-teaser-list` ersatzlos entfernt – auf der Startseite ist das die Haupt-Nachrichtenliste; auf Artikeln liegt sie in `section.content__related`, das bereits eine eigene Regel hat.
- **computerbase.de**: `div.block1.block1--breakout` ersatzlos entfernt – auf Artikeln 0 Treffer, auf der Startseite 2, beide redaktioneller Inhalt (Top-Test-Teaser, Kaufberatung/Ranglisten).
- **rbb24.de**: `section.section__stacked` traf auf der Startseite 3 redaktionelle Content-Module mit Audio-/Video-Playern. Da Klassen und Elternknoten auf beiden Seitentypen identisch sind, auf den Überschriftentext "Mehr bei rbb" gepinnt.
- **androidauthority.com**: `main > div:has(a[href*="/external-links/"])` versteckte auf der Startseite den kompletten Artikel-Feed (10467px), weil der Affiliate-Disclaimer dort eine Ebene tiefer liegt. Auf `div:has(> p > a[href*="/external-links/"])` eingegrenzt.
- **arstechnica.com**: `a.post-navigation-link` blockierte auf der Startseite den "Load more"-Button und damit die Pagination. Auf die Artikel-Wrapper `.nav-previous` / `.nav-next` umgestellt.
- **ifun.de** / **iphone-ticker.de**: `div > div > div > form[action][method]` blockierte auf der Startseite das Suchfeld. Auf den Contact-Form-7-Wrapper `div.wpcf7` eingegrenzt; das Kommentarformular ist ohnehin über `#article-single-comments` abgedeckt.
- **sportschau.de**: Die Button-Gruppe "Live-Ticker zum Nachlesen" wurde mitgeblockt – Live-Ticker dürfen nie geblockt werden. Button-Gruppen mit Liveticker-Link ausgeschlossen, die Kalender-Promo bleibt geblockt.
- **raider.io**: Promo-Banner-Regel entfernt – `slds-m-bottom--small` ist nicht mehr exklusiv für Promos und traf auf der Startseite die Sektionsüberschrift "Top Mythic+ Teams".
- **theverge.com**: Beide `#zephr-anchor`-Regeln entfernt – das Element ist inzwischen der Artikeltext-Container, nicht mehr der CTA-Anker. `#zephr-anchor > div:has(> span + ul)` hätte Artikeltext verstecken können.

### Behoben – Underblocking (Noise war sichtbar)
- **stadt-bremerhaven.de**: Artikel-Empfehlungsbox (`#cb-related-box`, 6 Karten) und "Auf Google folgen"-Promo (`a.cb-google-follow-meta`) waren komplett ungeblockt.
- **wowhead.com**: Newsletter-Box "Subscribe to our Newsletters!" (`#newsletter-cta`) war ungeblockt.
- **ndr.de**: WhatsApp-Kanal-Abo-Box ("News aus deiner Region – jetzt auch direkt per WhatsApp") war ungeblockt. Auf den WhatsApp-Link gepinnt, damit redaktionelle Infoboxen unangetastet bleiben.
- **amazon.de**: Auf Mobile heißt der Footer `#nav-ftr`, nicht `#navFooter` – der Footer war auf Mobile komplett ungeblockt. Zusätzlich `#mobile-dp-ilm_feature_div_01` auf `_0` korrigiert (gleiche ID-Umnummerierung wie zuvor beim Prime-Banner).
- **9to5google.com**: Die Affiliate-Box-Regeln von 9to5mac.com ergänzt – beide Seiten nutzen dasselbe Theme, die Regeln fehlten hier bisher.

Sauber, keine Änderung: 9to5mac.com, arstechnica.com (Artikel), de.ifixit.com, macrumors.com, tarnkappe.info, gamestar.de, golem.de, spiegel.de, zeit.de, taz.de, focus.de, handelsblatt.com, wiwo.de, tagesschau.de, zdfheute.de, deutschlandfunk.de, derstandard.at, derstandard.de, imgur.com, startpage.com, wikipedia.org, dhl.de, mydealz.de, myhermes.de, my.dpd.de, sz-magazin.sueddeutsche.de, sportdaten.spiegel.de.

Nicht prüfbar in der Testumgebung (bestehende Regeln unverändert gelassen): buffed.de und pcgameshardware.de (Cloudflare-Bot-Check auf Artikelseiten), hsreplay.net, steamdb.info, tracker.gg (Cloudflare-Bot-Check), transfermarkt.de (Wartungsmodus), nytimes.com (im Browser der Testumgebung gesperrt).

---

## [2026-07-27] - Wöchentlicher Rotations-Audit Bucket 2

Geprüft (Bucket 2 von 5, Rotation nach ISO-Kalenderwoche): tarnkappe.info, taz.de, tracker.gg, wikipedia.org, amazon.de, androidauthority.com, buffed.de, computerbase.de, derstandard.at, derstandard.de, deutschlandfunk.de, dhl.de.

### Behoben
- **wikipedia.org**: `div.post-content.footer-content` entfernt – matcht auf de.wikipedia.org und de.m.wikipedia.org (Desktop + Mobile-Skin geprüft) nicht mehr, DE nutzt inzwischen ebenfalls den Vector-Skin-Footer (`mw-footer-container`), der bereits separat geblockt wird.

Sauber, keine Änderung: tarnkappe.info, taz.de, amazon.de, androidauthority.com, computerbase.de, deutschlandfunk.de, dhl.de.

Nicht prüfbar (Cloudflare-Bot-Check bzw. Consent-Wall ohne Content-Load in der Testumgebung): tracker.gg, buffed.de (Artikelseite), derstandard.at, derstandard.de – bestehende Regeln unverändert gelassen.

---

## [2026-07-20] - Wöchentlicher Rotations-Audit Bucket 1

Geprüft (Bucket 1 von 5, Rotation nach ISO-Kalenderwoche): 9to5google.com, 9to5mac.com, arstechnica.com, de.ifixit.com, hsreplay.net, imgur.com, my.dpd.de, raider.io, sportdaten.spiegel.de, stadt-bremerhaven.de, steamdb.info.

### Behoben
- **9to5google.com** / **9to5mac.com**: `p:has(> em:only-child)` blockte fälschlich normalen Artikeltext (jeder Absatz mit genau einem `<em>`-Kind, z. B. Zitate wie "In a statement to *9to5Mac*, …") – auf `p:has(> em:only-child > strong:first-child)` präzisiert. Trifft weiterhin das "Follow Ben: Twitter/X, Threads, …"-Widget, nicht mehr normalen Fließtext.
- **de.ifixit.com**: Werbebanner ("Kostenloser Versand ab 65 € Bestellwert*") von `.component-WPCampaignBanner` auf `.component-RibbonBanner` migriert – alte Klasse griff nicht mehr, Banner war sitewide ungeblockt sichtbar. Neue Klasse ergänzt.

Sauber, keine Änderung: arstechnica.com, imgur.com.

Nicht prüfbar (Cloudflare-Bot-Check/Login-Wall verhindert Content-Zugriff in der Testumgebung): hsreplay.net, steamdb.info, my.dpd.de (Paketverfolgung erfordert Sendungsdaten/Login) – bestehende Regeln unverändert gelassen. raider.io: Kern-Selektoren (Footer, Cookie-Banner) bestätigt intakt; die Recruitment-Panel-Selektoren (SLDS-Klassen) konnten mangels erreichbarer Gilden-Recruitment-Seite nicht verifiziert werden. sportdaten.spiegel.de: Heimspiel-Widget erscheint nur an Bundesliga-Spieltagen (aktuell Sommerpause) – nicht testbar.

---

## [2026-07-16] - Vollständiger Audit aller Domains (Teil 2)

Fortsetzung des vollständigen Audits (Teil 1 s.u.). Geprüft: derstandard.at, derstandard.de, deutschlandfunk.de, dhl.de, faz.net, focus.de, gamestar.de, golem.de, rbb24.de, spiegel.de, sportdaten.spiegel.de, sportschau.de, stadt-bremerhaven.de, startpage.com, sueddeutsche.de, sz-magazin.sueddeutsche.de, t-online.de, tagesschau.de, tagesspiegel.de, tarnkappe.info, taz.de, theverge.com, tomsguide.com (23 Domains). Damit sind alle 55 Domains der Liste einmal vollständig durchlaufen.

### Hinzugefügt
- **startpage.com**: Bezahlter "Sponsored"-Ergebnisblock auf der Suchergebnisseite (`.serp-result-preview`) ergänzt.

### Behoben
- **rbb24.de**: `.container__article-component--small` blockte auch das reguläre Inline-Artikelbild (gleiche Klassenkombination) – auf Elemente mit clinker-Teaser-Kind eingeschränkt.
- **sportschau.de**: `div.copytext-element-wrapper.columns.twelve` blockte im Artikelkopf die Autorenzeile mit – Autorenzeile ausgeschlossen.
- **stadt-bremerhaven.de**: `p.post-byline` blockte die komplette Autor-Metazeile inkl. Name und Datum statt nur des Kommentar-Links – auf den Kommentar-Link eingeschränkt. `article table` war zu generisch und hätte reguläre Inhaltstabellen mitblockiert – auf die Amazon-Affiliate-Tabellenklasse eingeschränkt.
- **sueddeutsche.de**: `[data-manual-remove]` blockte die Anhören-Toolbar, die echten Audio-Player-Elemente und die Teilen-Toolbar mit – diese ausgeschlossen. Zusätzlich blockte `[data-testid="byline"]` fälschlich die Autorenzeile – Regel entfernt.
- **faz.net**: `[data-external-selector="html-element"]` blockte auch eingebettete Interactive-Content-Elemente (Karten, Datawrapper-Charts) im Artikeltext – auf die zwei tatsächlichen Werbe-Wrapper (Newsletter-Box, Job-Empfehlungen) eingeschränkt.
- **theverge.com**: `a[href="/subscribe"]` griff nicht mehr, da der Subscribe-Button-Link inzwischen immer Tracking-Query-Parameter trägt – auf Präfix-Match umgestellt.

Sauber, keine Änderung: deutschlandfunk.de, dhl.de, focus.de, gamestar.de, spiegel.de, sportdaten.spiegel.de, sz-magazin.sueddeutsche.de, t-online.de, tagesschau.de, tagesspiegel.de, tarnkappe.info, taz.de. Nicht prüfbar (Anti-Adblock-/Consent-Wall verhindert Content-Load in der Testumgebung): derstandard.at, derstandard.de, golem.de – bestehende Regeln unverändert gelassen, Nachprüfung mit echtem Browser/Adblocker-Setup empfohlen.

Hinweis (kein Filterlisten-Fix möglich): tomsguide.com leitete in mehreren unabhängigen Tests reproduzierbar und ohne Nutzerinteraktion zu einer Scareware-Seite (`report.error-report.com`, gefälschte Fehlermeldung) weiter – vermutlich ein kompromittiertes Werbenetzwerk. Da es sich um einen JS-/Netzwerk-Redirect und kein DOM-Element handelt, kann eine Cosmetic-Filterliste dies nicht beheben.

---

## [2026-07-16] - Vollständiger Audit aller Domains (Teil 1)

Auf Nutzerwunsch vollständige Prüfung sämtlicher Domains statt nur des Wochen-Buckets. Geprüft: 9to5google.com, 9to5mac.com, amazon.de, androidauthority.com, arstechnica.com, buffed.de, computerbase.de, de.ifixit.com, handelsblatt.com, heise.de, hsreplay.net, ifun.de, imgur.com, iphone-ticker.de, lto.de, macrumors.com, my.dpd.de, mydealz.de, myhermes.de, n-tv.de, ndr.de, nytimes.com, pcgameshardware.de, raider.io (24 Domains) sowie tracker.gg, transfermarkt.de, wikipedia.org, wiwo.de, wowhead.com, zdfheute.de, zeit.de (bereits am 2026-07-13 im Rotations-Bucket geprüft). Restliche ~24 Domains (derstandard.at/.de, deutschlandfunk.de, dhl.de, faz.net, focus.de, gamestar.de, golem.de, rbb24.de, spiegel.de, sportdaten.spiegel.de, sportschau.de, stadt-bremerhaven.de, startpage.com, sueddeutsche.de, sz-magazin.sueddeutsche.de, t-online.de, tagesschau.de, tagesspiegel.de, tarnkappe.info, taz.de, theverge.com, tomsguide.com) sind für den nächsten Durchlauf zurückgestellt.

### Hinzugefügt
- **9to5mac.com**: Affiliate-Box "Do more with your Apple products" (Amazon-Produktlinks) im Artikel ergänzt.
- **androidauthority.com**: "Our top deals of the day"-Affiliate-Widget im Artikeltext ergänzt.
- **buffed.de**: Kommentarsektion (`#article_comment_box`) und Social-Share-Icons (`span.artSocialLinks`) ergänzt.
- **hsreplay.net**: Ad-Slot auf der Startseite und Eigenwerbungs-Banner im Header ergänzt.
- **imgur.com**: Kommentarbereich (`div.CommentsList`) und klebender Bottom-Ad-Banner (`.Ad-adhesive`) ergänzt.
- **pcgameshardware.de**: Affiliate-PC-Vergleichstabelle im Artikel ergänzt.

### Behoben
- **amazon.de**: ID-Nummerierung geändert (`_01` → `_0`), Prime-Video-Promo-Regel griff nicht mehr.
- **ifun.de** / **iphone-ticker.de**: `#viewport-share` griff nicht mehr, Share-Leiste liegt jetzt in `span.socialnetworks`.
- **imgur.com**: `div.BottomRecirc` war tot (Klasse existiert nach Redesign nicht mehr).
- **macrumors.com**: `#maincontent > div` blockte auf Roundup-/Guide-Seiten fälschlich die redaktionelle Timeline-Chronik (Overblocking, kompletter Seiteninhalt versteckt) – Timeline anhand des Klassen-Präfixes ausgeschlossen.
- **mydealz.de**: Klasse `bRad--a` zu `bRad--fromW4-a` umbenannt, Regel griff auf normalen Produkt-Deals nicht mehr.

Sauber, keine Änderung: 9to5google.com, arstechnica.com, computerbase.de, de.ifixit.com, handelsblatt.com, heise.de, lto.de, myhermes.de, n-tv.de, ndr.de, raider.io. Nicht prüfbar (Browser-Tool blockiert/verweigert Zugriff): my.dpd.de, nytimes.com.

---

## [2026-07-13] - Wöchentlicher Rotations-Audit Bucket 5: transfermarkt.de, zeit.de

### Behoben
- **zeit.de**: `div.article-actions.article__item` blockte den kompletten Toolbar-Container inkl. Audio-Player (TTS-Vorlesefunktion) – Kritische Regel „Audio-Player im Artikel nie blockieren" verletzt. Auf den Kommentare-Link (`> a[href="#comments"]`) eingeschränkt, Audio-Player/Verschenken/Zusammenfassen/Merken bleiben sichtbar.
- **transfermarkt.de**: „Weitere News"-Empfehlungsbox (`div.more-news`) und Newsforum-Diskussionsbox (`div.box:has(a[href*="/newsforum/"])`) auf News-Artikelseiten waren bislang ungeblockt – beides DIVs statt der bereits erfassten SECTION-/ID-Selektoren.

Rotations-Runde für Bucket 5 (Kalenderwoche 29): tracker.gg, transfermarkt.de, wikipedia.org, wiwo.de, wowhead.com, zdfheute.de, zeit.de geprüft. tracker.gg, wikipedia.org, wiwo.de, wowhead.com, zdfheute.de sauber, keine Änderungen.

---

## [2026-07-06] - Wöchentlicher Rotations-Audit Bucket 4: n-tv.de, rbb24.de, sportschau.de

### Hinzugefügt
- **sportschau.de**: Social-Share-Bar am Artikelkopf (`nav.socialbuttons` – Facebook/WhatsApp/E-Mail/Drucken) war bislang ungeblockt.
- **n-tv.de**: Outbrain-Empfehlungswidget am Artikelende (`div[class*="Outbrain_space"]`) ergänzt – lag außerhalb von `aside`/`footer` und war nicht erfasst.

### Behoben
- **rbb24.de**: Der Selektor für den Kommentarbereich (`section.container.section--white.section--rounded`) traf inzwischen auch die Artikel-Body-`<section>`, die dieselbe Klassenkombination bekommen hat – dadurch wurde der **gesamte Artikeltext versteckt**. Auf den Kommentar-Container (`:has(> #comments)`) eingeschränkt; der Artikel-Body hat als direktes Kind `div.container__article`, nie `#comments`, und bleibt jetzt sichtbar.
- **n-tv.de**: n-tv liefert die am 2026-07-02 als „umbenannt" geglaubten Klassen wieder unter den alten Namen aus (`social-share_social-share`, `article-detail-footer_tags`) – offenbar A/B-/Rollout-Varianten. Beide Namensvarianten werden jetzt parallel abgedeckt, damit Share-Bar und Tag-Liste in jedem Bundle getroffen werden.

Rotations-Runde für Bucket 4 (Kalenderwoche 28): macrumors.com, mydealz.de, myhermes.de, n-tv.de, ndr.de, nytimes.com, pcgameshardware.de, rbb24.de, spiegel.de, sportschau.de, startpage.com geprüft. macrumors.com, myhermes.de, ndr.de, nytimes.com, pcgameshardware.de, startpage.com sauber. spiegel.de unverändert (die Feature-Bar-Regel versteckt bewusst alles außer „Artikel verschenken", auf Nutzerwunsch dokumentiert). mydealz.de: zwei tote Selektoren (`[data-t="voteSecondary"]`, `div.bRad--a.bg--main.space--mt-2`) auf dem geprüften Deal nicht auslösbar – vermutlich seitentyp-spezifisch (Gutschein-Deal), nicht sicher retargetbar, daher unverändert belassen.

---

## [2026-07-02] - Wöchentlicher Rotations-Audit Bucket 5: theverge.com, tomsguide.com, transfermarkt.de, wiwo.de, wowhead.com

### Hinzugefügt
- **tomsguide.com**: Tag-Liste ("TOPICS") und Autoren-Bio-Box am Artikelende entfernt.
- **wiwo.de**: Inline-Artikel-Teaser im Fließtext entfernt – gleiches Wrapper-Muster wie handelsblatt.com, bislang auf wiwo.de nicht übernommen.
- **wowhead.com**: Artikel waren bis auf Autoren-Bio, endofpost und Footer komplett ungeblockt. Neu: „Drop the Ads"-Werbefrei-Eigenwerbung (`#premium-house-block`), „Blue Tracker"/„Recent News"-Empfehlungsspalten (`div.news-recent`), gesamter Kommentarbereich inkl. „Show N Comments"-Button (`#news-comments-wrapper`).

### Behoben
- **theverge.com**: `.duet--article--related` griff nicht mehr (0 Treffer) – Klasse umbenannt zu `duet--layout--header-pattern`. Neue Klasse deckt zusätzlich bislang ungeblockte „Most Popular"- und „Top Stories"-Sidebar-Widgets ab.
- **transfermarkt.de**: Neue Spieltermine-Sektion (`section#tm-matches`, Svelte-Widget) bekam ebenfalls die Klasse `.box` – `section.box` war dadurch nicht mehr exklusiv für die Videos-Eigenwerbung und hätte legitime Spieltermine mitgeblockt (Overblocking-Prävention). Zusätzlich einen zweiten Footer außerhalb des `<footer>`-Tags ergänzt (`section.tm-footer__mobile`, trotz Namens auch auf Desktop gerendert), der bisher ungeblockt war.

Fünfte und letzte Runde des ersten wöchentlichen Rotations-Durchlaufs: theverge.com, tomsguide.com, transfermarkt.de, wiwo.de, wowhead.com, zdfheute.de, zeit.de geprüft. Damit sind erstmals alle 55 Domains der Liste einmal durchlaufen.

---

## [2026-07-02] - Wöchentlicher Rotations-Audit Bucket 4: n-tv.de, t-online.de

### Behoben
- **n-tv.de**: CSS-Modules-Klassennamen bei Redesign umbenannt (`social-share` → `ShareBtn_share-*`, `article-detail-footer_tags` → `ArticleDetailFooter_tags-*`) – alte Selektoren griffen nicht mehr, Share-Buttons und Tag-Liste blieben sichtbar.
- **t-online.de**: Seiten-Footer wechselte von `<div data-testid="PageFooter">` zu `<footer data-testid="PageFooter">` (semantisches HTML-Tag) – die auf `div` eingeschränkte Regel griff nicht mehr, Footer blieb sichtbar.

Vierte Runde des wöchentlichen Rotations-Checks: n-tv.de, ndr.de, nytimes.com, pcgameshardware.de (Cloudflare-Check, übersprungen), rbb24.de, spiegel.de, sportschau.de, startpage.com (Homepage-Check hing, SERP-Regeln bestätigt), sueddeutsche.de, t-online.de, tagesschau.de, tagesspiegel.de geprüft – alle anderen sauber.

---

## [2026-07-02] - Wöchentlicher Rotations-Audit Bucket 3: gamestar.de, ifun.de, iphone-ticker.de

### Hinzugefügt
- **gamestar.de**: „Zum Thema"-Empfehlungsbox (`div.contentteaser.row.box.contenttimelineitem-box`) entfernt – neue Variante des bekannten Teaser-Musters, bisher nicht erfasst.
- **ifun.de**: Tag-Liste am Artikelende (`#article-single-footer-tags`) entfernt.
- **iphone-ticker.de**: Tag-Liste am Artikelende (`#article-single-footer-tags`) entfernt – gleiches Muster wie ifun.de (identische Plattform).

Dritte Runde des wöchentlichen Rotations-Checks: faz.net, focus.de, gamestar.de, golem.de, handelsblatt.com, heise.de, ifun.de, iphone-ticker.de, lto.de, macrumors.com, mydealz.de, myhermes.de geprüft – alle anderen sauber.

---

## [2026-07-02] - Wöchentlicher Rotations-Audit Bucket 2: androidauthority.com, deutschlandfunk.de

### Hinzugefügt
- **deutschlandfunk.de**: Artikel-Empfehlungs-Box am Artikelende (`article.b-thema-teaser-list`, „Mehr zu …"-Kachelreihe), Hörtipps-Empfehlungslinks im Artikel und Sendungshinweis („Diese Nachricht wurde am … gesendet") entfernt – bislang blockte nur der Footer.

### Behoben
- **androidauthority.com**: Follow-Topics-Widget lief an der bestehenden Regel vorbei – Viafoura rendert den Follow-Button jetzt als Custom-Element `<vf-topic-follow>` statt der alten Button-Klasse `vf-topic-follow-button`. Zusätzlich einen „Comment Policy"-Hinweistext direkt vor dem Kommentarbereich entfernt, der bislang nicht abgedeckt war.

Zweite Runde des wöchentlichen Rotations-Checks: tarnkappe.info, taz.de, tracker.gg (übersprungen), wikipedia.org, amazon.de, androidauthority.com, buffed.de (übersprungen), computerbase.de, derstandard.at/de, deutschlandfunk.de, dhl.de geprüft.

---

## [2026-07-02] - Wöchentlicher Rotations-Audit: 9to5google.com, iFixit, Spiegel-Spielbanner

### Hinzugefügt
- **de.ifixit.com**: News-Artikel waren bis auf einen Campaign-Banner komplett ungeblockt. Neu: „Kommentar hinzufügen"-Link im Byline (`li.entry-meta-comments`), Artikel-Empfehlungen (`div.related-posts-wrap`), gesamter Kommentarbereich (`#wppost-comments-container`), Footer inkl. Newsletter-Box (`footer`).

### Behoben
- **9to5google.com**: Google-Preferred-Source-Badge und Werbe-Disclaimer, die inzwischen an den „More on …"-Abschnitt angehängt werden, liefen an der bestehenden Regel vorbei und blieben sichtbar (`div.google-preferred-source-badge`, `div.ad-disclaimer-container`) – analog zum 9to5mac.com-Fix aus der letzten Prüfung.
- **spiegel.de** (Iframe `sportdaten.spiegel.de`): Glücksspiel-Disclaimer im Spiel-/Match-Banner war als ID `#legal-notice` adressiert – die Seite nutzt diese ID nicht mehr, der Disclaimer („10€ Einsatz | 18+ | … | Nur für Neukunden") leakte sichtbar durch. Selektor auf die neue Klasse `div.hs-legal-notice` umgestellt.

### Geändert
- **sueddeutsche.de**: `sz-magazin.sueddeutsche.de` wurde als eigenständige Subdomain aufgegeben und leitet komplett auf `www.sueddeutsche.de/magazin/...` um. Die alten subdomain-gescopeten Regeln greifen dadurch nie mehr (Cosmetic-Filter wirken pro Frame-Domain). Kein Ersatzbedarf: `/magazin`-Artikel laufen über dasselbe Template wie der Rest von sueddeutsche.de und sind durch das dortige Regelset bereits abgedeckt. Regeln als Doku im Quelltext belassen.

Erste Runde des neuen wöchentlichen Rotations-Checks (siehe `noise-killer-weekly-audit`): 9to5google.com, arstechnica.com, de.ifixit.com, hsreplay.net (Cloudflare-Check, übersprungen), imgur.com, my.dpd.de, raider.io, sportdaten.spiegel.de, stadt-bremerhaven.de, steamdb.info (Cloudflare-Check, übersprungen), sz-magazin.sueddeutsche.de geprüft.

---

## [2026-07-02] - wiwo.de hinzugefügt, 9to5mac.com Affiliate-Box entfernt

### Hinzugefügt
- **wiwo.de**: Neue Domain. Läuft auf derselben Angular-Plattform wie **handelsblatt.com** (Handelsblatt Media Group), daher analoge `app-*`-Selektoren: Werbung (`app-advertisement`, `app-content-advertisement`, `app-special-advertisement`, `app-storyline-advertisement`), Commercial-Teaser (`app-commercial-teaser`, `app-commercial-teaser-group`), Artikel-Empfehlungen (`app-related-content-teaser-group`, `app-storyline-related-content`), Google-Preferred-Source-Promo (`app-google-preferred-source`), VG-Wort-Tracking (`app-vg-wort`), Footer (`app-footer`, `app-detail-page-footer`, `app-detail-page-content-footer`, enthält u. a. Outbrain-Empfehlungen). Bewusst **nicht** geblockt: `app-storyline-podcast` – im Testartikel ein zum Artikel gehöriger WiWo-Podcast-Beitrag (Audio-Player im Artikel bleibt laut Kernregel immer sichtbar).
- **9to5mac.com**: „Best … accessories"-Affiliate-Box am Artikelende (Amazon-Produktliste mit Google-Preferred-Source-Badge und Werbe-Disclaimer) entfernt. Überschrift ist textabhängig auf das nachfolgende Muster gepinnt (`h3.wp-block-heading:has(+ ul.wp-block-list + div.google-preferred-source-badge)`), damit reguläre Zwischenüberschriften im Artikel nicht betroffen sind.

---

## [2026-06-16] - spiegel.de: Tipico-Sportwetten aus Spielbanner entfernt

### Hinzugefügt
- **spiegel.de**: Tipico-Sportwetten-Teile aus dem Spiel-/Match-Banner („Die nächsten Top-Spiele", bei WM oben, bei der Bundesliga mittig) entfernt. Das Banner ist ein Heimspiel-Widget-Iframe von `sportdaten.spiegel.de`; die Regeln sind auf diese Iframe-Domain gescoped. Entfernt werden die Tipico-Quoten-Boxen (`.hs-ad`, je ein Wett-Iframe pro Match) und der Glücksspiel-Disclaimer (`#legal-notice`, „10€ Einsatz | 18+ | … | Nur für Neukunden"). Das Banner selbst – Flaggen, Teamnamen, Anstoßzeiten – bleibt erhalten.

---

## [2026-06-16] - spiegel.de: Overblocking behoben, Verschenken-Button bleibt

### Behoben
- **spiegel.de**: Overblocking von `section[data-area="html-embed"]` behoben – die Regel (für die Newsletter-Box gedacht) hat auch legitime Inhalte versteckt: Scrollytelling-Bildstrecken mit eingeblendeten Bildunterschriften und Video-Embeds. Selektor jetzt auf das Newsletter-Iframe (Gruppenkonto) eingeschränkt (`section[data-area="html-embed"]:has(iframe[src*="gruppenkonto"])`); die Newsletter-Box bleibt geblockt.
- **spiegel.de**: Artikel-Toolbar-Regel verfeinert – der „Artikel verschenken"-Button bleibt jetzt sichtbar, während die übrigen Toolbar-Items (Merkliste, Anhören, X, Facebook, E-Mail, Link kopieren, mobiles Share-Menü) weiterhin versteckt werden (`[data-area="feature-bar"] li:not(:has(button[title="Artikel verschenken"]))`).

---

## [2026-06-14] - README: Vivaldi-Kompatibilität korrigiert

### Behoben
- **README.md**: Die Angabe, noise-killer funktioniere in Vivaldi über den eingebauten Werbeblocker ohne Extension, war falsch. Vivaldis eingebauter Blocker macht nur Netzwerk-Blocking plus eine automatische Heuristik gegen Leerräume; er wendet **keine** Cosmetic-/Element-Hiding-Regeln (`##selector`, `:has()`) aus abonnierten Listen an (Vivaldi folgt ABP-Syntax ohne Cosmetic-Filtering). Da noise-killer ausschließlich aus Cosmetic-Filtern besteht, funktioniert die Liste in Vivaldi nur über eine Chromium-Extension (uBlock Origin / AdBlock Plus / AdGuard). Vivaldi-Abschnitt umgeschrieben; die frühere Annahme „gleiche adblock-rust-Engine wie Brave, daher ohne Extension nutzbar" entfernt (Brave wendet Cosmetic-Filter an, Vivaldis eingebauter Blocker nicht).

---

## [2026-06-14] - Google-Preferred-Source-Promos auf drei Seiten blockiert

### Hinzugefügt
- **sueddeutsche.de**: „SZ bei Google bevorzugen"-Promo im Artikel (Google-Preferred-Source-Link zu `google.com/preferences/source`). Der äußere Wrapper trägt 24px/16px-Margin und wird mitentfernt, damit kein Leerraum bleibt (`div:has(> div > a[href*="google.com/preferences/source"])`).
- **androidauthority.com**: „Don't want to miss the best from Android Authority?"-Box (Google-Discover-/Preferred-Source-Promo, `nc-disclosure-box`) im Artikeltext. Auf die `andauth.co/AAGoogle…`-Links im Content-Wrapper gepinnt; der Header-„Add on Google"-Button bleibt unberührt (`[data-content-wrapper="true"] > div:has(a[href*="andauth.co/AAGoogle"])`).
- **ndr.de**: „Machen Sie NDR.de zu Ihrer bevorzugten Nachrichten-Quelle bei Google"-Infobox am Artikelende. Auf den ARD-Einrichtungslink gepinnt, damit redaktionelle Infoboxen unangetastet bleiben (`div.contentbox.infobox:has(a[href*="ndr-bevorzugte-google-quelle"])`).

---

## [2026-05-23] - golem.de Chat-Bubble

### Hinzugefügt
- **golem.de**: ZipChat-Chat-Bubble / Coaching-Chat-Widget (Floating-Widget unten rechts, AI-Chat mit Coaching-/Karriere-Greetings, `#zipchat-shadow-host`)

---

## [2026-05-23] - heise.de Videos-Widget, transfermarkt.de Eigenwerbung & Kommentare, Vivaldi-Kompatibilität

### Hinzugefügt
- **heise.de**: „Videos by heise"-Eigenwerbungs-Widget im Artikeltext (Inline-Block mit „c't 3003 / heise & ct / Peertube"-Tabs und eingebetteten heise-Videos, `div.ad.ad--inread`)
- **transfermarkt.de**: „Transfermarkt Videos"-Eigenwerbungs-Box auf Spielerprofilen (`section.box`)
- **transfermarkt.de**: „Andere Spieler"-Empfehlungen in Hauptspalte und Sidebar (`#recommender`, `#recommender_sidebar`)
- **transfermarkt.de**: Kommentar-/Diskussions-Box am Profilende (`.player-discussions`)

### Geändert
- **README.md**: Vivaldi als unterstützten Browser ergänzt (Installations-Abschnitt für den eingebauten Tracker- und Werbeblocker sowie Hinweis, dass die Liste auch via uBlock Origin / AdBlock Plus / AdGuard-Extension in Vivaldi funktioniert). Die Cosmetic-Filter selbst sind unverändert kompatibel, da Vivaldis Built-in-Blocker auf derselben adblock-rust-Engine wie Brave basiert.

---

## [2026-05-13] - handelsblatt.com Google-Preferred-Source-Ribbon, lto.de Opinary-Umfrage

### Hinzugefügt
- **handelsblatt.com**: Google-Preferred-Source-Top-Ribbon „Legen Sie das Handelsblatt als Ihre wichtige Nachrichtenquelle fest" (`app-google-preferred-source`)
- **handelsblatt.com**: Inline-Artikel-Teaser im Fließtext (`app-storyline-element:has(> app-storyline-teaser)`)
- **lto.de**: Opinary-Live-Abstimmungs-Widget im Artikel (`div#opinary-root`)

---

## [2026-05-13] - faz.net Auto-Sprung zur Aktuell-Übersicht behoben

### Behoben
- **faz.net**: Auf Mobile sprang die Seite nach ca. 10–20 Sekunden ohne Nutzerinteraktion zur Aktuell-Übersicht (`/aktuell/#overscroll-article`), meist nach kurzem Scrollen im Artikel. Ursache: ein Overscroll-Sentinel am Artikelende wird per IntersectionObserver beobachtet; weil unsere Cosmetic-Filter Container unterhalb des Artikeltexts entfernen, rutschte der Trigger schon beim normalen Scrollen in den sichtbaren Bereich. Sentinel wird jetzt direkt entfernt (`#overscroll-article`, `[data-external-selector="overscroll-article"]`, `[class*="overscroll-article"]`).

---

## [2026-04-18] - rbb24.de hinzugefügt

### Hinzugefügt
- **rbb24.de**: Floating Social-Share-Bar (TikTok, Instagram, Facebook, YouTube etc., `.bottom-nav-article`)
- **rbb24.de**: Kommentar-Link und Social-Share im Artikel (`.interaction-bar`)
- **rbb24.de**: Inline Artikel-Empfehlung im Fließtext (`.container__article-component--small`)
- **rbb24.de**: Sendungshinweis am Artikelende (`.container__article-component:has(> .component-text > p > i)`)
- **rbb24.de**: Tag-Liste am Artikelende (`.container__article-component.tags`)
- **rbb24.de**: Kommentarbereich (`section.container.section--white.section--rounded`)
- **rbb24.de**: „Mehr bei rbb|24" Artikel-Empfehlungen (`section.section__stacked`)
- **rbb24.de**: Footer (`footer.footer`)

---

## [2026-04-15] - heise.de Autoren-Bio und Inline-Promo-Banner

### Hinzugefügt
- **heise.de**: Autoren-Bio-Box in der rechten Sidebar (`section.article-sidebar`)
- **heise.de**: Inline-Autoren-Dossier im Artikeltext – Mobile-Ansicht (`.js-dossier`)
- **heise.de**: Inline-Promo-/Hinweis-Banner im Artikelkopf (`details.notice-banner`)

---

## [2026-04-14] - lto.de Podcast-Player, Newsletter, Tags; t-online.de Inline-Teaserboxen

### Hinzugefügt
- **t-online.de**: Inline-Artikelteaser im Fließtext (Magenta-Aufzählung mit Artikellinks, `StageLayout.StreamItem:has(> ul[class*="before:bg-magenta"])`)
- **t-online.de**: Post-Artikel-Teaserboxen nach dem Artikelende (`StageLayout.StreamItem:has(> article)`)
- **t-online.de**: Taboola-Feed (`TaboolaFeed`, `TaboolaFeeds.Feed`)

---

## [2026-04-14] - lto.de Podcast-Player, Newsletter, Tags

### Hinzugefügt
- **lto.de**: Inline-Podcast-Player (letscast.fm-Embed) blockiert (`div:has(> script[src*="letscast.fm"])`)
- **lto.de**: Newsletter-Anmelde-Boxen (`.newsletter-subscription-block`)
- **lto.de**: Schlagwort-Tags am Artikelende (`ul.tags`)

---

## [2026-04-08] - iphone-ticker.de / ifun.de Startseiten-Noise, raider.io Eigenwerbung

### Hinzugefügt / Behoben
- **iphone-ticker.de**: Startseiten-Noise ergänzt – Share-Buttons pro Artikel (`#viewport-share`), Kommentar-Badges (`.comments-block`, `.comments-block-mobile`), Google-Ad-Platzhalter (`.consumernotice`).
- **ifun.de**: Gleiche Ergänzungen wie iphone-ticker.de (identische Plattform).
- **raider.io**: Umfangreiche Erweiterung der bestehenden Filter –
  - Adblock-Modal-Box (`.adblock-modal`) ergänzt (Overlay war schon blockiert)
  - „Raider.IO News"-Sidebar + Support-Plea (`.rio-sidebar-section`)
  - „Get App & AddOn"-CTA-Button (`button.slds-button--raiderio-gradient`)
  - Inline-Promo-Zeilen in der Rankings-Tabelle (`tr:has(> td.rio-simple-table-cell)`)
  - Promo-Banner über der Rankings-Tabelle (`#content .slds-col.slds-size--1-of-1 > div > .slds-m-bottom--small`)
  - Startseite: Merch-Banner + YouTube-Embed (`.rio-right-pane > section`), 3× „Support Raider.IO"-Plea (`.slds-text-align--center.slds-m-vertical--large`), Guild-Recruitment (`.rio-recruitment-pane`), „Midnight is upon us"-Promo 2× (`#content .slds-m-top--large:has(.slds-button--raiderio)`), Selbstbeschreibungs-Blurb (`.slds-grid.align-justify`)

---

## [2026-04-06] - raider.io hinzugefügt, t-online.de Schlagzeilen-Fix

### Hinzugefügt
- **raider.io**: Footer (`.rio-footer--bg`), Cookie-Consent-Banner (`.cookie-footer--wrapper`) und Adblock-Erkennungs-Modal (`.adblock-modal__overlay`) blockiert.

### Behoben
- **t-online.de**: Schlagzeilen-Inline-Box war nicht blockiert – Selektor `div.rounded-8.bg-alpine.p-12` traf falschen Tag (Element ist ein `aside`). Ersetzt durch `aside[data-testid="Stage.Schlagzeilen.Inline"]`.

---

## [2026-04-04] - startpage.com hinzugefügt

### Hinzugefügt
- **startpage.com**: App-Promo (Hamburger-Menü + Hero-Widget), Browser-Extension-Promo, Blog/Newsletter-Menü-Button, Marketing-Tagline und alle Marketing-Sektionen unterhalb der Suchleiste (Homepage) blockiert. Auf der Suchergebnisseite: Support-Banner, Feedback-Widget und Extension-Installations-Toast blockiert. Footer blockiert. Nur Suchleiste, Kategorien und Einstellungen bleiben sichtbar.

---

## [2026-04-03] - heise.de pvg-widget, theverge.com: Follow-Buttons, Subscribe, Autoren-Bio, Inline-Related

### Behoben
- **heise.de**: Inline-Preisvergleich-Shop-Box (PVG-Widget, `.pvg-widget`) blockiert – iframe-basierter Preisvergleich auf bestenlisten/testbericht-Seiten.

### Hinzugefügt
- **theverge.com**: Topic/Autoren-Follow-Buttons (○-Kreise neben Themen-Tags und in der Byline) blockiert (`aside[id^="popover-"]`). Subscribe-Button in der Top-Navigation blockiert (`a[href="/subscribe"]`). Autoren-Bio-Box unterhalb des Artikel-Bildes blockiert (`.duet--ledes--standard-lede-bottom`). Inline-„Related"-Artikel-Box im Artikeltext blockiert (`.duet--article--related`).

---

## [2026-04-01] - tagesschau.de Neubau, lto.de "Mehr zum Thema"

### Hinzugefügt
- **tagesschau.de**: Filter komplett neu aufgebaut. Bild-Overlap (Artikel + Startseite) behoben via `:style(padding-bottom: 56.25%)` auf `.article-head__media` / `.teaser__media`. Weitere Noise-Elemente blockiert: Inline-Video-Teaser (`.copytext-element-wrapper--overlap`), Sendungshinweis (`.meldungsfooter`), Backlink (`.backlink`), "Mehr zum Thema"-Aside, Artikel-End-Buttons, ARD-Konto-Promo, Footer.
- **lto.de**: „Mehr zum Thema"-Tag-Links am Artikelende blockiert (`.article-text-wrapper > nav`).

---

## [2026-03-30] - Bugfixes & neue Filter: 5 Domains

### Behoben
- **stadt-bremerhaven.de**: `replace-node-text`-Scriptlets entfernt – zerstören Seitenstruktur durch XPath-Auswertung auf Script-Inhalte. Bare-Text-Knoten bleiben ohne Fix (CSS-seitig nicht targetierbar).
- **faz.net**: Inline-Newsletter-Box und „Verlagsangebot"-Marktplatz-Widget jetzt via äußerem Wrapper `[data-external-selector="html-element"]` blockiert (statt nur `#nl_footer_widget`).
- **spiegel.de**: „Geschichten, die wir Ihnen heute empfehlen:" – redaktionelle Empfehlungsbox im Artikeltext blockiert.

### Hinzugefügt
- **heise.de**: Affiliate-Inline-Werbung auf Bestenlisten-Testberichten blockiert (`gridWidgetTypeAffiliateLink`, `gridWidgetTypeTrackonomics`, `gridWidgetTypeStoryPriceAndRating`, `gridWidgetTypeBestenlistenRelatedBox`).
- **tagesschau.de**: Vorleseplayer („Artikel anhören", `div.mediaplayer--teaser-top.mediaplayer--audio`) blockiert.

---

## [2026-03-28] - Bugfixes: faz.net / spiegel.de / stadt-bremerhaven.de

### Behoben
- **faz.net**: Newsletter-Footer-Box (`#nl_footer_widget`) blockiert – via avenga.snacks dynamisch gerendert (`data-fsw="newsletterpromote"`).
- **faz.net**: Artikel-Toolbar (`aside[data-external-selector="upper-toolbar"]`) blockiert – Anhören / Merken / Teilen / Drucken / Zusammenfassung – auf expliziten Nutzerwunsch.
- **spiegel.de**: Inline-Newsletter-Box (`section[data-area="html-embed"]`) blockiert – Gruppenkonto-Iframe eingebettet im Artikeltext.
- **stadt-bremerhaven.de**: Nackte Textknoten „Dann teile ihn mit deinen Freunden." und „Mit dem Absenden eines Kommentars stimmst du unserer … und der Speicherung … Daten zu." per uBlock Origin `+js(replace-node-text)` entfernt – CSS-seitig nicht targetierbar; Brave bleibt ohne Fix.

---

## [2026-03-27] - Bugfix tagesschau.de Inline-Teaser und Buttongroup

### Behoben
- **tagesschau.de**: `copytext-element-wrapper--overlap` korrekt wieder aktiviert – sind Related-Content-Teaser-Player (Audio/Video fremder Artikel inline zwischen Absätzen), kein Artikelinhalt. `copytext__video` (Inline-Video des eigenen Artikels mit schema.org-Markup) bleibt weiterhin ungeblockt.
- **tagesschau.de**: `buttongroup`-Selector tag-agnostisch gemacht (`.buttongroup` statt `ul.buttongroup`) – Element ist je nach Artikel ein `div` oder `ul`.

---

## [2026-03-27] - Bugfix tagesschau.de Startseite- und Kommentare-Button

### Behoben
- **tagesschau.de**: Startseite- und Kommentare-Button am Artikelende wurden nicht blockiert. `div.buttongroup` hat nie gematcht – das Element ist ein `ul`, kein `div`. Fix: `ul.buttongroup` (Tag korrigiert, `>` Direktkind-Selector bleibt korrekt).

---

## [2026-03-27] - androidauthority.com / focus.de hinzugefügt

### Hinzugefügt
- **androidauthority.com**: Sidebar (`aside`), Footer (`footer`), Kommentarsektion (`#comments-section`), Deal-Promo-Bar (`#__next > div:has(a[href*="andauth.co"])`), Affiliate-Disclaimer, Tag-Liste, Follow-Widget und „Join the conversation"-Prompt (Viafoura) blockiert.
- **focus.de**: Kommentar-Button (`div.Article-Comments-Button`), Kommentarsektion (`div.Article-Comments`), Partnerangebote-Box (`div.Article-LinkBox`), Opinary-Widget (`#opinary-root`) und Footer (`footer`) blockiert. Live-Ticker-Einträge bleiben unangetastet.

---

## [2026-03-27] - nytimes.com hinzugefügt

### Hinzugefügt
- **nytimes.com**: Related-Content-Bereich (`section[data-testid="recirculation-placeholder"]`), „More on…"-Themen-Guide (`article#story > div:has(> div > section#styln-guide)`), Site-Index-Navigation (`nav#site-index`) und Footer (`footer`) blockiert.

---

## [2026-03-22] - 9to5mac.com hinzugefügt / Wikipedia auf alle Sprachversionen erweitert

### Hinzugefügt
- **9to5mac.com**: Alle Filter von 9to5google.com übertragen (identisches Theme).
- **wikipedia.org**: Regeln auf alle Sprachversionen ausgeweitet (`wikipedia.org` statt einzelner Subdomains).

---

## [2026-03-22] - Bugfixes: 9to5google.com / stadt-bremerhaven.de / spiegel.de / faz.net

### Behoben
- **9to5google.com**: Infinite-Scroll-Trigger (`#infinite-handle`) und Lade-Spinner (`div.infinite-loader`) blockiert – verhinderte, dass der Loader immer wieder neue Artikel nachlud.
- **9to5google.com**: „Follow Ben: Twitter/X, Threads, Bluesky, and Instagram" blockiert (`p:has(> em:only-child)`).
- **stadt-bremerhaven.de**: Redaktionelle Inline-Werbung (WordPress-oEmbed-Artikel-Teaser) blockiert (`div.video-container:has(> blockquote.wp-embedded-content)`).
- **stadt-bremerhaven.de**: Tag-Liste am Artikelende blockiert (`p.post-tags`).
- **spiegel.de**: Affiliate-Produktboxen im Artikeltext blockiert – Disclaimer-Box (`aside[data-area="contentbox"]`), Produkt-Liste (`section[data-area="contentbox"]`) und individuelle ANZEIGE-Boxen pro Produkt (`div[data-area="heise-widget"]`).
- **faz.net**: Social-Share-Leiste (`div.tik4-sharing`) unter einzelnen Live-Ticker-Einträgen blockiert.
- **faz.net**: Opinary-Inline-Umfrage-Widget (`iframe.opinary-iframe`) im Artikeltext blockiert.

## [2026-03-22] - 9to5google.com / macrumors.com / amazon.de / en.wikipedia.org

### Hinzugefügt
- **9to5google.com**: Featured-Sidebar (`aside.sidebar`) blockiert – Artikel-Karussell rechts neben dem Artikel.
- **9to5google.com**: Kommentar-Link in der Byline (`a.comments`) blockiert.
- **9to5google.com**: Kommentarsektion (`#comments`) blockiert.
- **9to5google.com**: „Guides"-Box (`div.related-guides`) blockiert.
- **9to5google.com**: Author-Bio-Box (`div.author-bio`) blockiert.
- **9to5google.com**: YouTube-Kanal-Promo (`div.article__youtube-video`) – „Check out 9to5Google on YouTube for more news" – blockiert.
- **9to5google.com**: Infinite-Scroll-Artikel (`[id^="infinite-view-"]`) blockiert – weitere Artikel die unter dem aktuellen Artikel nachladen.
- **9to5google.com**: „More on Android/Chrome/…"-Abschnitt (`h2[id^="h-more-on-"]` + folgende `ul`) blockiert.
- **amazon.de**: Footer (`#navFooter`) blockiert – ersetzt die bisherigen Einzelfilter `#nav-ftr-gototop` und `#nav-ftr-links`.
- **amazon.de**: Empfehlungs-Carousels (`[id^="sims-"]`) blockiert – „Wird oft zusammen gekauft", SIMS-Ähnlichkeits-Container.
- **amazon.de**: Prime-Video/Promo-Banner (`#prime-desktop-dp_feature_div_01`) blockiert.
- **en.wikipedia.org**: Footer (`div.mw-footer-container`) blockiert – „This page was last edited…" + Links zu Privacy Policy, About, Disclaimers.

### Behoben
- **macrumors.com**: `div[role="main"] > div` hat nie gegriffen – kein Element mit `role="main"` vorhanden (React-App). Ersetzt durch `#maincontent > div` (Newsletter-Box, „Popular Stories", Kommentarsektion).
- **macrumors.com**: `div.linkback` ergänzt – „Related Roundups" / „Related Forum"-Links im Artikeltext.
- **macrumors.com**: `.js-article .noskim` ergänzt – Artikel-Footer mit „[ 100 comments ]"-Link.
- **macrumors.com**: `#canvas-sidebar` ergänzt – Slide-Panel mit Videos/Guides/Upcoming/Other-Stories-Widgets.

## [2026-03-20] - faz.net / spiegel.de / sueddeutsche.de: Live-Ticker & FAZ-Promo

### Behoben
- **faz.net**: F.A.S.-Sonntagszeitung-Eigenwerbung im Artikeltext – „Dieser Text stammt aus der Frankfurter Allgemeinen Sonntagszeitung" + „F.A.S. jetzt lesen"-Button. Nur für Abonnenten sichtbar; Selector über `zeitung.faz.net`-Link innerhalb `body-elements-container`.
- **spiegel.de**: Social-Share-Leiste (`div.tik4-sharing`) in Tickaroo-Liveblog-Einträgen – „Teilen: [Link] [Facebook] [X] [Mail]" unter jedem Ticker-Beitrag.
- **sueddeutsche.de**: Redaktionelle Artikel-Links (`div.tik4-link-list`) im Tickaroo-Liveblog – „Mehr zum Krieg in der Ukraine" mit verlinkten Artikeln.
- **sueddeutsche.de**: Social-Share-Leiste (`div.tik4-sharing`) in Tickaroo-Liveblog-Einträgen ergänzt (analog spiegel.de).

## [2026-03-19] - handelsblatt.com: Leerraum + „Mehr:"-Links

### Behoben
- **handelsblatt.com**: `app-storyline-element:not(:has(*))` – komplett leere Wrapper-Elemente (Angular rendert sie mit `<!---->` ohne Inhalt, aber `spacer-top-l` gibt 40px Margin) erzeugen Leerraum zwischen Absätzen.
- **handelsblatt.com**: `app-storyline-element:has-text(/^Mehr:/)` – „Mehr:"-Eigenwerbungslinks (z. B. „Mehr: Verfolgen Sie alle Entwicklungen im Iran-Krieg hier im Newsblog") blockiert.

## [2026-03-19] - handelsblatt.com: Leerraum zwischen Absätzen (Embed-Wrapper)

### Behoben
- **handelsblatt.com**: `app-storyline-element:has(> app-storyline-embed)` – `app-embed` blockt bereits den Embed-Inhalt, aber der äußere `app-storyline-element`-Wrapper (`display: grid`, `marginTop: 40px`) blieb mit seinem Margin im Flow und erzeugte Leerraum zwischen Textabsätzen.

## [2026-03-19] - handelsblatt.com: Artikel-Noise-Ergänzungen

### Hinzugefügt
- **handelsblatt.com**: `app-commercial-teaser` (Einzel-Werbe-Teaser, bisher nur Group blockiert).
- **handelsblatt.com**: `app-detail-page-content-footer` (sichtbar, h:105) – enthält Google-Preferred-Source-Eigenwerbung („Handelsblatt als Nachrichtenquelle bei Google") und Redaktionskontakt-Link.
- **handelsblatt.com**: `app-follow-topic-button` – „Folgen"-Buttons unter Themen-Tags.
- **handelsblatt.com**: `app-related-topics` – Verwandte-Themen-Box mit Follow-Buttons am Artikelende.
- **handelsblatt.com**: `app-special-advertisement` – Sonderwerbeformat.
- **handelsblatt.com**: `app-storyline-advertisement` – Inline-Werbung innerhalb des Artikeltexts.
- **handelsblatt.com**: `app-storyline-related-topics` (vereinfacht von `.ng-star-inserted`-Variante).
- **handelsblatt.com**: `app-vg-wort` – VG-Wort-Tracking-Pixel (h:105 durch CSS-Margins trotz unsichtbarem Inhalt).

## [2026-03-19] - sueddeutsche.de: „Zur SZ-Startseite"-Button

### Behoben
- **sueddeutsche.de**: „Zur SZ-Startseite"-Button am Artikelende (`a.lp_is_end`) blockiert.

## [2026-03-19] - sueddeutsche.de: IframelyEmbed-Leerraum im Artikel

### Behoben
- **sueddeutsche.de**: Leerer Iframely-Embed-Wrapper (`div[data-testid="IframelyEmbed"]:not(:has(iframe))`) erzeugte 120px Leerraum zwischen Textabsätzen (je 60px `margin-top` und `margin-bottom` trotz h:0). Nur ausgeblendet wenn kein `<iframe>` geladen wurde – bei funktionierenden Embeds bleibt der Inhalt sichtbar.

## [2026-03-19] - sueddeutsche.de Bugfixes: Karussell-Leerräume + Trennlinien

### Behoben
- **sueddeutsche.de**: `div[data-manual-remove]` auf `[data-manual-remove]` erweitert – greift jetzt auch bei `section`-Karussell-Elementen, die SZ's eigenes JS via `data-manual-remove="true"` versteckt.
- **sueddeutsche.de**: Äußere Separator-Wrapper (je h:48 + zwei Trennlinien) werden jetzt mitgeblockt: `.szde-homie-page-content__separator-item--both:has(> [data-manual-remove])` – vorher blieben die leeren Wrapper-Divs mit ihren CSS-Trennlinien als Freifläche sichtbar.

## [2026-03-19] - sueddeutsche.de Bugfixes: SZ-Shop + Leerraum-Freiflächen

### Behoben
- **sueddeutsche.de**: SZ-Shop-Banner zusätzlich via `#meineSZ` (innere Div-ID) blockiert – Fallback falls `[data-qa="meine_sz"]`-Filter nicht greift.
- **sueddeutsche.de**: Zwei h:168-Leerraum-Freiflächen behoben: `[data-qa="misch_teaser_group"]:not(:has(article))` blockiert Bild-only Teaser-Gruppen (SZ-Erleben-Shop-Promo + Streiflicht-Kolumnen-Promo) ohne redaktionellen Artikel-Inhalt.

## [2026-03-19] - sueddeutsche.de Deep-Audit Startseite

### Hinzugefügt
- **sueddeutsche.de**: SZ-Shop-Banner + Gutschein-Slider (`[data-qa="meine_sz"]`) blockiert – lädt per `h-include-lazy` als Fragment und enthält SZ-Shop-Werbebanner sowie Affiliate-Gutschein-Slider.
- **sueddeutsche.de**: Separates Gutschein-Widget (`[data-qa="voucher_widget"]`) blockiert.
- **sueddeutsche.de**: SZ-Stellenmarkt-Eigenwerbung (`[data-qa="stellenmarkt"]`) blockiert.
- **sueddeutsche.de**: Outer-Wrapper aller Personalisierungs-Gruppen (`[data-qa^="personalization_group_hp_"]`) blockiert – bisheriger Filter (`section[data-testid^="personalization-group"]`) entfernte nur den inneren Inhalt; der äußere Wrapper mit Trennlinien (h:48) blieb als Freifläche sichtbar.

## [2026-03-19] - Startseiten-Audit: 5 Sites

### Hinzugefügt
- **sueddeutsche.de**: Stellenanzeigen-Eigenwerbungsbox (`aside.sz-disable-dark-mode`) blockiert.
- **sueddeutsche.de**: „Für Sie ausgewählt"-Empfehlungsbox (`section[data-testid^="personalization-group"]`) blockiert.
- **spiegel.de**: SPIEGEL+ Newsletter-Brief-Promo (`section[data-area="block>magletterarticles"]`) auf der Startseite blockiert.
- **faz.net**: „Folgen Sie uns"-Social-Follow-Bar (`section.nw-htmlbar.social`) blockiert.
- **faz.net**: Newsletter-Slider-Iframe (`#iframenewsletterslider`) blockiert.
- **tagesschau.de**: „Ihr ARD-Konto"-Eigenwerbungsbox (`div.promo-box.promo-box--highlight`) blockiert.

### Behoben
- **tagesschau.de**: `div.buttongroup` war zu breit – blockierte auf der Startseite Navigations-Buttons wie „Weitere Inlandsnachrichten". Auf Artikel-Kontext beschränkt: `div.content-wrapper__group > div.buttongroup`.
- **computerbase.de**: Shoutbox-Filter deckte nur Artikel-Variante (`--article-view`) ab. Vereinfacht auf `div.shoutbox-container` (deckt alle Varianten inkl. `--homepage`).

## [2026-03-19] - spiegel.de Toolbar + tagesschau.de Artikel-Link-Box

### Hinzugefügt
- **spiegel.de**: Artikel-Toolbar (Lesezeichen/Teilen, `[data-area="feature-bar"]`) blockiert – auf expliziten Nutzerwunsch.

### Behoben
- **tagesschau.de**: Artikel-Link-Box am Artikelende nicht blockiert. Element ist `ul.buttongroup.buttongroup--copytext` (ein `UL`, kein `DIV`) – bisheriger `div.buttongroup`-Filter griff nicht. Fix: `div.copytext-element-wrapper:has(ul.buttongroup--copytext)` blockiert den gesamten Wrapper inkl. Trennlinien.

## [2026-03-18] - Bugfix gamestar.de: Empfohlen-Box nicht blockiert

### Behoben
- **gamestar.de**: „Empfohlen"-Box oben rechts (`div.contentteaser.row.box.contentitem-box`) nicht blockiert – dritte contentteaser-Variante ergänzt.

## [2026-03-18] - Bugfix gamestar.de: Unter-Startseiten leer

### Behoben
- **gamestar.de**: `div.contentteaser.row.box` hat auch `contentnewsitem-box` geblockt – Artikel-Listings auf Unter-Startseiten (z.B. `/news/spiele/`) wurden komplett geleert. Aufgeteilt auf `div.contentteaser.row.box.chartteaser-box` (Top-Artikel) und `div.contentteaser.row.box.contentmediaitem-box` (Aktuelle Artikel).

## [2026-03-18] - Bugfix gamestar.de: BoostBoxx-Buttons und Werbeboxen

### Behoben
- **gamestar.de**: Grüne BoostBoxx-Schaltflächen (`a[href*="boostboxx"]`) und „Warum einen GameStar Gaming-PC von BoostBoxx?"-Werbeboxen (`div.custom-info`) blockiert. `div.wp-block-wbd-affiliate-widget` deckte nur die Produkt-Slider ab, nicht die einzelnen Button-Links im Artikeltext.

## [2026-03-18] - Globale Outbrain- und Taboola-Blocker

### Hinzugefügt
- **Global**: Outbrain-Widget (`div.OUTBRAIN`, `[id^="outbrain"]`) siteübergreifend blockiert.
- **Global**: Taboola-Widget (`[id^="taboola"]`, `div[class^="trc_"]`) siteübergreifend blockiert.

## [2026-03-18] - gamestar.de: Inline Affiliate-Produkt-Slider blockiert

### Hinzugefügt
- **gamestar.de**: Inline Affiliate-Produkt-Slider (`div.wp-block-wbd-affiliate-widget`) blockiert – WordPress-Blöcke mit Preisen und grünen „Zum Shop"-Buttons, direkt im Artikeltext eingebettet.

## [2026-03-18] - Bugfixes + Erweiterung gamestar.de

### Behoben
- **gamestar.de**: `div:has(> h3:has-text(/auch spannend/i))` hat nie gegriffen – Titel steht in `div.title`, nicht `h3`. Ersetzt durch `div.recirculation-box` (deckt alle Varianten: „Auch spannend", „Mehr zum Thema", „Aktuelle GameStar PC-Highlights", „Zu allen Special Editions" u.a.).

### Hinzugefügt
- **gamestar.de**: Author-Bio-Box (`div.author-box`) blockiert.
- **gamestar.de**: Eigenwerbungs-Popup „GameStar hat noch mehr für dich!" (`#inactivity-popup`) blockiert.
- **gamestar.de**: Outbrain-Empfehlungswidget (`div.OUTBRAIN`) blockiert.
- **gamestar.de**: Unterer „zu den Kommentaren"-Link (`a[href="#comments"]`) blockiert.

## [2026-03-18] - Bugfix mydealz.de: Ähnliche Gutscheine

### Behoben
- **mydealz.de**: „Ähnliche Gutscheine"-Box wurde nicht blockiert. `has-text()` mit Umlaut war unzuverlässig. Selector auf `div.bRad--a.bg--main.space--mt-2` umgestellt (exklusive Klasse dieser Box).

## [2026-03-18] - ndr.de: Sendungshinweis und untere Breadcrumb blockiert

### Behoben
- **ndr.de**: Sendungshinweis „Dieses Thema im Programm" (`div.relatedbroadcast`) und untere Breadcrumb-Navigation (`nav#breadcrumb`) am Artikelende blockiert.

## [2026-03-18] - Bugfixes: arstechnica, tagesschau, pcgameshardware, gamestar (Affiliate/Shop)

### Behoben
- **arstechnica.com**: Author-Box blockiert nicht vollständig. Selector geändert von `div:has(> a[href*="/author/"])` zu `div.author-mini-bio` (blockiert komplette Bio-Box inkl. Avatar und Text).
- **tagesschau.de**: "Zur Startseite"-Button nicht blockiert. Selector war `ul.buttongroup`, aber Element ist `div.buttongroup`.
- **pcgameshardware.de**: Comment-Sprechblase am Anfang und Ende nicht blockiert. `div.commentIcon` ergänzt.
- **gamestar.de**: Inline-Werbung "Auch spannend" nicht blockiert. `div:has(> h3:has-text(/auch spannend/i))` ergänzt.
- **gamestar.de** (erweitert): Affiliate- und Shop-Werbung auf Produktseiten (z.B. Crimson Desert). `div.offerteaser-box` (GameStar PC Shop-Box) und `div.affiliate-buttons` (GamesPlanet Affiliate-Links) ergänzt.

## [2026-03-18] - Bugfixes: mydealz.de, n-tv.de, ndr.de, stadt-bremerhaven.de

### Behoben
- **mydealz.de**: „Ähnliche Gutscheine"-Abschnitt blockiert via `[data-t="main"] div:has(> h3:has-text(/Gutschein/))`.
- **n-tv.de**: Artikel-Tags am Artikelende blockiert (`[class*="article-detail-footer_tags"]`); CSS-Grid-Wrapper per `:style(display:block)` auf Block-Layout gesetzt, damit der rechte Leerraum (reservierte Grid-Spalte für die blockierte Aside) kollabiert.
- **ndr.de**: Artikel-Tags am Artikelende blockiert (`div.tagbox`).
- **stadt-bremerhaven.de**: Whitespace-Fix verbessert – `max-width: 100% !important` zur `:style()`-Injection ergänzt, um hartcodierten `max-width`-Wert zu überschreiben.

## [2026-03-18] - Bugfixes: ifun.de, iphone-ticker.de, mydealz.de komplett neu

### Behoben
- **ifun.de / iphone-ticker.de**: `#article-single-stats` ergänzt – enthält Kommentar-Link und Mastodon-Share-Button am Artikelanfang.
- **mydealz.de**: Kompletter Neuaufbau. `div.stickyBar-bottom` und `section[role][data-t]` nicht mehr gefunden (Redesign). Neue Selektoren auf Basis stabiler `data-t`-Attribute: Kommentare, Related Deals, Share-Button, Subscribe, Keyword-Widget, Vote-Erklärung, internalLinking, App-Download und Footer blockiert.

## [2026-03-18] - Bugfixes: pcgameshardware.de, gamestar.de, derstandard.de, handelsblatt.com

### Behoben
- **pcgameshardware.de**: `##footer` blockierte nichts (kein `<footer>`-Element vorhanden). Footer ist `div.header2.footer3`; Print/Abo-Werbung in `ul.rowAlt.footer2` ergänzt.
- **gamestar.de**: `div.contentteaser.row.box.contentmediaitem-box` deckte nur „Beliebt"/„Aktuell" ab, nicht „Empfohlen" (`contentitem-box`). Selector vereinfacht auf `div.contentteaser.row.box`. `a.do-toggle-comments` (Kommentar-Link im Artikelkopf, außerhalb `#comments`) und `ul.taglist` (Artikel-Tags) ergänzt.
- **derstandard.de**: Eigenständige Domain (`.de`) hatte keine Filter. Alle Selektoren von `derstandard.at` gespiegelt. `a.article-postingcount` (Posting-Count-Button im Artikelkopf) für beide Domains ergänzt. `div.story-tool` (floating Panel mit Posting-Count + Social-Share-Buttons inkl. Bluesky) für beide Domains ergänzt.
- **handelsblatt.com**: `app-embed.ng-star-inserted > app-iframe > iframe` ließ den äußeren Container sichtbar (leere Newsletter-Box). Vereinfacht auf `app-embed`.

## [2026-03-18] - Bugfix: tagesspiegel.de Opinary-Widget

### Behoben
- **tagesspiegel.de**: Opinary-Widget renderte sich trotz geblockem `#opinary-automation-placeholder` neu in `#opinary-root` + `#opinary-iframe`. Beide IDs ergänzt.

## [2026-03-18] - Bugfixes: tarnkappe.info, tagesspiegel.de, t-online.de

### Behoben
- **tarnkappe.info**: `div.sonderwerbemittel` hat den gesamten Artikelbereich blockiert (wraps `#primary`). Entfernt.
- **tagesspiegel.de**: Floating Share-/Mail-Button (sticky `ul`) blockiert via `ul:has([data-gtm-class="article-social-link"])`; Themen-Buttons am Artikelende blockiert via `p:has(> a[data-gtm-class="article-home-link"]) ~ ul`; P mit „Zur Startseite"-Link nun komplett blockiert statt nur das A-Element.
- **t-online.de**: `div[data-testid="Page.PageStages"]` blockiert – enthält „Neueste Artikel"-Teaser, „Themen"-Pills und „Internationale Politik von A bis Z"-Navigation am Artikelende.

## [2026-03-18] - Umfangreiche Überarbeitung: 15 Sites gefixt und erweitert

### Behoben
- **arstechnica.com**: `main > div` hat alle Artikel-Gruppen auf der Startseite geblockt. Ersetzt durch `div.ad-wrapper`.
- **buffed.de**: Alle Selektoren außer `aside` nicht mehr gefunden (Redesign). Kritischer Filter `header.mainHeader` entfernt (hätte Site-Header geblockt). Nur bestätigte Selektoren behalten + `div.wadtag` ergänzt.
- **derstandard.de**: Domain-Fehler – korrekte Domain ist `derstandard.at`. `div.story-community-postings` nicht gefunden; ersetzt durch `section.story-community`.
- **golem.de**: `div.go-teaser-block` hat alle 25 Artikelgruppen auf der Startseite geblockt. Ersetzt durch gezielte Modifier-Selektoren (`--career`, `--carousel`, `--small-text`).
- **ndr.de**: `div.teaser` hat alle Artikel-Cards auf der Startseite geblockt (55 Elemente). Entfernt.
- **pcgameshardware.de**: Fünf veraltete Selektoren entfernt (nicht mehr gefunden nach Redesign). Ersetzt durch `aside.innerArticleModule`, `aside.column.right`, `aside.rec_box_bottom`.
- **tarnkappe.info**: `div > div > div[data-nosnippet]` hat Navigationsleisten geblockt. `div.column.is-one-third` hat alle Artikel-Cards auf der Startseite geblockt. Ersetzt durch präzise Selektoren.
- **taz.de**: `section > section` hat Artikel-Teaser-Sections auf der Startseite geblockt. Ersetzt durch `section.outerwrapper.contains-module-article > section:not([x-data])`.

### Hinzugefügt
- **arstechnica.com**: `#comments` (Kommentarsektion).
- **gamestar.de**: `#comments` (Kommentarsektion), `div.row:has(> .newsletter-form-container)` (Newsletter-Box).
- **handelsblatt.com**: `app-advertisement`, `app-content-advertisement` (Display- und Inline-Werbung), `app-detail-page-footer` (Artikelfooter mit Outbrain).
- **heise.de**: Startseiten-Filter via `data-component`: `NewAdModule`, `MarketingTeaserModule`, `HeiseJobsModule`, `PreisvergleichModule`.
- **ifun.de**: `#article-single-comments` (Kommentarsektion).
- **iphone-ticker.de**: `#article-single-comments` (Kommentarsektion).
- **n-tv.de**: `section[class*="widget-teaser"]` (Teaser-Widgets), `div[class*="social-share"]` (Social-Share-Bar).
- **steamdb.info**: `a.support-above-footer` (Support-Button über dem Footer).
- **stadt-bremerhaven.de**: CSS-Injection `div.main-inner.group > div.content:style(width: 100% !important; float: none !important)` – behebt Leerraum rechts nach Sidebar-Blockierung.
- **t-online.de**: `aside[data-testid="StreamLayout.Companion"]` (rechte Sidebar), `div[data-testid="nativendo-container"]` (Native Ads), `div[data-testid="Commercial.SDI"]` (Werbeplatz), `div[data-testid="PageFooter"]` (Footer).
- **tagesspiegel.de**: `#opinary-automation-placeholder` (Meinungsumfrage-Widget), `#outbrain-container` (Outbrain-Empfehlungen), `button[data-gtm-class="open-community"]` (Kommentare-Button), `a[data-gtm-class="article-home-link"]`, `footer`.
- **derstandard.at**: `section.story-recommended` (Taboola-Empfehlungen).

## [2026-03-18] - The Verge Kommentare + Follow-Widget

### Hinzugefügt
- **theverge.com**: Kommentar-Links (`duet--article--comments-link`), „12 Comments"-
  Schaltfläche am Artikelende (`#zephr-anchor > span`) und „Follow topics and authors"-
  Widget (`#zephr-anchor > div:has(> span + ul)`) blockiert.

## [2026-03-18] - The Verge erweitert

### Hinzugefügt
- **theverge.com**: Native Anzeigen (`duet--ad--native-ad-linkset`, `duet--ad--native-ad-rail`),
  „Most Popular"-Sidebar (`duet--layout--rail`) und Newsletter-Abo-Box (`duet--cta--newsletter`)
  blockiert. Footer-Selector auf semantisches `duet--navigation--footer` präzisiert.

## [2026-03-18] - Spiegel Mobile-Bugfix Leerraum am Artikelende

### Behoben
- **spiegel.de**: Mobile Anzeigen-Container (`[data-advertisement~="mobile"]`) reservieren auf
  Mobilgeräten per CSS-Klasse `sm:min-h-632` bis zu 632px Leerraum, wenn keine Werbung lädt
  (z. B. bei Brave). Auf Desktop sind sie bereits durch Spiegels CSS verborgen. Filter
  `[data-advertisement~="mobile"]` entfernt die Platzhalter nun auch auf Mobile.
  Zusätzlich drei Klassen-Selektoren als Fallback für Brave (adblock-rust verarbeitet
  `data-advertisement`-Filter evtl. zu spät) und für ein Platzhalter-Div ohne Attribut:
  `[class~="sm:min-h-352"]`, `[class~="sm:min-h-492"]`, `[class~="sm:min-h-632"]`.

## [2026-03-18] - Spiegel Mobile-Bugfix "Mehr lesen über" / "Verwandte Artikel"

### Behoben
- **spiegel.de**: `section[data-smartfeed-id="further-reads"]` blockierte auf Mobile
  nicht zuverlässig. Die Section ist im serverseitigen HTML sichtbar – Alpine.js versteckt
  sie nur auf Desktop. Filter auf element-agnostisch geändert
  (`[data-smartfeed-id="further-reads"]`) + innere Sections als Fallback ergänzt:
  `section:has(> h3:has-text(/^Mehr lesen über$/))` und
  `section:has(> h3:has-text(/^Verwandte Artikel$/))`.

## [2026-03-18] - Tagesschau Kommentare-Button

### Behoben
- **tagesschau.de**: `a.btn.btn--text.btn--standard-secondary.btn--fullwidth` hat nur
  den sekundären „Zur Startseite"-Button geblockt. Der primäre „Kommentare zur Meldung"-Button
  (`btn--standard-primary`) blieb sichtbar. Ersetzt durch `ul.buttongroup`, der die
  gesamte Buttongroup am Artikelende sauber entfernt.

## [2026-03-17] - Spiegel Bugfix "Mehr lesen über"

### Behoben
- **spiegel.de**: `section:has(> h3:has-text(/^Mehr lesen über$/))` hat nur
  die innere Section getroffen, nicht den äußeren Container – „Mehr lesen über"-Box
  blieb sichtbar und hinterließ einen großen Whitespace. Ersetzt durch
  `section[data-smartfeed-id="further-reads"]`, der den kompletten Container
  sauber entfernt.

## [2026-03-17] - Deutschlandfunk hinzugefügt

### Hinzugefügt
- **deutschlandfunk.de**: Footer (footer.b-footer) blockiert
