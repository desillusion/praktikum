Um die Unterschiede im Datenmodell zwischen einer NoSQL-Datenbank wie Apache Cassandra und einer relationalen Datenbank wie MySQL anhand einer Bäckerei zu veranschaulichen, stellen wir uns vor, wie eine Bäckerei ihre Daten in beiden Datenbanksystemen speichern könnte.

### Relationale Datenbank (z.B. MySQL)

**1. Tabellenstruktur:**
In einer relationalen Datenbank werden Daten in Tabellen organisiert, die durch Zeilen und Spalten definiert sind. Jede Tabelle repräsentiert eine spezifische Entität, und die Beziehungen zwischen den Tabellen werden durch Fremdschlüssel hergestellt.

**Beispiel:**
- **Tabelle `Kunden`**
  - KundeID (Primärschlüssel)
  - Name
  - Adresse
  - Telefonnummer

- **Tabelle `Bestellungen`**
  - BestellungID (Primärschlüssel)
  - KundeID (Fremdschlüssel)
  - Datum
  - Gesamtbetrag

- **Tabelle `Produkte`**
  - ProduktID (Primärschlüssel)
  - Name
  - Preis

- **Tabelle `Bestellungspositionen`**
  - BestellungspositionID (Primärschlüssel)
  - BestellungID (Fremdschlüssel)
  - ProduktID (Fremdschlüssel)
  - Menge

**Beziehungen:**
- Ein Kunde kann mehrere Bestellungen haben (1:n Beziehung zwischen `Kunden` und `Bestellungen`).
- Eine Bestellung kann mehrere Produkte enthalten (n:m Beziehung zwischen `Bestellungen` und `Produkten`, realisiert durch `Bestellungspositionen`).

### NoSQL-Datenbank (z.B. Cassandra)

**1. Schemafrei:**
NoSQL-Datenbanken sind oft schemafrei, was bedeutet, dass die Struktur der Daten flexibel ist und sich leicht ändern lässt. Daten werden in Dokumenten, Schlüssel-Wert-Paaren oder Spaltenfamilien gespeichert.

**Beispiel:**
- **Kundendokument:**
  ```json
  {
    "KundeID": "123",
    "Name": "John Doe",
    "Adresse": "123 Bäckerstraße",
    "Telefonnummer": "0123456789",
    "Bestellungen": [
      {
        "BestellungID": "456",
        "Datum": "2024-07-08",
        "Gesamtbetrag": 50.00,
        "Produkte": [
          {
            "ProduktID": "789",
            "Name": "Brot",
            "Preis": 2.00,
            "Menge": 5
          },
          {
            "ProduktID": "101",
            "Name": "Kuchen",
            "Preis": 10.00,
            "Menge": 3
          }
        ]
      }
    ]
  }
  ```

**Unterschiede:**

1. **Datenmodellierung:**
   - **Relationale Datenbank:** Daten sind stark normalisiert und in verschiedenen Tabellen verteilt. Beziehungen zwischen den Tabellen werden durch Fremdschlüssel hergestellt.
   - **NoSQL-Datenbank:** Daten sind oft denormalisiert und in einem einzigen Dokument oder einer Sammlung gespeichert, was das Abrufen der Daten effizienter macht, aber zu Datenredundanz führen kann.

2. **Flexibilität:**
   - **Relationale Datenbank:** Ein festes Schema, das definiert, wie Daten gespeichert werden. Änderungen am Schema sind oft komplex und können Ausfallzeiten erfordern.
   - **NoSQL-Datenbank:** Schemafrei oder schemalos, was bedeutet, dass Datenstrukturen flexibel sind und sich leicht ändern lassen, ohne die gesamte Datenbank zu beeinflussen.

3. **Skalierbarkeit:**
   - **Relationale Datenbank:** Horizontale Skalierung (Sharding) ist schwieriger und erfordert oft komplexe Architekturen. Besser geeignet für vertikale Skalierung.
   - **NoSQL-Datenbank:** Entwickelt für horizontale Skalierung, wobei Daten über mehrere Knoten hinweg verteilt werden können, um Last und Speicherbedarf zu bewältigen.

4. **Abfragekomplexität:**
   - **Relationale Datenbank:** Unterstützt komplexe Abfragen und Transaktionen mittels SQL. Ideal für Anwendungen, die ACID-Eigenschaften benötigen.
   - **NoSQL-Datenbank:** Einfachere Abfragesprachen und weniger komplexe Transaktionen. Besser geeignet für Anwendungen, die hohe Verfügbarkeit und Skalierbarkeit über strikte Konsistenz benötigen.

Durch diese Analogie lässt sich gut nachvollziehen, wie sich die beiden Datenbanktypen in ihrer Struktur, Flexibilität und Skalierbarkeit unterscheiden und welche Anwendungsfälle für welche Datenbanktypen besser geeignet sind.