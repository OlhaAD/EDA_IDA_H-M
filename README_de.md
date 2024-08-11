# Marktdynamik der Mode bei H&M: Analyse von Trends, Preisen und Kundenverhalten

## Einführung

Im Rahmen dieses Projekts liegt der Schwerpunkt auf der primären Datenanalyse der Marke H&M. Die Analyse wird mit der Programmiersprache Python durchgeführt und umfasst eine umfangreiche explorative Datenanalyse (Exploratory Data Analysis, EDA) sowie eine anfängliche Datenanalyse (Initial Data Analysis, IDA). Diese Analysemethoden helfen, die Haupttrends, Anomalien, Muster und mögliche Richtungen für weitere tiefergehende Untersuchungen der Daten zu identifizieren.

Das Ziel des Projekts ist es, einen umfassenden Überblick über den aktuellen Stand der Verkäufe und das Kundenverhalten bei H&M zu bieten sowie den Einfluss verschiedener Faktoren auf die Verbraucheraktivität und die Wirksamkeit der Geschäftsstrategien zu bewerten. Die Ergebnisse dieser Analyse werden die Grundlage für die Entwicklung von Empfehlungen zur Optimierung der Marketing- und Verkaufsstrategien des Unternehmens bilden.

## Wie man das Projekt startet
- Klone das Repository auf deinen lokalen Computer:
```sh
git clone https://github.com/your-username/your-repository.git
```
- Daten für die Analyse:
Die Daten sind zu groß, um sie auf GitHub zu speichern. Im Projekt werden direkte Links zu 3 Dateien auf meinem Google Drive verwendet: articles, customers und transactions.

- Öffne die Notebooks:
Öffne die Notebooks im Ordner /notebooks über Google Colab oder Jupyter Notebook, um den Code anzusehen und auszuführen.

- Installiere die erforderlichen Abhängigkeiten:
Installiere die erforderlichen Abhängigkeiten mit dem folgenden Befehl:
```sh
pip install -r requirements.txt
```
(Es wird angenommen, dass du eine Datei requirements.txt erstellt hast, die alle notwendigen Bibliotheken auflistet).

**Beispielcode für den Zugriff auf Daten auf Google Drive in Google Colab**
```python
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials
import pandas as pd

# Authentifizierung und Autorisierung
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

# Herunterladen von Dateien von Google Drive
file_ids = {
    'articles': '1H-g4oAbw1ZjYDOncx3xU3oro3tH3UIg6',
    'customers': '1KLM7Vum2O35MR17ULRLneM0uGVX61-VR',
    'transactions': '18ESMoz4VDe_ZCZzRPKKZS-UargXvrRdi'
}

for name, file_id in file_ids.items():
    downloaded = drive.CreateFile({'id': file_id})
    downloaded.GetContentFile(f'{name}.csv')
    print(f'{name}.csv downloaded')

# Lesen der Daten in DataFrames
df_articles = pd.read_csv('articles.csv')
df_customers = pd.read_csv('customers.csv')
df_transactions = pd.read_csv('transactions.csv')

# Anzeige der ersten Zeilen jedes DataFrames
print(df_articles.head())
print(df_customers.head())
print(df_transactions.head())
```
## Ziele und Aufgaben
### Ziele
Einen umfassenden Überblick über den aktuellen Stand der Verkäufe und des Kundenverhaltens bei H&M zu bieten, sowie den Einfluss verschiedener Faktoren auf die Kundenaktivität und die Wirksamkeit der Geschäftsstrategien zu bewerten. Die Ergebnisse dieser Analyse werden die Grundlage für die Entwicklung von Empfehlungen zur Optimierung der Marketing- und Verkaufsstrategien des Unternehmens bilden.
### Aufgaben
1. **Daten sammeln und vorverarbeiten:** Suchen, Herunterladen und Bereinigen der Daten von Fehlern und fehlenden Werten, Vorbereitung der Daten für die Analyse.
2. **Datenanalyse:** Untersuchung von Mustern, Trends und Zusammenhängen in den vorbereiteten Daten.
3. **Datenvisualisierung:** Erstellung von Grafiken und Diagrammen zur anschaulichen Darstellung der Analyseergebnisse.
4. **Schlussfolgerungen:** Interpretation der Analyse- und Visualisierungsergebnisse zur Formulierung der abschließenden Schlussfolgerungen und Empfehlungen
## Detaillierte Methodik
### Werkzeuge und Bibliotheken
In diesem Projekt wurden die folgenden Werkzeuge und Bibliotheken verwendet:

- **Python:** Die Hauptprogrammiersprache für Datenanalyse und Modellierung.

- **Pandas:** Bibliothek zur Datenverarbeitung und -analyse. Verwendet für die Arbeit mit DataFrames.

- **NumPy:** Bibliothek zur Arbeit mit Arrays und zur Durchführung numerischer Berechnungen.

- **Seaborn:** Auf matplotlib basierende Bibliothek zur Datenvisualisierung. Verwendet zur Erstellung statistischer Diagramme.

- **Matplotlib:** Die Hauptbibliothek zur Erstellung von Diagrammen und zur Datenvisualisierung.

- **Squarify:** Eine Bibliothek zur Erstellung von Treemap-Diagrammen.

- **textwrap:** Eine Bibliothek zum Umbruch von Textzeilen, damit der Text in die angegebenen Grenzen passt.

- **Plotly:** Eine Bibliothek für interaktive Datenvisualisierung.

### Datensammlung und Vorverarbeitung
**Datenquelle:**
Die Daten für dieses Projekt stammen von https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations/data

**Datenbankstruktur:**
Die Datenbank ist in drei Dateien unterteilt: ArticlesHM, CustomersHM und TransactionsHM.

**ArticlesHM** ist eine Tabelle, die alle Artikel von H&M enthält, mit insgesamt **105 542 Zeilen** und den folgenden Spalten:
- **article_id:** Artikel-ID, Datentyp - int64
- **prod_name:** Artikelname, Datentyp - object
- **product_type_name:** Produkttypname, Datentyp - object
- **product_group_name:** Produktgruppenname, Datentyp - object
- **graphical_appearance_name:** Name des grafischen Erscheinungsbildes, Datentyp - object
- **colour_group_name:** Farbgruppenname, Datentyp - object
- **index_name:** Name des Unterabschnitts, Datentyp - object
- **index_group_name:** Name des Abschnitts, Datentyp - object
- **section_name:** Sektionsname, Datentyp - object
- **garment_group_name:** Kategorie, Datentyp - object
- **detail_desc:** Details, Datentyp - object

**CustomersHM** ist eine Tabelle, die Informationen über H&M-Kunden enthält, mit insgesamt **1 371 979 Zeilen** und den folgenden Spalten:
- **customer_id:** Kunden-ID, Datentyp - object
- **Active:** Aktivitätsstatus, Datentyp - float64
- **club_member_status:** Clubmitgliedsstatus, Datentyp - object
- **fashion_news_frequency:** Häufigkeit der Modenachrichten, Datentyp - object
- **age:** Alter des Kunden, Datentyp - float64
- **postal_code:** Postleitzahl, Datentyp - object

**TransactionsHM** ist eine Tabelle, die Informationen über H&M-Verkäufe enthält, mit insgesamt **31 788 323 Zeilen** und den folgenden Spalten:
- **t_dat:** Verkaufsdatum, Datentyp - object
- **customer_id:** Kunden-ID, Datentyp - object
- **article_id:** Artikel-ID, Datentyp - int64
- **price:** Preis, Datentyp - float64
- **sales_channel_id:** Vertriebskanal, Datentyp - int64

#### Datenoptimierung

Der DataFrame **df_articles** erfordert die folgende Optimierung:

1. **Umwandlung der Spalte `article_id` in `int32`:**
    - Reduzierung des Speicherplatzbedarfs durch Verwendung eines 32-Bit-Ganzzahltyps anstelle eines 64-Bit-Typs. Dies spart Speicherplatz bei der Speicherung von Ganzzahldaten. Der minimale Wert von article_id beträgt 108 775 015 und der maximale Wert 959 461 001, was innerhalb des Bereichs von int32 (-2 147 483 648 bis 2 147 483 647) liegt.
   
