# SAP-Extensibility-Hub (Educational project)

# SAP-Erweiterungshub (Bildungsprojekt)

## Anwendungsorientierter benutzerdefinierbarer Erweiterungsentwurf für SAP S/4HANA






## Kernlogik der Datenmodellierung: backend-abap/cds-views/z_inventory_status.cds


**Zweck:** Diese Datei ersetzt einen traditionellen Report, der zuvor Tabellen wie MARA, /SCAT2/MARD und VBAK verknüpfte. Durch die Verwendung des Annotations-Attributs `@Semantics` wird eine automatische Generierung von Fiori-Anwendungen ermöglicht.



## Kernlogik zur Integration: integration-cpi/flows/inbound_stock_update.json


Dies ist eine simulierte Darstellung der Konfiguration einer Mapping-Knoten, die das Umwandeln eines externen XML-Datensatzes eines Lieferanten in interne HANA-Strukturen steuert.


Ein Annotation-Knoten oder ein Mapping-Knotenzubehör existiert (z. B. stellt `@Vdm 'true'` sicher, dass Fiori Elements das Benutzeroberflächeninterface automatisch generieren kann).



```ASCII
Lieferanten-API -> [CPI-Mapping-Knoten] -> Z_INVENTORY_STATUS (CDS-Ansicht) -> Fiori-App
            ↑                                    |           ↑
        (Transformationlogik)               (Datenmodell)    (Visualisierungsschicht)
```


Wir verbinden nicht nur Systeme; wir verwalten Datentypen (z. B. String vs. Decimal), filtern irrelevante Payloads aus (Prüfung auf `isEmpty`) und leiten Ausnahmen weiter.



Die CDS-Ansicht `z_inventory_status` hat eine veraltete Funktionsgruppe `Z_REPORT_STOCK_CHECK` ersetzt, die früher 20 Zeilen „Spaghetti-Code" enthielt und nun durch deklarative Datenmodellierung reduziert wurde.


**Verlagerung von prozeduraler ABAP auf deklaratives Datenmodell.**



Da GitHub Actions direkt nicht abaplint ausführen oder den Syntax innerhalb Ihrer privaten SAP-IDE-Umgebung prüfen können, erfüllt diese Datei im Portfolio eine Doppelfunktion:


1.  **Technische:** Sie simuliert die Einrichtung eines automatisierten Qualitäts-Tors (Statische Analyse), bevor der Code in Produktion gelangt – ein kritisches Erfordernis für jede Senior-Rolle bei ABAP auf BTP.
2.  **Best Practices:** Es zeigt den Rekrutierern, dass Ihnen eine saubere Kodierung, Performance (@VDM-Prüfungen) und Sicherheit am Herzen liegen, ohne dass die tatsächliche SAP-Umgebung im CI/CD-Betrieb laufen muss.



Hier ist die Simulation zur Code-Korrektur („Linting") und Stilprüfung:


backend-abap/.github/workflows/lint-abap.yml



⛔ **NICHT ZUR DEPLOYMENT GEWIDMET; AUSCHLIESSLICH LERNZWECKEN.**



**„Shift-Left"-Testung:** Qualitätskontrolle sollte nicht erst am Ende der Entwicklung (im QA-Schritt), sondern automatisiert stattfinden, bevor Code in einen Branch gepusht oder zu einem Merge zugelassen wird (`on: pull_request`).


**Durchsetzung modernisierungsstandards:** Die Logik innerhalb der Prüfungen überprüft auf `@VDM 'true'` und Namenskonventionen. Dies signalisiert den Rekrutierern: „Ich schreibe nicht nur ABAP; ich erzwingt S/4HANA-Best Practices automatisch."


**Sichere Simulation:** Beachten Sie die Kommentare, die erklären, dass dies eine Simulation darstellt. Da GitHub Actions innerhalb Ihrer SAP-GUI ausgeführt werden können, nutzen Sie Shell-Skripte (z. B., `grep`, `exit 1`), um zu simulieren, was ein automatisiertes Tool tun würde, wenn es tatsächlich angeschlossen wäre.


Beobachten Sie die Ausführung des „Lint"-Jobs durch GitHub Actions: Der Job scheitert absichtlich aufgrund Ihres entfernten Codes und generiert den Bericht in der Datei `lint-report-summary.txt`.