# Pokémon Vault – lokale Web-App

## Starten
1. `index.html` mit einem aktuellen Browser (Chrome, Edge, Firefox) öffnen.
2. Für OCR braucht die App eine Internetverbindung, da Tesseract.js bei Bedarf von jsDelivr geladen wird.
3. Fotos und Karten werden in IndexedDB im aktuellen Browserprofil gespeichert. Sie werden nicht automatisch auf andere Geräte synchronisiert.
4. Regelmäßig über „Backup exportieren“ eine JSON-Sicherung speichern. CSV exportiert die Tabellendaten.

## Was funktioniert
- Kartenfoto hochladen und Vorschau anzeigen
- OCR/Texterkennung über Tesseract.js (Deutsch/Englisch), OCR-Text wird in Notizen übernommen
- Kartenname, Set, Kartennummer, Sprache, Variante, Zustand, Grading und Anzahl pflegen
- Preise für Cardmarket, Collectr und TCGplayer manuell eintragen
- Sammlungswerte und Anzahl berechnen
- Einträge bearbeiten/löschen, suchen/sortieren, JSON-Backup importieren/exportieren, CSV exportieren
- Links zu Cardmarket und TCGplayer öffnen

## Grenzen und sinnvoller nächster Schritt
- OCR ist keine echte Kartenidentifikation: sie kann sichtbaren Text extrahieren, aber nicht zuverlässig Set, Druck, Seltenheit oder Variante bestimmen. Vor dem Speichern bitte kontrollieren.
- Die App liest keine Live-Preise aus den Plattformen. Cardmarket erklärt, dass aktuell keine neuen API-Zugänge angenommen werden: https://help.cardmarket.com/de/cardmarket-api
- TCGplayer sagt in der aktuellen Entwicklerdokumentation, dass neue API-Zugänge derzeit nicht vergeben werden: https://docs.tcgplayer.com/docs/getting-started
- Collectr bietet API-Zugang auf Anfrage/Genehmigung; die API-Bedingungen beschränken die Nutzung und untersagen u.a. nicht genehmigtes Scraping und konkurrierende Anwendungen: https://getcollectr.com/api-terms-and-conditions.html
- Deshalb enthält diese Version keine Scraper und behauptet keine Live-Preise. Für echte Preisautomatik braucht es zulässigen Datenzugang bzw. einen lizenzierten Datenanbieter. Zugangsschlüssel gehören bei einer späteren Serverlösung ausschließlich auf den Server, nie in den Browser.
- Die Daten bleiben lokal im Browser. Für Nutzung auf mehreren Geräten oder sichere Synchronisierung wäre ein Backend mit Anmeldung und Datenbank nötig.

## Import der vorhandenen Excel-Sammlung
Öffne deine Excel-Datei und speichere das Blatt „Kartensammlung“ als CSV UTF-8 mit Semikolon-Trennung. Die App erkennt sowohl die englischen Feldnamen als auch passende deutsche Spaltenüberschriften (z. B. `Kartenname`, `Set / Edition`, `Kartennummer`, `Anzahl`, `Einkaufspreis`, `Deutschland Preis/Stück`, `Collectr Preis/Stück`, `TCGplayer Preis/Stück`, `Notizen`). Speichere das Tabellenblatt `Kartensammlung` aus Excel als CSV UTF-8 und importiere diese CSV. Bilder werden beim CSV-Import nicht mitübernommen; dafür JSON-Backup verwenden.

### Preise aktualisieren
In der Sammlung gibt es den Button **„Preise aktualisieren“**. Er zeigt alle gespeicherten Karten in einer Sammelbearbeitung, bietet Suchlinks zu Cardmarket, Collectr und TCGplayer und lässt die Preise für alle Karten in einem Durchgang speichern. Ohne API-Zugänge werden Preise nicht automatisch live abgerufen; du recherchierst sie über die Links und trägst die Werte ein. Das Prüfdatum wird beim Speichern aktualisiert.

## Handy-App installieren und Kamera nutzen

Die App ist jetzt als **installierbare Web-App (PWA)** vorbereitet. Auf dem Handy kann sie dann wie eine App zum Startbildschirm hinzugefügt werden. Das Kartenfoto-Feld verwendet `capture="environment"`, damit unterstützte Handys direkt die rückseitige Kamera öffnen.

**Wichtig:** Für die Installation, Kamerafunktion und Offline-App muss die App auf einer HTTPS-Adresse veröffentlicht sein (oder lokal über `localhost` laufen). Eine einzelne HTML-Datei, die direkt aus Downloads geöffnet wird, kann diese Funktionen je nach Handy/Browser einschränken.

### Schnellstart
1. Lade das komplette ZIP herunter und entpacke es.
2. Veröffentliche den Inhalt des Ordners `pokemon_card_webapp` auf einem HTTPS-fähigen statischen Hosting-Anbieter (z. B. GitHub Pages oder Netlify).
3. Öffne die veröffentlichte HTTPS-Adresse auf dem Handy.
4. **Android/Chrome:** Menü `⋮` → „App installieren“ oder „Zum Startbildschirm hinzufügen“.
5. **iPhone/Safari:** Teilen-Symbol → „Zum Home-Bildschirm“.

Die Datenbank bleibt derzeit lokal auf dem jeweiligen Gerät im Browser. Für eine gemeinsame Sammlung zwischen PC und Handy ist zusätzlich eine Synchronisierung oder ein Export/Import-Backup nötig. Ein Browserwechsel oder das Löschen der Browserdaten kann lokale Daten entfernen; exportiere daher regelmäßig ein JSON-Backup.