Diese Umwandlungen haben den Speicherplatzbedarf des DataFrames `df_article` von **8,9 MB** vor der Optimierung auf **8,5 MB** nach der Optimierung reduziert.

Der DataFrame **df_customers** erfordert die folgende Optimierung:

1. **Umwandlung der Spalte `Active` von `float64` in `bool`:**
    - Wir haben festgestellt, dass `Active` nur einen Wert von 1 annimmt, während die meisten anderen Werte NaN sind. Daher ist die Umwandlung dieser Spalte von float64 in bool gerechtfertigt und ermöglicht eine erhebliche Optimierung unserer Daten.

2. **Umwandlung der Spalten `club_member_status` und `fashion_news_frequency` von `object` in den kategorialen Datentyp (`category`):**
    - Beide Spalten nehmen eine begrenzte Anzahl von Werten an, nämlich jeweils 3. `fashion_news_frequency` kann die Werte 'NONE', 'Regularly', 'Monthly' und `club_member_status` die Werte 'ACTIVE', 'PRE-CREATE', 'LEFT CLUB' haben. Daher ist die Umwandlung von object in diesem Fall notwendig.

3. **Umwandlung der Spalte `age` von `float64` in `uint8`:**
    - Die Spalte `age` nimmt Werte von 0 bis 99 an, daher ist die Umwandlung in den Datentyp uint8, der Werte im Bereich von 0 bis 255 verwendet, sinnvoll.

Durch diese Transformationen konnten wir die von DataFrame „df_customers“ verwendete Speichermenge erheblich reduzieren, von **62,8 MB** vor der Optimierung auf **26,2 MB** nach der Optimierung.

Der DataFrame **df_transactions** stellt ein sehr großes Informationsvolumen dar und erfordert daher die folgende zusätzliche Optimierung:

1. **Umwandlung der Spalte `t_dat` in `datetime64[ns]`:**
    - Speicherersparnis durch die Verwendung eines effizienteren Formats für Datumsangaben, das das Speichervolumen im Vergleich zum Typ object reduziert.

2. **Umwandlung der Spalte `article_id` in `int32`:**
    - Speicherreduktion durch die Verwendung von 32-Bit-Ganzzahlen anstelle von 64-Bit-Ganzzahlen. Dies spart Speicherplatz bei der Speicherung von ganzzahligen Daten. Der minimale Wert von article_id beträgt 108 775 015 und der maximale Wert 956 217 002, was innerhalb des Bereichs von int32 (-2 147 483 648 bis 2 147 483 647) liegt.

3. **Umwandlung der Spalte `price` in `float32`:**
    - Speicherreduktion durch die Verwendung von 32-Bit-Gleitkommazahlen anstelle von 64-Bit-Gleitkommazahlen. Dies ist besonders nützlich für numerische Daten, bei denen keine hohe Genauigkeit erforderlich ist.

4. **Umwandlung der Spalte `sales_channel_id` in `int8`:**
    - Minimierung des Speicherbedarfs für diese Spalte durch die Verwendung von 8-Bit-Ganzzahlen. Da es in der Spalte sales_channel_id nur zwei eindeutige Werte (1 und 2) gibt, ist diese Umwandlung effektiv.

Diese Umwandlungen haben den Speicherbedarf des DataFrame df_transactions erheblich reduziert, von **1,2 GB** vor der Optimierung auf **757.9 MB** nach der Optimierung, was die Gesamtleistung des Systems bei der Arbeit mit großen Datenmengen verbessert.

**Datenbeispiele**
Produktgruppen:
```python
product_group_name
Garment Upper body       42741
Garment Lower body       19812
Garment Full body        13292
Accessories              11158
Underwear                 5490
Shoes                     5283
Swimwear                  3127
Socks & Tights            2442
Nightwear                 1899
Unknown                    121
Underwear/nightwear         54
Cosmetic                    49
Bags                        25
Items                       17
Furniture                   13
Garment and Shoe care        9
Stationery                   5
Interior textile             3
Fun                          2
```
Beispiele für Produkttypen in der Gruppe "Accessories":
```python
product_group_name     product_type_name       
Accessories            Accessories set                 7
                       Alice band                      6
                       Baby Bib                        3
                       Bag                          1280
                       Beanie                         56
                       Belt                          458
                       Bracelet                      180
                       Braces                          3
                       Bucket hat                      7
                       Cap                            13
                       Cap/peaked                    573
                       Dog Wear                       20
                       Earring                      1159
                       Earrings                       11
                       Eyeglasses                      2
                       Felt hat                       10
                       Giftbox                        15
                       Gloves                        367
                       Hair clip                     244
                       Hair string                   238
                       Hair ties                      24
                       Hair/alice band               854
                       Hairband                        2
                       Hat/beanie                   1349
                       Hat/brim                      396
                       Headband                        1
                       Necklace                      581
                       Other accessories            1034
                       Ring                          240
                       Scarf                        1013
                       Soft Toys                      46
                       Straw hat                       6
                       Sunglasses                    621
                       Tie                           141
                       Umbrella                       26
                       Wallet                         77
                       Watch                          73
                       Waterbottle                    22
```
Produktbereiche und ihre Kategorien
```python
index_group_name  index_name                      section_name                  
Baby/Children     Baby Sizes 50-98                Baby Boy                          1717
                                                  Baby Essentials & Complements     4932
                                                  Baby Girl                         1760
                                                  Kids & Baby Shoes                  457
                                                  Kids Local Relevance                 9
                  Children Accessories, Swimwear  Kids & Baby Shoes                 1685
                                                  Kids Accessories, Swimwear & D    1731
                                                  Kids Outerwear                    1199
                  Children Sizes 134-170          Boys Underwear & Basics            842
                                                  Girls Underwear & Basics          1485
                                                  Kids Outerwear                     636
                                                  Young Boy                         2352
                                                  Young Girl                        3899
                  Children Sizes 92-140           Boys Underwear & Basics           1192
                                                  Girls Underwear & Basics          2005
                                                  Kids Boy                          3328
                                                  Kids Girl                         4469
                                                  Kids Local Relevance               183
                                                  Kids Outerwear                     830
Divided           Divided                         Divided Accessories               1732
                                                  Divided Asia keys                  280
                                                  Divided Basics                    1723
                                                  Divided Collection                7124
                                                  Divided Complements Other           35
                                                  Divided Projects                  2364
                                                  Divided Selected                   991
                                                  EQ Divided                          26
                                                  Ladies Denim                       874
Ladieswear        Ladies Accessories              Womens Big accessories            1665
                                                  Womens Shoes                      2026
                                                  Womens Small accessories          3270
                  Ladieswear                      Collaborations                     559
                                                  H&M+                              2337
                                                  Ladies Denim                       227
                                                  Ladies Other                         4
                                                  Mama                              2266
                                                  Special Collections                682
                                                  Womens Casual                     2725
                                                  Womens Everyday Basics            1581
                                                  Womens Everyday Collection        7295
                                                  Womens Jackets                     829
                                                  Womens Nightwear, Socks & Tigh     228
                                                  Womens Premium                    1270
                                                  Womens Tailoring                  3376
                                                  Womens Trend                      2622
                  Lingeries/Tights                Womens Lingerie                   3598
                                                  Womens Nightwear, Socks & Tigh    1338
                                                  Womens Swimwear, beachwear        1839
Menswear          Menswear                        Contemporary Casual               1560
                                                  Contemporary Smart                1778
                                                  Contemporary Street               1490
                                                  Denim Men                          521
                                                  Men Accessories                   1337
                                                  Men Edition                        330
                                                  Men Other                           25
                                                  Men Other 2                        190
                                                  Men Project                        298
                                                  Men Shoes                          645
                                                  Men Suits & Tailoring             1428
                                                  Men Underwear                     2322
                                                  Mens Outerwear                     629
Sport             Sport                           Kids Sports                        626
                                                  Ladies H&M Sport                  1894
                                                  Men H&M Sport                      872
```
**CustomersHM** ist eine Tabelle, die Informationen über H&M-Kunden enthält, mit insgesamt **1 371 979 Zeilen** und den folgenden Spalten:
- **customer_id:** Kunden-ID, Datentyp - object
- **Active:** Aktivitätsstatus, Datentyp - float64
- **club_member_status:** Clubmitgliedsstatus, Datentyp - object
- **fashion_news_frequency:** Häufigkeit der Modenachrichten, Datentyp - object
- **age:** Alter des Kunden, Datentyp - float64
- **postal_code:** Postleitzahl, Datentyp - object

