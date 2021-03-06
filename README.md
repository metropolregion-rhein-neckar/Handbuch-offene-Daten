# Handbuch-offene-Daten


> **Feedback (Hinweise, Wünsche und Fragen)** bitte per E-Mail senden an: heinrich.lorei@m-r-n.com


# Leitlinien der Metropolregion Rhein-Neckar für einfach nutzbare Behördendaten

Diese Leitlinien basieren auf den Leitlinien des [Kantons Zürich](https://github.com/openZH/mdd-ogd-handbook/blob/main/publikationsleitlinien.md) für einfach nutzbare Behördendaten.

Handlungsleitende Normen, um offene Behördendaten ('Open Government Data', OGD) bereitzustellen, die einfach nutzbar sind:
- [Datei-Formate](#datei-formate)
- [Daten-Strukturen](#daten-strukturen)

## Datei-Formate

### Grundsatz
Offene Daten stehen in einem nicht-proprietären, [offenen Format](http://opendatahandbook.org/glossary/en/terms/open-format/) zur Verfügung.

### Vorgaben
Für tabellarische Daten verwenden wir das Format [CSV](http://opendatahandbook.org/glossary/en/terms/csv/) in Unicode UTF-8 Kodierung (**nicht** XLS). <br>

Variabeln und Werte werden in einer CSV standardgemäß mittels Kommata `,` getrennt. Wir akzeptieren jedoch auch, wie im deutschen Standard üblich, ein Semikolon als Trennzeichen  `;`.
- [So erstelle ich aus einer XLS-Datei ein CSV.](https://github.com/openZH/mdd-ogd-handbook/blob/main/publikationsleitlinien/UTF-8-kodieren.md)
- [So speichere ich ein CSV als Unicode (UTF-8) ab.](https://github.com/openZH/mdd-ogd-handbook/blob/main/publikationsleitlinien/UTF-8-kodieren.md)

### Empfehlungen
Für Daten mit komplexen Strukturen oder um Daten einfach zwischen Programmen und Systemen zu übertragen, eignet sich das Format [JSON](http://opendatahandbook.org/glossary/en/terms/json/) sehr gut.

## Daten-Strukturen

### Grundsatz
Offene Daten stehen als [strukturierte Daten](http://opendatahandbook.org/glossary/en/terms/structured-data/) zur Verfügung (**nicht** als Word, PDF oder Fliesstext).

### Vorgaben
Tabellarische Daten im Format CSV strukturieren wir gemäss dem Prinzip ['Tidy Data'](https://github.com/openZH/mdd-ogd-handbook/blob/main/publikationsleitlinien/warum_tidy_data.md). <br>

Das heisst: [pro Variable eine Spalte](#pro-variable-eine-spalte), [pro Beobachtung eine Zeile](#pro-beobachtung-eine-zeile) und [pro Wert eine Zelle](#pro-wert-eine-zelle). <br>

[Beispiel](https://www.zh.ch/de/politik-staat/opendata.html?keyword=ogd#/details/523@fachstelle-ogd-kanton-zuerich): <br>
![tidy_data_bsp](https://github.com/openZH/mdd-ogd-handbook/blob/main/publikationsleitlinien/tidy_data_bsp.png)

#### Pro Variable eine Spalte
Keine Spalten-Hierarchien, also keine miteinander zusammengeführten Zellen (z.B. um Ober- und Unterkategorien zu repräsentieren), sondern Oberkategorien in einer ersten Spalte, Unterkategorien in einer zweiten Spalte. <br>

Spaltenüberschriften (Variabeln):
- beginnen nicht mit einer Zahl,
- haben keine Leerzeichen, sondern sind entweder zusammengeschrieben (Gross- und Kleinbuchstaben sind möglich) oder besser mittels 'Underline' verbunden (z.B. `gesuche_total`),
- haben keine Umlaute, sondern sind ausgeschrieben als `ae`, `oe`, `ue` und
- haben keine Sonderzeichen, sondern sind ausgeschrieben (z.B. `prozent` statt `%`).
```
jahr,organisationseinheit,gesuche_haengig_jan,gesuche_total,zugang_uneingeschraenkt_gewaehrt
2013,Direktion der Justiz und des Innern,1,52,45
2014,Direktion der Justiz und des Innern,11,31,19
...
```
Die Anzahl Variablen ist nicht beschränkt. Dabei spielt es keine Rolle, wenn man in der Fensteransicht nicht mehr alle Variablen auf einmal sieht. <br>

#### Pro Beobachtung eine Zeile
- Keine Leerzeilen.
- Keine Fussnoten und ähnliche Verweise. Hinweise vermitteln wir:
   - entweder in einer eigenen Spalte oder
   - (wenn kurz) in der Metadaten-Beschreibung der entsprechenden Daten-Ressource oder
   - (wenn ausführlicher) als HTML-Page, TXT- oder PDF-Datei, die wir in den Metadaten unter "Weitere Informationen" referenzieren.

#### Pro Wert eine Zelle
Alle Zellen einer Spalte haben dasselbe Daten-Format. Die häufigsten sind: 
1. `Text`
2. `Zahl`
3. `Datum`
4. `Uhrzeit`
5. `URL`
6. `Geographischer Standort`

Einheitsangaben dürfen nicht zusammen mit Werten in derselben Zelle stehen. <br>

##### 1. Text 
Werte mit Daten-Format `Text`, die Kommas enthalten, klammern wir zwingend mittels Anführungs- und Schlusszeichen ein (z.B. `"Französisch, Deutsch"`). Das ist wichtig, damit diese Text-Inhalte (in der Fachsprache bezeichnet als `String` bzw. Zeichenkette) trotz Leerzeichen oder Kommas als zusammengehörend interpretiert werden. Falls als Trennzeichen ein Semikolon verwendet wurde, kann dieser Punkt vernachlässigt werden. <br>

##### 2. Zahl 
Werte mit Daten-Format `Zahl` formatieren wir einheitlich ohne Hochkommas, Leerzeichen oder andere 1000er-Trennzeichen.
- Als Dezimaltrennzeichen verwenden wir einen Punkt.
- Ob man rundet oder nicht, kommt auf den Datensatz und seine Nutzung an. Falls gerundet wird, muss dies aber in den Metadaten deklariert werden.

##### 3. Datum 
Werte mit Daten-Format `Datum` geben wir nicht als Zeichenketten (z.B. `24. Dez. 2021`) an, sondern verwenden den [internationalen Standard ISO 8601](https://www.w3.org/TR/NOTE-datetime): `YYYY-MM-DD` (z.B. `2021-12-24`). <br>

##### 4. Uhrzeit 
Werte mit Daten-Format `Uhrzeit` geben wir dem [internationalen Standard ISO 8601](https://www.w3.org/TR/NOTE-datetime) gemäss an als `hh:mm:ss`. Wir verwenden die Zeitzone `UTC+1`: `YYYY-MM-DDThh:mm:ssTZD (z.B. 2021-12-24T19:20:30+01:00)`. <br>

##### 5. URL 
Werte mit Daten-Format `URL` schreiben wir standardmässig aufrufbar aus im Format `https://...`. <br>

##### 6. Geographischer Standort
Werte über den geographischen Standort können auf unterschiedliche Weise eingetragen werden:
- Längen/Breitengrad (jeweils eine Spalte)
- Adresse, d.h. Straße, Hausnummer, Postleitzahl und Ort (jeweils eine Spalte)
- Geometrie im [WKT](http://giswiki.org/wiki/Well_Known_Text)-Format

Falls Koordinaten oder eine Geometrie für die Angabe des Geographischen Standorts verwendet wurden, sollte zusätzlich noch das verwendete Koordinatensystem angegeben werden.
Hierfür den EPSG-Code im Dateinamen oder explizit in den Metadaten vermerken (bspw. Beispiel_Tabelle_4326.csv).

### Empfehlungen
Wir wählen möglichst aussagekräftige Spaltenüberschriften (Variabeln). Ihre Bedeutung erklären wir:
- (wenn kurz) in der Metadaten-Beschreibung der entsprechenden Daten-Ressource oder
- (wenn ausführlicher) auf einer HTML-Page, in einer TXT- oder PDF-Datei, die wir in den Metadaten unter "Weitere Informationen" referenzieren.

Werte, die ausdrücklich unbekannt sind, weisen wir als `None` aus.

Zellen ohne Werte lassen wir leer:
```
jahr,organisationseinheit,gesuche_haengig_jan,gesuche_total,zugang_uneingeschraenkt_gewaehrt
2013,Direktion der Justiz und des Innern,1,52,45
2013,Sicherheitsdirektion,,12,4
2013,Finanzdirektion,,14,14
2013,Volkswirtschaftsdirektion,,3,2
2013,Gesundheitsdirektion,1,45,8
2013,Bildungsdirektion,6,25,10
2013,Baudirektion,1,9,7
2013,Staatskanzlei,,,
...
```

## Lizenzen
Lizenzen bestimmen die Regeln, unter denen Nutzer die vorhandenen Daten verwenden können. Grundsätzlich arbeiten wir mit freien Lizenzen und lassen nur in begründeten Fällen weitere Lizenztypen zu. 

Wir unterstützen folgende offenen Lizenztypen und orientieren uns hierbei an den Vorgaben vom nationalen Datenportal: 
[Vorgaben vom nationalen Datenportal](https://www.dcat-ap.de/def/licenses/)
