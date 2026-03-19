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