**TransactionsHM** ist eine Tabelle, die Informationen über H&M-Verkäufe enthält, mit insgesamt **31 788 323 Zeilen** und den folgenden Spalten:
- **t_dat:** Verkaufsdatum, Datentyp - object
- **customer_id:** Kunden-ID, Datentyp - object
- **article_id:** Artikel-ID, Datentyp - int64
- **price:** Preis, Datentyp - float64
- **sales_channel_id:** Vertriebskanal, Datentyp - int64

### Analyse und Visualisierung der Daten

**Verteilung der Produkte nach Produktgruppen**

Die Datenbank enthält insgesamt 19 Produktgruppen. Die größte Anzahl an Produkten gehört zur Gruppe "Garment Upper body", die 40,5% aller Produkte ausmacht. Die am wenigsten vertretenen Gruppen sind: 'Nightwear', 'Unknown', 'Underwear/nightwear', 'Cosmetic', 'Bags', 'Items', 'Furniture', 'Garment and Shoe care', 'Stationery', 'Interior textile', 'Fun'. Alle kleineren Gruppen sind in der Visualisierung unter "Other" zusammengefasst.

![VerteilungProdukteNachProduktgruppen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductGroupPie.png)

**Verteilung der Produkte nach Produkttypen innerhalb jeder Gruppe**

Jede der 19 Gruppen hat zusätzlich eine Unterteilung nach Produkttypen. Die Gruppe "Accessories" hat die meisten verschiedenen Produkttypen. Beispiele für Produkttypen in der Gruppe "Accessories" sind im oberen Abschnitt dargestellt. Die Verteilung der drei größten Gruppen "Garment Full body", "Garment Lower body" und "Garment Upper body" nach Produkttypen ist im untenstehenden Balkendiagramm dargestellt.

![VerteilungProdukteNachProdukttypenInnerhalbJederGruppe](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductTypesIn3Groups.png)

**Verteilung der Produkte nach Drucktypen**

Die Analyse der Drucktypen zeigt, welche Drucke unter den Produkten am häufigsten vorkommen. Die Datenbank enthält insgesamt 30 verschiedene Drucktypen. Aus dem Diagramm geht hervor, dass der beliebteste Druck "Solid" ist, der 47,1% aller Produkte ausmacht. Die seltensten Drucktypen sind in der Gruppe "Other" zusammengefasst.

![VerteilungProdukteNachDrucktypen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductDruckePie.png)


**Verteilung der Produkte nach Farben**

Von den 50 verschiedenen Farben ist Schwarz die am häufigsten vorkommende Farbe. Für eine bessere Übersichtlichkeit der folgenden Visualisierung wurde ein Farblexikon erstellt und die Bibliothek Squarify verwendet.

![VerteilungProdukteNachFarben](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductColorsTreemap.png)

**Verteilung der Produkte nach Abteilungen**

Eine weitere wichtige Visualisierung zeigt, wie die Produkte auf die verschiedenen Abteilungen verteilt sind. Dies hilft zu verstehen, welche Produkte beliebter sind. Aus dem Diagramm geht hervor, dass die Abteilung "Ladieswear" mit einem Anteil von 24,6% den größten Teil ausmacht. Die zweitgrößte Abteilung "Divided" umfasst jugendliche und preisgünstigere Kleidung.

![VerteilungProdukteNachAbteilungen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductIndexPie.png)

**Verteilung der Produkte nach Sektionen und Abteilungen innerhalb der Abteilungsgruppen**

Zusätzlich sind einige Abteilungen in Gruppen zusammengefasst, und jede Abteilung enthält Produktsektionen. Im Abschnitt "Datenbankstruktur" ist ein Beispiel für die Daten in Form einer Liste aller Sektionen mit ihrer Unterteilung nach Abteilungen und Abteilungsgruppen dargestellt. Unten ist ein Sunburst-Diagramm dargestellt, das diese Aufteilung visualisiert.

![VerteilungProdukteNachSektionenUndAbteilungenInnerhalbAbteilungsgruppen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductSectionsInCategories.png)

**Verteilung der Produkte nach Sektionen und Kategorien innerhalb der Abteilungsgruppe "Ladieswear"**

Aus dem obigen Diagramm sehen wir, dass nur zwei Abteilungsgruppen eine weitere Unterteilung in mehrere Kategorien haben, von denen jede ihre eigenen Sektionen hat. Diese Abteilungsgruppen sind "Ladieswear" und "Baby/Children". Diese beiden Abteilungsgruppen sind jeweils separat visualisiert.

![VerteilungProdukteNachSektionenUndKategorienInnerhalbAbteilungsgruppeLadieswear](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductSectionsInLadieswear.png)

**Verteilung der Produkte nach Sektionen und Kategorien innerhalb der Abteilungsgruppe "Baby/Children"**

![VerteilungProdukteNachSektionenUndKategorienInnerhalbAbteilungsgruppeBabyChildren](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductSectionsInBaby_Children.png)

**Verteilung der Produkte nach Kategorien**

Wir sehen, dass die größte Kategorie "Jersey Fancy" ist, gefolgt von der Kategorie "Accessories".

![VerteilungProdukteNachKategorien](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ProductGarmentPie.png)

**Verteilung der Kunden nach ihrem Clubstatus**

Die Mehrheit der Kunden sind Clubmitglieder (92.7%), etwa 6.8% befinden sich im Prozess der Clubmitgliedschaft, und ein sehr kleiner Teil — 0.0003% (467 Kunden) hat den Club verlassen. Diese Gruppe wurde zusammen mit den unbestimmten Werten in die Kategorie "Other" aufgenommen.

![VerteilungKundenNachIhremClubstatus](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ClubStatusClientPie.png)

**Analyse der Häufigkeit des Versands von Nachrichten an Kunden**

Etwas mehr als ein Drittel der Kunden (34.8%) sind für regelmäßige Nachrichten angemeldet, 0.1% erhalten Nachrichten monatlich. Der Großteil der Kunden (65.1%) hat überhaupt kein Abonnement. Dies ist ein bedeutender Anteil, und es sollten Schritte unternommen werden, um diesen Anteil zu verringern. Wichtig ist, dass die Nachrichten nicht zu Spam werden, sondern moderelevante Inhalte enthalten, die Interesse wecken, die Website des Unternehmens besuchen und idealerweise Käufe tätigen.

![AnalyseDerHäufigkeitDesVersandsVonNachrichtenAnKunden](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/FashionNewsFrequencytPie.png)

**Visualisierung der Altersverteilung der Kunden**

Das Histogramm zeigt zwei Haupt-Altersspitzen unter den Käufern:

- Der erste Gipfel liegt bei etwa 21 Jahren.
- Der zweite Gipfel liegt bei etwa 50 Jahren.

Es ist auch ein Rückgang der Aktivität im Bereich um die 40 Jahre zu erkennen. Dies könnte ein interessanter Bereich für eine detaillierte Analyse sein. Zum Beispiel sollte untersucht werden, welche Produktgruppen diese Altersgruppe kauft, zu welcher Zeit sie einkaufen und wie oft sie Newsletter erhalten. Das Verständnis dieser Faktoren kann helfen, die Gründe für den Rückgang der Aktivität in dieser Altersgruppe zu erkennen.

