# Wolff’s Naturkosmetik – SPEC.md
Stand nach Meeting 1

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
1. Händlerpreise gelten ab 50 Einheiten pro Bestellung. Darunter gelten Privatkundenpreise. (Nachricht 3)
2. Wiederverkäufer zahlen keinen Versand. Für Privatkunden ist der Versand bei einem Bestellwert über 39 Euro kostenlos. (Nachricht 3)
3. Ware mit dem nächsten Mindesthaltbarkeitsdatum soll zuerst verschickt werden. Bei weniger als einem Monat Resthaltbarkeit verkauft Nina sie günstiger als Restposten. (Nachricht 2)
4. Bei Produkten mit relevanten Allergenen müssen Kunden den Hinweis vor Bestellabschluss ausdrücklich bestätigen. (Nachricht 6)
5. Die Voraussetzungen und Vorteile für Stammkunden sind noch zu klären. (Nachricht 12)

Die Auswahl der fünf Regeln ist vorläufig.
Weitere Bedingungen aus dem Gespräch: Privatkunden und
neue Wiederverkäufer zahlen im Voraus. Bewährte Händler
können ein Zahlungsziel ab Versanddatum erhalten.
Nina darf alle Daten verwalten; ihre Mutter darf
nur die Packliste ansehen. (Nachrichten 4 und 9)

## Widersprüche
1. Nina nennt zunächst Versand nach Zahlungseingang, später Zahlungsziele für Händler. Geklärt: Privatkunden und neue Händler zahlen im Voraus, bewährte Händler können nach Versand zahlen. (Nachrichten 1, 3 und 4)
2. Ein zweiter eindeutiger Widerspruch ist noch offen und muss in Meeting 2 geklärt werden.

## Prioritäten
- Erste Version: Bestellübersicht, offene Aufgaben, Lagerbestand, Chargen, Mindesthaltbarkeitsdaten, Bestandsprüfung und Allergen-Bestätigung
- Danach: Stammkunden, Händlerverträge und die monatliche Abo-Box mit vier Produkten für 39 Euro
- Später: Marketing-Auswertung, Offline-Modus und weitere Mitarbeiterrollen

Quellen: Nachrichten 10 bis 12.

## Offene Fragen
- Wann gilt jemand als Stammkunde und welche Vorteile gibt es?
- Wie funktionieren Zahlung, Lieferung, Pause und Kündigung der Abo-Box?
- Welche Versandregel gilt bei genau 39 Euro?
- Wann wird Bestand reserviert?
- wie werden Marktverkäufe erfasst?
- Wie wird die Allergen-Bestätigung gespeichert?
- Welche Bestellstatus und Vertragsdaten werden benötigt?
- Welcher zweite Widerspruch muss geklärt werden?
