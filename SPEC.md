# Wolff’s Naturkosmetik – SPEC.md
Stand: nach Meeting 2

## Entitäten
- Kunde: Kundennummer, Name, Kontakt, Lieferadresse, Kundentyp
- Bestellung: Bestellnummer, Datum, Bestellkanal, Bearbeitungsstatus, Zahlungsstatus, Versanddatum, Sendungsnummer
- Bestellposition: Positionsnummer, Bestellung, Produkt, Stückzahl, Einzelpreis
- Produkt: Produktnummer, Name, Kategorie, Beschreibung, Privatkundenpreis, Händlerpreis, vegan, Herstellungsdauer
- Charge: Chargennummer, Produkt, Produktionsdatum, Mindesthaltbarkeitsdatum, Bestand
- Chargenzuordnung: Zuordnungsnummer, Bestellposition, Charge, entnommene Stückzahl
- Inhaltsstoff: Inhaltsstoffnummer, Name, Kennzeichnung als Allergen
- Händlerkondition: Konditionsnummer, Wiederverkäufer, Zahlungsziel, Freigabe für Zahlung nach Versand

## Beziehungen
- Kunde 1:n Bestellung: Ein Kunde kann mehrere Bestellungen aufgeben.
- Bestellung 1:n Bestellposition: Eine Bestellung enthält eine oder mehrere Positionen.
- Produkt 1:n Bestellposition: Ein Produkt kann in mehreren Bestellpositionen vorkommen.
- Produkt 1:n Charge: Ein Produkt kann mehrere Chargen haben.
- Bestellposition 1:n Chargenzuordnung: Eine Position kann mehrere Chargenzuordnungen haben.
- Charge 1:n Chargenzuordnung: Eine Charge kann für mehrere Positionen verwendet werden.
- Produkt n:m Inhaltsstoff: Ein Produkt enthält mehrere Inhaltsstoffe. Derselbe Inhaltsstoff kann in mehreren Produkten vorkommen.
- Wiederverkäufer 1:0..1 Händlerkondition: Vorerst wird höchstens ein aktueller Konditionsdatensatz je Händler angenommen.

Die Beziehung zwischen Bestellung und Produkt wird über
die Bestellposition erfasst. Die Beziehung zwischen
Bestellposition und Charge wird über die Chargenzuordnung
mit der jeweiligen Stückzahl erfasst.

## Business Rules
1. Wiederverkäufer bekommen ab 50 Stück pro Bestellung den Händlerpreis. Bei kleineren Bestellungen gilt der Privatkundenpreis. (Meeting 1, Nachricht 3)
2. Wiederverkäufer zahlen ab 50 Stück keinen Versand. Darunter gelten die gleichen Versandregeln wie für Privatkunden. Für Privatkunden ist der Versand ab 39 Euro nach Abzug des Rabatts kostenlos. (Meeting 2, Nachricht 4)
3. Produkte, die am frühesten ablaufen, werden zuerst verschickt. Sind sie weniger als einen Monat haltbar, verkauft Nina sie günstiger. (Meeting 1, Nachricht 2)
4. Bei Produkten mit gekennzeichneten Allergenen müssen Kunden bestätigen, dass sie den Hinweis gelesen haben. Ohne Bestätigung können sie nicht bestellen. Bei Produkten ohne relevante Allergene ist keine Bestätigung nötig. (Meeting 1, Nachricht 6)
5. Stammkunden haben innerhalb von zwölf Monaten mindestens sechs Bestellungen bezahlt und erhalten. Sie bekommen zehn Prozent Rabatt und können neue Chargen 24 Stunden früher bestellen. Auf Händlerpreise und reduzierte Restposten gibt es keinen zusätzlichen Treuerabatt. Messekäufe zählen mit, wenn bekannt ist, welcher Kunde gekauft hat. (Meeting 2, Nachrichten 2 und 3)
   
Weitere Bedingungen aus dem Gespräch: Privatkunden und
neue Wiederverkäufer zahlen im Voraus. Bewährte Händler
können ein Zahlungsziel ab Versanddatum erhalten.
Nina darf alle Daten verwalten; ihre Mutter darf
nur die Packliste ansehen. (Nachrichten 4 und 9)

## Widersprüche
1. Nina nennt zunächst Versand nach Zahlungseingang, später Zahlungsziele für Händler. Geklärt: Privatkunden und neue Händler zahlen im Voraus, bewährte Händler können nach Versand zahlen. (Nachrichten 1, 3 und 4)
2. Nina sagt zuerst, dass Wiederverkäufer nie Versandkosten zahlen. In Meeting 2 schränkt sie das ein.
Geklärt: Kostenloser Versand gilt für Händlerbestellungen ab 50 Stück. Darunter gelten die Versandregeln für Privatkunden. (Meeting 1, Nachricht 3; Meeting 2, Nachricht 4)

## Prioritäten
- Erste Version: Bestellübersicht, offene Aufgaben, Lagerbestand, Chargen, Mindesthaltbarkeitsdaten, Bestandsprüfung und Allergen-Bestätigung
- Danach: Stammkunden, Händlerverträge und die monatliche Abo-Box mit vier Produkten für 39 Euro
- Später: Marketing-Auswertung, Offline-Modus und weitere Mitarbeiterrollen

Quellen: Nachrichten 10 bis 12.

## Offene Fragen
- Wie wird die Allergen-Bestätigung gespeichert?
- Wie hoch sind die Versandkosten bei Bestellungen unter 39 Euro?
- Wie lange bleibt Ware bei unbezahlten Bestellungen reserviert?
- Welche Bestellstatus soll es genau geben?
- Wie werden Kündigungen und Erstattungen bei der Abo-Box endgültig geregelt?

## Bestandsführung
Ware wird bei der Bestellung reserviert und beim Verpacken vom Bestand abgezogen.
Reservierte Ware ist für andere Kunden nicht verfügbar.
Bei Stornierung vor dem Verpacken wird sie wieder frei. Die Bestellung bleibt gespeichert.
Marktverkäufe werden sofort vom Bestand abgezogen.
Quelle: Meeting 2, Nachrichten 7 und 8.

## Neue Anforderung – Abo-Box
„Self-Care-Monthly“ enthält vier Produkte für 39 Euro monatlich.
Abbuchung am 1., Versand zwischen dem 3. und 5.
Pausen sind höchstens zwei Monate am Stück möglich.
Danach läuft das Abo weiter oder endet, je nach vorheriger Wahl des Kunden.
Bei Ausfall einer bezahlten Box gibt es einen Gutschein über 39 Euro.
Die App verwaltet Abos, Boxinhalte und Liefertermine
und warnt bei fehlenden Produkten.
Kündigung und Erstattung sind noch nicht endgültig geklärt.
Quelle: Meeting 2, Nachrichten 1, 5 und 6.