Darüber hinaus zeigt das Histogramm einen recht langen Schwanz in Richtung der älteren Kunden, was auf eine beträchtliche Anzahl älterer Käufer hinweist. Dies ist bei der Entwicklung von Marketingstrategien wichtig zu berücksichtigen, da sie eine bedeutende Kundengruppe darstellen.

![AltersverteilungDerKundenMithilfeHistogramm](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ClientsAgeHistogramm.png)

Das Boxplot zeigt:

- Der Median des Altersverteilung liegt bei 31 Jahren, was darauf hinweist, dass die Hauptgruppe der Kunden jung ist.
- Das erste Quartil (25%) umfasst die Altersgruppe von 24 bis 31 Jahren.
- Das dritte Quartil (75%) umfasst die Altersgruppe von 31 bis 49 Jahren, was deutlich breiter ist als die Altersgruppe des zweiten Quartils.

Diese Analyse unterstreicht erneut die Bedeutung der Kunden im dritten Quartil und die Notwendigkeit zusätzlicher Analysen und Maßnahmen seitens des Unternehmens, um die Bedürfnisse dieser Gruppe zu erfüllen.

![AltersverteilungDerKundenMithilfeBoxplot](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ClientsAgeBoxPlot.png)

**Verteilung der Nachrichtensendehäufigkeit nach Altersquantilen**

Das vorherige Boxplot-Diagramm zeigte die Notwendigkeit einer zusätzlichen Analyse der Kunden nach Altersquantilen. Insbesondere interessiert uns das dritte Quartil und der Aktivitätsrückgang dieser Altersgruppe. Im folgenden Balkendiagramm sehen wir, dass alle Gruppen ungefähr gleich verteilt sind, mit geringfügigen Unterschieden.

Der niedrigste Prozentsatz an Newsletter-Abonnements ist in der aktivsten Kundengruppe im Alter von 24-31 Jahren zu beobachten. Es lohnt sich, zusätzlich mit dieser Gruppe zu arbeiten, um ihr Interesse an Abonnementmaterialien zu erhöhen und die Bedürfnisse dieser Gruppe genauer zu untersuchen. Dies gilt auch für die Kunden des dritten Quartils.

![VerteilungNachrichtensendehäufigkeitNachAltersquantilen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/FashionNewsFrequencyAgeQuartile.png)

**Verteilung des Aktivitätsstatus nach Altersquantilen**

Das folgende Diagramm zeigt die Verteilung der aktiven Kunden nach Altersquantilen. Es ist zu erkennen, dass der Prozentsatz der aktiven Kunden ebenfalls relativ gleichmäßig auf alle Quartile verteilt ist, obwohl es immer noch kleine Unterschiede gibt, die untersucht und genutzt werden können, um die Aktivität in jeder Altersgruppe zu steigern.

![VerteilungAktivitätsstatusNachAltersquantilen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/ActiveStatusAgeQuartile.png)

**Verteilung der Kunden nach Postleitzahl**

Wir sehen, dass sehr viele Kunden die gleiche Postleitzahl haben. Ich gehe davon aus, dass dieser Index nichts mit dem physischen Index der Kunden zu tun hat und höchstwahrscheinlich der Index eines Paketterminals oder einer Lieferstelle für große Bestellungen ist

| Index  | Postal Code                                                      | Counts |
|--------|------------------------------------------------------------------|--------|
| 61034  | 2c29ae653a9282cce4151bd87643c907644e09541abc28ae87dea0d1f6603b1c | 120303 |
| 281937 | cc4ed85e30f4977dae47662ddc468cd2eec11472de6fac                   | 261    |
| 156090 | 714976379549eb90aae4a71bca6c7402cc646ae7c40f6c                   | 159    |
| 171208 | 7c1fa3b0ec1d37ce2c3f34f63bd792f3b4494f324b6be5                   | 157    |
| 126228 | 5b7eb31eabebd3277de632b82267286d847fd5d44287ee                   | 156    |

**Analyse der Gesamtzahl der verkauften Artikel nach Zeiträumen**

Für die Analyse und Visualisierung der Daten wurde der DataFrame df_transactions verwendet, der Informationen über Transaktionen für den Zeitraum vom 20.09.2018 bis zum 22.09.2020 enthält. Um die Analyse zu vereinfachen, wurden die Daten in zwei Jahresintervalle unterteilt:
- **Periode 1:** vom 20.09.2018 bis zum 19.09.2019
- **Periode 2:** vom 20.09.2019 bis zum 19.09.2020
Die Daten wurden wie folgt aufgeteilt:
```python
split_date1 = pd.to_datetime('2019-09-20')
split_date2 = pd.to_datetime('2020-09-20')
period1_transactions = df_transactions[df_transactions['t_dat'] < split_date1]
period2_transactions = df_transactions[(df_transactions['t_dat'] >= split_date1) & (df_transactions['t_dat'] < split_date2)]
```
Die Ergebnisse der Analyse zeigten Folgendes:
- Gesamtzahl der Verkäufe für den Zeitraum 20.09.2018 - 19.09.2019: **16.803.901**
- Gesamtzahl der Verkäufe für den Zeitraum 20.09.2019 - 19.09.2020: **14.887.938**
- Prozentuale Veränderung des Gesamtumsatzes: **-11,40%**

Die Visualisierung dieser Daten wird im folgenden Diagramm dargestellt:
![VerteilungGesamtmengeVerkauftenSKUsNachZeitraum](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/GesamtanzahlVerkauftenArtikelPlot.png)

**Visualisierung der durchschnittlichen Anzahl der Verkäufe pro Kunde nach Zeiträumen**

Die Ergebnisse der Analyse zeigten Folgendes:
- Durchschnittliche Anzahl der Verkäufe pro Kunde für den Zeitraum 20.09.2018 - 19.09.2019: **16,71**
- Durchschnittliche Anzahl der Verkäufe pro Kunde für den Zeitraum 20.09.2019 - 19.09.2020: **14,99**
- Prozentuale Veränderung der durchschnittlichen Anzahl von Verkäufen: **-10,26%**

Die Visualisierung dieser Daten wird im folgenden Diagramm dargestellt:

![DurchschnittlicheAnzahlVerkaufterSKUsProKundeNachZeitraum](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/DurchschnittlicheanzahlVerk%C3%A4ufeProKundelPlot.png)

**Visualisierung der Verteilung der Anzahl der Verkäufe pro Kunde mit Boxplot**

Für eine detailliertere Analyse wurde die Verteilung der Anzahl der Verkäufe pro Kunde nach Quartilen durchgeführt:
- **Erster Zeitraum (20.09.2018 - 19.09.2019):**
    - Anzahl der Kunden: 1.005.899
    - Minimum: 1.0000
    - Erster Quartil (25. Perzentil): 3.0000
    - Median (50. Perzentil): 8.0000
    - Oberer Quartil (75. Perzentil): 20.0000
    - Maximum: 897.0000

- **Zweiter Zeitraum (20.09.2019 - 19.09.2020):**
    - Anzahl der Kunden: 993.045
    - Minimum: 1.0000
    - Erster Quartil (25. Perzentil): 3.0000
    - Median (50. Perzentil): 8.0000
    - Oberer Quartil (75. Perzentil): 18.0000
    - Maximum: 1021.0000
  
- **Erster Quartil (25. Perzentil):** In beiden Zeiträumen bleibt der erste Quartil bei 3, was bedeutet, dass 25% der Kunden maximal 3 Käufe in beiden Zeiträumen getätigt haben.

- **Median (50. Perzentil):** Der Medianwert ist in beiden Zeiträumen gleich und beträgt 8. Das bedeutet, dass der mittlere Kunde in beiden Zeiträumen 8 Käufe getätigt hat.

- **Oberer Quartil (75. Perzentil):** Der Wert ist von 20 im ersten Zeitraum auf 18 im zweiten Zeitraum gesunken. Dies weist auf eine geringere Kaufaktivität bei den aktivsten 25% der Kunden hin.

- **Maximalwerte:** Die Erhöhung des maximalen Wertes der Anzahl der Käufe von 897 auf 1021 deutet auf das Auftreten einer kleinen Anzahl von Kunden hin, die im zweiten Zeitraum im Vergleich zum ersten deutlich mehr Käufe getätigt haben.

Die Visualisierung dieser Daten wird im folgenden Diagramm dargestellt:
![РаспределениеКоличестваПроданыхАртикуловНаОдногоКлиентаПоПериодам](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/AnzahlVerk%C3%A4ufeProKundeZweiPeriodeBoxPlot.png)


**Analyse des Gesamtumsatzes nach Zeiträumen**

Die Ergebnisse der Analyse zeigten Folgendes:
- Gesamtumsatz für den Zeitraum 20.09.2018 - 19.09.2019: **461.507,12**
- Gesamtumsatz für den Zeitraum 20.09.2019 - 19.09.2020: **419.750,19**
- Prozentuale Veränderung des Gesamtumsatzes: **-9,05%**

Die Visualisierung dieser Daten ist im folgenden Diagramm dargestellt:
![GesamtumsatzNachZeiträumen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/GesamtUmsatzlPlot.png)

**Visualisierung der durchschnittlichen Einkaufssumme pro Kunde nach Zeiträumen**

Die Ergebnisse der Analyse zeigten Folgendes:
- Durchschnittliche Einkaufssumme pro Kunde für den Zeitraum 20.09.2018 - 19.09.2019: **0,46**
- Durchschnittliche Einkaufssumme pro Kunde für den Zeitraum 20.09.2019 - 19.09.2020: **0,42**
- Prozentuale Veränderung der durchschnittlichen Einkaufssumme pro Kunde: **-7,87%**

Die Visualisierung dieser Daten ist im folgenden Diagramm dargestellt:

![DurchschnittlichenEinkaufssummeProKundeNachZeiträumen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/DurchschnittlicheEinkaufssummeProKundelPlot.png)

**Visualisierung der Verteilung der Einkaufssumme pro Kunde anhand eines Boxplots**

Für eine detailliertere Analyse wurde die Verteilung der Einkaufssumme pro Kunde nach Quartilen durchgeführt:

- **Erster Zeitraum (20.09.2018 - 19.09.2019):**
    - Anzahl der Kunden: 1.005.899
    - Minimum: 0,0008
    - Erster Quartil (25. Perzentil): 0,0826
    - Median (50. Perzentil): 0,2054
    - Oberer Quartil (75. Perzentil): 0,5136
    - Maximum: 26,3276
- **Zweiter Zeitraum (20.09.2019 - 19.09.2020):**
    - Anzahl der Kunden: 993.045
    - Minimum: 0,0008
    - Erster Quartil (25. Perzentil): 0,0830
    - Median (50. Perzentil): 0,2027
    - Oberer Quartil (75. Perzentil): 0,4862
    - Maximum: 34,9546
  
Die Werte des ersten Quartils und des Medians bleiben zwischen den Zeiträumen nahezu unverändert. Dies bedeutet, dass 50% der Kunden in beiden Zeiträumen ungefähr den gleichen Betrag ausgeben, was auf eine stabile Basis loyaler Kunden hinweist. Im oberen Quartil (75. Perzentil) ist ein Rückgang zu verzeichnen, was darauf hinweist, dass die aktivsten 25% der Kunden weniger ausgeben. Die maximalen Werte haben zugenommen, was darauf hindeutet, dass eine kleine Gruppe von Kunden im zweiten Zeitraum im Vergleich zum ersten deutlich mehr Geld ausgegeben hat. Diese Kunden zeigten eine extrem hohe Aktivität.

Die Visualisierung dieser Daten ist im folgenden Diagramm dargestellt:

![EinkaufssummeProKundeBoxplots](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/EinkaufssummeProKundeZweiPeriodeBoxPlot.png)

**Analyse und Visualisierung der Durchschnittspreisverteilung nach Perioden**

Die präsentierte Visualisierung zeigt Boxplots, die die Verteilung der durchschnittlichen Preise pro Artikel in zwei aufeinanderfolgenden Jahresperioden darstellen. 
![DurchschnittspreisverteilungNachPerioden](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/DurchschnittlichenPreisverteilungZweiPeriodeBoxPlot.png)

Hier sind die Schlüsselpunkte der Analyse:

**Durchschnittspreis:**
- Erster Zeitraum (20.09.2018 - 19.09.2019): Der durchschnittliche Preis betrug 0,0282 Einheiten.
- Zweiter Zeitraum (20.09.2019 - 20.09.2020): Der durchschnittliche Preis fiel leicht auf 0,0276 Einheiten.
- Die prozentuale Änderung des Durchschnittspreises zwischen den Perioden betrug -1,86 %, was auf einen geringfügigen Rückgang der Preise im zweiten Zeitraum hinweist.

**Preisverteilung:**
- Die Quartile der Preisverteilung zeigen, dass in beiden Perioden 25% der günstigsten Produkte Preise bis zu 0,0135 Einheiten hatten, während 50% der Produkte bis zu 0,0220 Einheiten im zweiten und 0,0218 Einheiten im ersten Zeitraum kosteten. Dies unterstreicht die Preisstabilität bei der Mehrheit der Produkte.
- Der maximale Preis eines Produkts erreichte in beiden Perioden 0,5068 Einheiten, was das Vorhandensein von Artikeln mit deutlich höheren als dem Durchschnittspreis belegt.
- Diese Visualisierung und Analyse helfen, die Dynamik der Produktpreise zwischen zwei Jahresintervallen zu bewerten und zeigen einen leichten Rückgang der durchschnittlichen Preise im letzten Zeitraum sowie eine allgemeine Preisstabilität bei den meisten Produkten. Diese Daten können nützlich sein für die Planung der Preisstrategie und die Analyse von Markttrends.

**Analyse der Kundenaktivität, des Mitgliederstatus im Club und der Häufigkeit des Erhalts von Modenachrichten nach Zeiträumen**

Diese Gruppe von Visualisierungen zeigt geringfügige Änderungen in der Kundenaktivität, dem Mitgliederstatus im Club und der Häufigkeit des Erhalts von Modenachrichten, aufgeteilt auf zwei aufeinanderfolgende Perioden: vom 20. September 2018 bis zum 19. September 2019 und vom 20. September 2019 bis zum 20. September 2020.

![KundenaktivitätMitgliederstatusHäufigkeit](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/%D0%90ktivit%C3%A4tClubmitgliedsstatusH%C3%A4ufigkeit.png)

Hier sind detaillierte Beobachtungen für jede Kategorie:

**Kundenaktivität nach Zeitraum:**
- Die Anzahl der aktiven und inaktiven Kunden bleibt zwischen den Perioden fast unverändert, mit einem leichten Rückgang der Anzahl der aktiven Kunden im zweiten Zeitraum. Dies könnte auf übliche Schwankungen in der Kundenbasis oder Änderungen in den Engagement-Strategien zurückzuführen sein.

**Mitgliederstatus im Club nach Zeitraum:**
- Die meisten Kunden bleiben aktive Clubmitglieder mit sehr geringen Änderungen zwischen den Perioden, was auf eine relative Stabilität des Clubs hinweist, aber auch auf neue Engagements.
  
**Häufigkeit des Erhalts von Modenachrichten nach Zeitraum:**
- Die Häufigkeit, mit der Kunden Modenachrichten erhalten, zeigt ebenfalls geringfügige Änderungen. Die meisten Kunden erhalten keine Nachrichten, gefolgt von denen, die Nachrichten erhalten. Ein kleinerer Teil der Kunden erhält monatlich Nachrichten. Die Verteilung bleibt zwischen den Perioden stabil, was auf eine unveränderte Kommunikationsstrategie hinweist.

Die Visualisierungen zeigen, dass die Kundenbasis hinsichtlich der Aktivität, Clubmitgliedschaft und Informationsaustausch relativ stabil ist, mit nur minimalen Schwankungen über die betrachteten Zeiträume, die nicht den Schwankungen im Verkaufsvolumen entsprechen, die wir zuvor festgestellt haben.

**Visualisierungen des Verkaufsvolumens nach Monaten für zwei Perioden (September 2018 — September 2019 und September 2019 — September 2020)**

![VisualisierungVerkaufsvolumeNachMonaten](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatBoxPlot.png)

Basierend auf der Visualisierung können folgende Schlussfolgerungen gezogen werden:

- **Saisonalität der Verkäufe:** Das Diagramm zeigt deutlich saisonale Schwankungen im Verkaufsvolumen. Zum Beispiel ist ein Anstieg der Verkäufe von April bis Juni zu beobachten, was mit saisonalen Marketingkampagnen oder einem Anstieg der Nachfrage im Frühjahr/Sommer zusammenhängen könnte.

- **Jahr-zu-Jahr-Vergleich:** Es ist ein allgemeiner Rückgang der Verkäufe im zweiten Zeitraum im Vergleich zum ersten in den meisten Monaten zu beobachten. Dieser Rückgang könnte auf verschiedene Faktoren zurückzuführen sein, wie Veränderungen im wirtschaftlichen Umfeld, der Konkurrenz, Veränderungen in den Verbraucherpräferenzen oder internen Strategien des Unternehmens.

- **Abschwung im Verkauf:** Ein besonders deutlicher Rückgang der Verkäufe ist in den Wintermonaten und im August festzustellen, was mit der Verkaufssaison zusammenhängen könnte. Während Verkaufszeiten, obwohl ein Anstieg des Verkaufsvolumens beobachtet wird, kann der durchschnittliche Verkaufspreis sinken, was den Gesamtumsatz beeinflusst. Eine weitere Untersuchung der Dynamik der Durchschnittspreise pro Monat für beide Perioden wird bei der Planung der Preisgestaltung und Marketingaktionen helfen, um die Rentabilität in diesen Schlüsselmonaten zu maximieren.

**Analyse der Verkaufsmengen pro Monat für zwei Perioden (September 2018 — September 2019 und September 2019 — September 2020)**

Das Diagramm der Verkaufsmengen pro Monat zeigt deutlich saisonale Schwankungen im Verkaufsvolumen. Ein Rückgang der Verkäufe ist in den Wintermonaten zu beobachten, einschließlich der Ausverkaufszeiten, was auf eine allgemeine Abnahme der Verbraucheraktivität oder eine Änderung der Verbraucherpräferenzen zu dieser Jahreszeit hinweisen könnte. Zudem ist erkennbar, dass die Sommermonate durch höhere Verkaufszahlen gekennzeichnet sind, was mit einer saisonalen Nachfragesteigerung nach bestimmten Produktkategorien, wie leichter Kleidung, zusammenhängen könnte.

![VerkaufsmengenProMonatFürZweiPerioden](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/AnzahlDerVerk%C3%A4ufeProMonatPlot.png)

**Analyse der Durchschnittspreise pro Monat für zwei Perioden (September 2018 — September 2019 und September 2019 — September 2020)**

Die Durchschnittspreise pro Monat zeigen ein relatives Absinken in den Sommermonaten und ein Ansteigen in den Herbstmonaten. Dies kann mit einer Veränderung des auf dem Markt angebotenen Produktangebots zusammenhängen, wobei im Sommer günstigere Artikel wie T-Shirts vorherrschen, während im Winter teurere Artikel wie Pullover mehr verkauft werden. Die Preisdynamik könnte auch saisonale Verkäufe und Aktionen widerspiegeln, die von Geschäften durchgeführt werden, um Kunden anzuziehen.

![DurchschnittspreiseProMonatFürZweiPerioden](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/DurchschnittsPreisProMonatPlot.png)

**Verteilung der Preise nach verschiedenen Produktkategorien**

Diese Diagramm hilft zu verstehen, welche Segmente höhere oder niedrigere Preise bieten und welche eine größere Variabilität in der Preisgestaltung aufweisen. Zum Beispiel ist die Preisspanne in der Kategorie der Kinderbekleidung relativ klein. Dies deutet auf eine stabilere und vorhersehbare Preisgestaltung hin, was ein wichtiger Faktor für Eltern ist, die Bekleidung für ihre Kinder planen.
In der Kategorie Damenbekleidung (Ladieswear) sehen wir eine deutlich größere Preisspanne sowie viele Ausreißer, was auf eine hohe Variabilität in der Preisgestaltung hindeutet. Dies könnte mit einem breiteren Sortiment an Produkten zusammenhängen, das sowohl erschwinglichere Alltagsartikel als auch exklusive oder Premium-Modelle umfasst. Die hohe Preisspanne und zahlreichen Ausreißer bei den Preisen zeigen, dass die Käufer aus einer breiten Produktpalette wählen können, abhängig von ihren Bedürfnissen und ihrem Budget.

![VerteilungDerPreiseNachProduktkategorien](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/PreiseNachProduktkategorien.png)

**Verteilung der Umsatzanteile nach Produktkategorien**

Die untenstehende Kreisdiagramm zeigt die Umsatzanteile verschiedener Produktkategorien für den betrachteten Zeitraum:

- **Damenbekleidung (Ladieswear):** Mit einem Anteil von 48,4% markiert sie die höchste Nachfrage innerhalb der Produktkategorien.
- **Divided:** Dieses Segment, das auf trendige Jugendmode ausgerichtet ist, trägt 21,4% zum Gesamtumsatz bei, was seine Beliebtheit unter jungen Leuten bestätigt.
- **Unterwäsche und Strumpfhosen (Lingeries/Tights):** Mit einem Anteil von 13,1% zeigt dieses Segment ebenfalls einen signifikanten Beitrag zum Gesamtumsatz.
- **Herrenbekleidung (Menswear):** Hat einen Anteil von 5,5% am Gesamtumsatz, was auf eine stabile Nachfrage hinweist.
- **Damenaccessoires (Ladies Accessories):** Mit einem Umsatzanteil von 4,8% bleiben Accessoires ein wichtiger Teil des Produktportfolios.
- **Sportbekleidung (Sport):** Sportartikel machen 4,1% des Marktes aus, was ihre Rolle in einem spezialisierten Segment unterstreicht.
- **Kinderbekleidung (Other):** Beinhaltet alle Arten von Kinderprodukten und macht 2,7% des Gesamtumsatzes aus. Dies reflektiert ein relativ geringes Interesse in diesem Segment, zeigt jedoch erhebliches Entwicklungspotenzial. Mütter, die Hauptkäuferinnen in den Segmenten Damen- und Jugendmode, könnten als Zielgruppe für die Expansion in den Kinderbereich dienen.

![UmsatzanteileNachProduktkategorienPie](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/UmsatzanteileProductIndexPie.png)

**Visualisierungen des Verkaufsvolumens und der verkauften Einheiten nach Produktkategorien für zwei Perioden (September 2018 – September 2019 und September 2019 – September 2020**

Diese Visualisierungen zeigen das Verkaufsvolumen und die Anzahl der verkauften Einheiten für verschiedene Produktkategorien von H&M im Zeitraum von September 2018 bis September 2020. Sie ermöglichen es uns zu erkennen, welche Kategorien den größten Beitrag zum Gesamtumsatz des Unternehmens leisten.

Wesentliche Beobachtungen:

- **Dominanz der Damenbekleidung:** Die Kategorie 'Damenbekleidung' (Ladieswear) zeigte das höchste Verkaufsvolumen, was auf eine hohe Nachfrage in diesem Segment hinweist. Gefolgt wird sie von der Kategorie 'Divided', die auf den Jugendmarkt ausgerichtet ist, und 'Lingeries/Tights' (Unterwäsche und Strumpfhosen), was ein stetiges Interesse an diesen Produkten zeigt.

- **Potenzial für Wachstum in anderen Kategorien:** Trotz des Erfolgs der Damenbekleidung besteht Potenzial für Wachstum in den Bereichen Herren- und Kinderbekleidung. Die Visualisierungen zeigen, dass diese Kategorien geringere Verkaufsvolumen aufweisen, was ein Ziel für zukünftige Marketing- und Produktstrategien sein könnte.

- **Rückgang bei Kinderbekleidung:** Besonders auffällig ist der starke Rückgang der Verkäufe in der Kategorie Kinderbekleidung im zweiten Zeitraum, was auf die Notwendigkeit hinweist, Angebote und Ansätze in diesem Segment zu überdenken.

- **Ausnahme im Bereich Sportbekleidung:** Die einzige Kategorie, die Wachstum zeigte, war 'Sport' (Sportbekleidung), was das veränderte Verbraucherverhalten und das wachsende Interesse an einem gesunden Lebensstil hervorhebt.

![VerkaufssummeInProduktkategorienNachPeriodenWarm](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeInProduktkategorien.png)

![VerkauftenEinheitenInProduktkategorienNachPeriodenWarm](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkauftenEinheitenInProduktkategorien.png)

![VerkaufssummeInProduktkategorienNachPeriodenPlot](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeInProduktIndexPlot.png)

![VerkauftenEinheitenInProduktkategorienNachPeriodenPlot](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkauftenEinheitenInProduktIndexPlot.png)

**Visualisierung der monatlichen Verkäufe nach Schlüsselproduktkategorien für zwei Perioden (September 2018 bis September 2019 und September 2019 bis September 2020)**

Die folgenden Diagramme zeigen die monatlichen Verkäufe in Schlüsselproduktkategorien: Damenbekleidung (Ladieswear), Damenaccessoires (Ladies Accessories), Sportbekleidung (Sport), Divided (Jugendmode), Unterwäsche/Strumpfwaren (Lingeries/Tights) und Herrenbekleidung (Menswear).

- **Damenbekleidung und Damenaccessoires:** Diese Kategorien zeigen ähnliche Trends, mit einem Anstieg der Verkäufe in den Monaten vor dem Jahresende des zweiten Zeitraums, gefolgt von einem Rückgang der Verkäufe in den ersten sieben Monaten des Jahres 2020.
- **Sportbekleidung:** In dieser Kategorie ist ein Anstieg zu Beginn des Jahres zu verzeichnen, insbesondere von Januar bis März, was mit Neujahrsvorsätzen zum Sporttreiben zusammenhängen könnte. Ein zusätzlicher Anstieg der Verkäufe in den Sommermonaten könnte durch Marketingaktionen, Sortimentserneuerungen oder teilweise Aufhebung von Pandemiebeschränkungen bedingt sein.
- **Unterwäsche/Strumpfwaren:** Diese Kategorie zeigt eine deutliche Saisonalität mit einem Verkaufshöhepunkt von April bis Juli, was auf eine erhöhte Nachfrage in der warmen Jahreszeit oder spezielle Aktionen hinweisen könnte.
- **Herren- und Jugendbekleidung:** Zeigen fast durchgehend einen Rückgang der Verkäufe in allen Monaten des zweiten Zeitraums.

![VerkaufssummeProMonatLadieswear](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatIndex%26Ladieswear.png)

![VerkaufssummeProMonatDivided](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatIndex%26Divided.png)

![VerkaufssummeProMonatLingeries_Tights](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatIndex%26Lingeries_Tights.png)

![VerkaufssummeProMonatMenswear](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatIndex%26Menswear.png)

![VerkaufssummeProMonatLadies_Accessories](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatIndex%26Ladies_Accessories.png)

![VerkaufssummeProMonatSport](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonatIndex%26Sport.png)

**Verteilung der Preise nach Produkttypen in den drei Hauptbekleidungskategorien**

Diese Visualisierung zeigt die Preisverteilung verschiedener Produkttypen in den drei größten Bekleidungskategorien: "Garment Full body", "Garment Lower body" und "Garment Upper body". Der Graph ermöglicht eine anschauliche Bewertung der Preisverteilung innerhalb jeder Kategorie und hebt teurere sowie zugänglichere Produkte hervor. Zum Beispiel zeigen "Coats" und "Jackets" eine breite Preisspanne, während Produkte wie "T-Shirts" und "Tops" eine kompaktere Verteilung aufweisen, was auf eine relativ stabile und erschwingliche Preiskategorie hinweist.

![VerteilungDerPreiseNachProdukttypen](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/PreiseInDreiProduktgruppen%20(1).png)

**Wärmekarten der Verkaufsvolumen und verkauften Einheiten in den drei Hauptbekleidungskategorien über zwei Perioden (September 2018 – September 2019 und September 2019 – September 2020)**

Wärmekarten illustrieren die Verteilung der Verkäufe und der verkauften Einheiten über zwei Jahresperioden in den drei Hauptbekleidungskategorien. Die Farbpalette der Karten spiegelt das Verkaufsniveau wider: Dunklere Töne zeigen höhere Werte an, während hellere Töne niedrigere Werte anzeigen. Diese visuelle Darstellung ermöglicht es, schnell die Jahre und Kategorien mit der höchsten Aktivität zu bewerten und die Veränderungen zwischen den beiden Perioden zu vergleichen.
Besonders bemerkenswert ist, dass trotz eines allgemeinen Rückgangs der Verkäufe bei den meisten Produkttypen die Verkäufe von Kleidern (Dresses), die den zweiten Platz sowohl im Volumen als auch in der Anzahl der Verkäufe einnehmen, eine relative Stabilität zeigten. In der zweiten Periode erhöhte sich die Anzahl der verkauften Kleider, obwohl der Verkaufsumsatz leicht sank. Diese Stabilität, im Gegensatz zu anderen Produkttypen, erfordert zusätzliche Untersuchungen. Neben Kleidern zeigten auch die Kategorien Top, Leggings/Tights und Skirt eine relative Stabilität, während in der Kategorie Blazer sogar ein Wachstum der Verkäufe beobachtet wurde. Jeder dieser Produkttypen erfordert eine zusätzliche Analyse und Datensammlung, um die Gründe für solche Variabilitäten in den Verkäufen zu verstehen.

![WärmekarteVerkaufsvolumenZweiPeriodenInDreiKategorien](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeInDreiProduktgruppen.png)
![WärmekarteVerkauftenEinhaltenZweiPeriodenInDreiKategorien](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkauftenEinheitenInDreiProduktgruppen.png)

**Säulendiagramme des Verkaufsvolumens und der verkauften Einheiten in den drei Hauptbekleidungskategorien für zwei Perioden (September 2018 – September 2019 und September 2019 – September 2020)**

Die Säulendiagramme zeigen dieselben Daten, die auch in den Wärmekarten für die beiden betrachteten Zeiträume dargestellt sind. Diese Diagramme ermöglichen einen visuellen Vergleich der Verkaufsvolumen zwischen verschiedenen Jahren und Produkttypen und veranschaulichen deutlich die Unterschiede zwischen den beiden Perioden.

Aus der Analyse der Säulendiagramme geht hervor, dass die drei Spitzenreiter im Verkauf unter den Produkttypen Hosen (Trousers), Kleider (Dresses) und Pullover (Sweater) sind. Diese Kategorien sind entscheidend für die Aufrechterhaltung eines hohen Verkaufsniveaus. Trotz ihrer Bedeutung ist jedoch in den Kategorien Hosen und Pullover ein erheblicher Rückgang der Verkäufe im zweiten Zeitraum zu verzeichnen. Dies weist auf die Notwendigkeit einer weiteren Analyse und möglicher Anpassungen der Marketing- und Produktstrategien hin, um einem weiteren Rückgang der Verkäufe in diesen Schlüsselkategorien entgegenzuwirken.

![BoxPlotVerkaufsvolumenZweiPeriodenInDreiKategorien](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeInDreiProduktgruppenPlot.png)
![BoxPloVerkauftenEinhaltenZweiPeriodenInDreiKategorien](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkauftenEinheitenInDreiProduktgruppenPlot.png)

**Visualisierungen der monatlichen Verkäufe nach Schlüsselprodukttypen**

Unten sind Visualisierungen der monatlichen Verkäufe für die wichtigsten Produkttypen dargestellt, einschließlich 'Hosen' (Trousers), 'Kleider' (Dress), 'Pullover' (Sweater), 'Jacken' (Jacket), 'Blusen' (Blouse), 'T-Shirts' (T-shirt), 'Röcke' (Skirt), 'Oberteile' (Top), 'Hemden' (Shirt) und 'Shorts'. Jedes Diagramm zeigt die Verkaufsdynamik über zwei Zeiträume: von September 2018 bis September 2019 und von September 2019 bis September 2020. Diese Daten zeigen Trends, Spitzenzeiten und Rückgangsperioden für jeden Produkttyp.

Haupterkenntnisse aus den Visualisierungen:

- **Saisonalität:** Die Diagramme veranschaulichen deutlich die saisonalen Schwankungen im Verkauf, was die Planung von Lagerbeständen und die Anpassung von Marketingkampagnen erleichtert. Jacken und Pullover erfahren eine erhöhte Nachfrage in der Herbst-Winter-Periode, während Shorts in den Sommermonaten beliebter sind.
- **Vergleich der Verkäufe zwischen den Perioden:** Der visuelle Vergleich der Verkäufe hilft, die Wirksamkeit der angewandten Verkaufsstrategien und die vorgenommenen Sortimentsänderungen zu bewerten.
- **Besondere Beobachtungen:** Zum Beispiel zeigte die Kategorie 'Kleider' eine Stabilität über die Jahre hinweg, mit einem Anstieg der Verkäufe von Oktober bis Februar im zweiten Jahr. Die folgenden Monate waren jedoch von einem Rückgang geprägt, was wahrscheinlich mit der Coronavirus-Pandemie zusammenhängt. Eine ähnliche Dynamik zeigten auch die Blusen, deren Verkäufe erheblich fielen, besonders von März bis Juli 2020, was mit einer verringerten Nachfrage nach Bürokleidung während der Pandemie zusammenhängen könnte.

![BlusenProMonat](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Blouse.png)

![KleiderProMonat](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Dress.png)

![JacketProMonat](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Jacket.png)

![HemdenProMonat](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Shirt.png)

![ShortsProMonat](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Shorts.png)

![RöckeProMonate](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Skirt.png)

![PulloverProMonate](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Sweater.png)

![TshirtsProMonate](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26T-shirt.png)

![TopsProMonate](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Top.png)

![HosenProMonate](https://github.com/OlhaAD/EDA_IDA_H_and_M_Python/blob/main/visualizations/VerkaufssummeProMonat%26Trousers.png)

**Basierend auf der Datenanalyse lassen sich folgende Schlussfolgerungen ziehen:**

- Die größte Anzahl an Artikeln gehört zur Gruppe "Garment Upper body".
- Die Artikel sind auch in Sektionen und Kategorien unterteilt, was eine detailliertere Analyse des Sortiments ermöglicht.
- Die größte Gruppe nach Warentyp sind Hosen ("Trousers"), mit über 11.169 Artikeln, gefolgt von Kleidern ("Dresses") mit 10.362 Artikeln.
- Die am häufigsten vorkommende Farbe der Artikel ist Schwarz ("Black") mit 22.670 Einheiten, und der am häufigsten vorkommende Druck ist einfarbig ("Solid") mit 49.747 Positionen.
- Der Rückgang der Aktivität von Kunden im Alter von etwa 40 Jahren und der lange Schwanz in Richtung älterer Kunden stellen wichtige Bereiche für weitere Untersuchungen dar.
-Die Daten zu den Verkaufszahlen und zur Statistik bestätigen eine geringere Käuferaktivität. Der Gesamtumsatz pro Jahr ist um 9,05% gesunken, und die Gesamtanzahl der verkauften Positionen pro Jahr ist um 11,40% gesunken.
- Die Werte des ersten Quartils und des Medians für die Einkaufssumme und die Anzahl der Käufe bleiben zwischen den Zeiträumen nahezu unverändert. Dies bedeutet, dass 50% der Kunden in beiden Zeiträumen ungefähr die gleiche Anzahl von Käufen tätigen und ungefähr den gleichen Betrag ausgeben. Dies weist auf eine stabile Basis loyaler Kunden hin.
- Rückgang der Kaufaktivität unter den Top-Kunden: Im oberen Quartil (75. Perzentil) ist sowohl bei der Einkaufssumme als auch bei der Anzahl der Käufe ein Rückgang zu verzeichnen. Dies deutet darauf hin, dass die aktivsten 25% der Kunden weniger Käufe tätigen und weniger Geld ausgeben.
- Die maximalen Werte sowohl für die Einkaufssumme als auch für die Anzahl der Käufe haben zugenommen. Dies bedeutet, dass eine kleine Gruppe von Kunden im zweiten Zeitraum im Vergleich zum ersten Zeitraum deutlich mehr Käufe getätigt und mehr Geld ausgegeben hat. Diese Kunden zeigten eine extrem hohe Aktivität.
-  Saisonalität und Einfluss von Marketingkampagnen: Die Daten zeigen eine klare Saisonalität der Verkäufe. Die Sommermonate zeichnen sich durch erhöhte Umsätze aus, die möglicherweise auf saisonale Marketingkampagnen und einen natürlichen Anstieg der Verbrauchernachfrage nach bestimmten Warenarten, beispielsweise leichter Kleidung, zurückzuführen sind. Im Winter ist ein Rückgang sowohl des Verkaufsvolumens als auch der verkauften Einheiten zu verzeichnen.
- Preistrends: Die durchschnittlichen Preise schwanken im Laufe des Jahres, mit Tiefstständen in den Sommermonaten und Anstiegen in den kälteren Monaten. Diese Änderung spiegelt möglicherweise saisonale Veränderungen im Produktmix wider, wobei im Sommer günstigere Artikel wie T-Shirts und Shorts und im Winter teurere Artikel wie Pullover und Mäntel verkauft werden.
- Allgemeiner Rückgang der Umsätze und Preise: Im zweiten Untersuchungszeitraum kommt es im Vergleich zum ersten Zeitraum zu einem allgemeinen Rückgang sowohl der Umsätze als auch der Durchschnittspreise. Dieser Rückgang kann durch eine Reihe von Faktoren verursacht werden, darunter Veränderungen im wirtschaftlichen Umfeld, im Marktwettbewerb sowie Veränderungen in den Vorlieben und im Verhalten der Verbraucher.
- Die Analyse des Umsatzvolumens nach Produktbereichen zeigt, dass Frauen die Hauptkäufer sind. Die gefragtesten Produktkategorien sind Damenbekleidung (Ladieswear), junge Mode (Divided) und Unterwäsche sowie Strumpfhosen (Lingeries/Tights). Herrenbekleidung (Menswear) und Kinderbekleidung machen nur 5,5 % bzw. 2,7 % des Gesamtumsatzes aus, was auf ihren geringen Marktanteil und das Potenzial für Wachstum hinweist. Dies unterstreicht die Möglichkeit, das Sortiment in diesen Segmenten zu erweitern, um mehr Kunden anzuziehen und die Verkäufe in den unterrepräsentierten Kategorien zu steigern
- Dynamik des Wachstums oder Rückgangs bestimmter Produkttypen: Zum Beispiel zeigten die Verkäufe von Kleidern (Dresses), die nach Hosen (Trousers) den zweiten Platz sowohl im Volumen als auch in der Anzahl der Verkäufe einnehmen, eine relative Stabilität, während die Verkäufe von Hosen erheblich fielen. Neben Kleidern zeigten auch die Produkte der Kategorien Top, Leggings/Tights und Skirt eine relative Stabilität, während in der Kategorie Blazer sogar ein Wachstum der Verkäufe zu verzeichnen war. Besondere Aufmerksamkeit sollte den Kategorien und Jahren gewidmet werden, in denen ein signifikantes Wachstum oder ein Rückgang der Verkäufe zu beobachten ist. Dies kann auf erfolgreiche oder erfolglose Änderungen im Sortiment oder in den Marketingaktionen hinweisen.
