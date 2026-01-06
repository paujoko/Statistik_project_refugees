# Statistik_project_refugees
Statistik Projekt Flüchtlingsströme


Dieses Statistikprojekt enthält eine Analyse zu globalen Flüchtlingsströmen anhand von den aktuellsten UNHCR Daten.
Ziel des Projekts ist es, reale UNHCR-Flüchtlingsdaten systematisch auszuwerten und mithilfe statistischer Methoden Fragestellungen (Hypothesen) zu untersuchen, wie wir sie im Statistik-Unterricht behandelt haben.

Das Projekt kombiniert Datenaufbereitung, explorative Analyse, Visualisierung sowie Hypothesentests.


# Projektstruktur

STATISTIK_PROJEKT
│
├── .idea/
├── .venv/
│
├── additional_data/                     
│   ├── API_NY.GDP.PCAP.CD_DS2_en_csv_v2_308461.csv
│   ├── API_SP.POP.TOTL_DS2_en_csv_v2_280659.csv
│   ├── custom.geo.json
│   ├── Metadata_Country_API_NY.GDP.PCAP.CD_DS2_en_csv_v2_308461.csv
│   ├── Metadata_Country_API_SP.POP.TOTL_DS2_en_csv_v2_280659.csv
│   ├── Metadata_Indicator_API_NY.GDP.PCAP.CD_DS2_en_csv_v2_308461.csv
│   └── Metadata_Indicator_API_SP.POP.TOTL_DS2_en_csv_v2_280659.csv
│
├── archive/                             
│   ├── asylum_seekers_monthly.csv
│   ├── asylum_seekers.csv
│   ├── demographics.csv
│   ├── persons_of_concern.csv
│   ├── resettlement.csv
│   └── time_series.csv
│
├── Hypothesen/
│   ├── Hypothese_1_Flüchtlinge_früher_vs_heute/
│   │   ├── master_statistik_fluechtlinge.ipynb
│   │   ├── refugee_vl8_analysis.ipynb
│   │   └── readme_Hypothese_1.md
│   │
│   └── Hypothese_2_zusammenhang_zwischen_Wohlstand_und_Flüchtlingsaufnahme/
│       ├── Append_continent.ipynb
│       ├── Append_gdp.ipynb
│       ├── Zusammenhang_zwischen_Wohlstand_und_Flüchtlingsaufnahme.ipynb
│       └── README_Hypothese_2.md
│
├── output_csv_files/                   
│   ├── Destination_refugees_per_capita_with_gdp.csv
│   ├── Destination_refugees_per_capita.csv
│   ├── flows_with_coords_1970_plus.csv
│   ├── flows_with_coords_2016.csv
│   ├── flows_with_coords_all_years.csv
│   ├── Origin_country_refugee_flow.csv
│   ├── Origin_refugees_per_capita.csv
│   ├── output_with_continent.csv
│   └── world_with_centroids.geojson
│
├── Kennzahlen_berechnen.ipynb
├── Flowmap.ipynb
├── Boxplot_histogram.ipynb
└── README.md

# Datengrundlage

Die Analysen basieren auf öffentlich zugänglichen Flüchtlings- und Bevölkerungsdaten von der UNHCR. Wir haben die Datensätze über Kaggle heruntergeladen und sie im "archive" Ordner plaziert. Die sechs Datensätze sind wie folgt strukturiert: 

-time_series (Hauptdatensatz)

Zeitreihendaten im Long-Format (1951–2016).
Eine Zeile pro Jahr, Land, Herkunft und Populationstyp (z. B. Refugees).

-persons_of_concern

Jährliche Bestandszahlen (1951–2016) zu allen Personengruppen unter UNHCR-Schutz
(Refugees, IDPs, Stateless Persons etc.).
Einziger Unterschied zu time_series ist der Umgang der Gliederung mit "retunees".

-asylum_seekers_monthly

Monatliche Asylanträge ausgewählter Länder (1999–2017).
Nützlich für kurzfristige Trends und Ereignisse.

-asylum_seekers

Jährliche Daten zu Asylverfahren (2000–2016), inklusive Anerkennungen, Ablehnungen und offenen Fällen.

-demographics

Demografische Struktur von Flüchtlingspopulationen (2001–2016), z. B. Alter und Geschlecht.

-resettlement

Daten zu Umsiedlungen von Flüchtlingen in Drittstaaten (1959–2016).

In diesem Projekt haben wir uns hauptsächlich auf den Datensatz time_series konzentriert, da dieser die umfassendste und vollständigste Datenbasis darstellt.
Für die Berechnung der Kennzahlen und die anschliessenden Analysen haben wir uns bewusst auf die Personengruppen Asylbewerber sowie Refugees (incl. refugee-like situations) beschränkt.
Der Fokus des Projekts liegt auf der Analyse internationaler Flüchtlingsbewegungen zwischen Ländern.
Personengruppen wie internally displaced persons oder Reternees wurden daher nicht berücksichtigt, da sie entweder innerhalb ihres Herkunftslandes verbleiben oder sich bereits in einem Rückkehrprozess befinden und somit nicht dem zentralen Fokus des Projekts auf Flüchtlinge entsprechen.

Diese Einschränkung ermöglicht eine klarere Interpretation der Ergebnisse und stellt sicher, dass die analysierten Kennzahlen direkt die grenzüberschreitenden Flüchtlingsströme widerspiegeln.

# Datenerweiterung

Zur besseren Einordnung der Flüchtlingszahlen wurden zusätzlich von der World Bank Group zwei Datensätze eingebunden. Diese befinden sich im additional_data Ordner. 

Einerseits beinhalted der "API_SP.POP.TOTL_DS2_en_csv_v2_280659" für jedes Jahr die Populationsgrösse für alle Länder. 

Die Datei namens "API_NY.GDP.PCAP.CD_DS2_en_csv_v2_308461" liefert den GDP per capita für jedes Land pro Jahr. 


# Kennzahl

Um die absoluten Flüchtlingszahlen sinnvoll vergleichen zu können, haben wir für jedes Land pro Jahr eine Kennzahl berechnet, die den Flüchtlingsstrom in relation zur derzeitigen Einwohnerzahl zeigt. Absolute Zahlen sind stark von der Grösse eines Landes abhängig und erlauben nur eingeschränkt Vergleiche zwischen Ländern. 

Zunächst wurden die jährlichen Flüchtlingszahlen pro Land zusammengerechnet. 	Anschliessend haben wir ein zusätzlicher Datensatz mit der jährlichen Gesamtbevölkerung pro Land geladen. Beide Datensätze wurden über Land und Jahr zusammengeführt. Auf dieser Basis wurde die Kennzahl Flüchtlinge pro Kopf pro 1000 Einwohner berechnet: 
Flüchtlinge pro Population = Anzahl Flüchtlinge / Gesamtbevölkerung

Diese Kennzahl normalisiert die Flüchtlingszahlen und macht Länder unabhängig von ihrer absoluten Bevölkerungsgrösse vergleichbar. Dadurch wird sichtbar:
	•	welche Länder relativ stark von Flüchtlingsbewegungen betroffen sind,
	•	wie hoch die Belastung pro Einwohner tatsächlich ist,
	•	dass kleine Länder mit moderaten absoluten Zahlen teilweise eine sehr hohe relative Aufnahme haben.

# Arbeitsteilung

Die Projektarbeit wurde von Beginn an gemeinsam geplant und diskutiert. Zu Projektstart haben wir zusammen überlegt, welche Fragestellungen sinnvoll sind, wie der Datensatz aufgebaut ist und welche statistischen Methoden aus dem Unterricht angewendet werden können. Viele zentrale Entscheidungen (Datenauswahl, Zeiträume, Kennzahlen, Hypothesen) wurden im Team erarbeitet und regelmässig gemeinsam besprochen.

Trotz der engen Zusammenarbeit hatte jedes Teammitglied einen inhaltlichen Schwerpunkt:
	•	Paul
Fokus auf komplexe Visualisierungen und Plots, insbesondere Karten, Flowmaps und grafische Darstellungen von Flüchtlingsbewegungen zwischen Ländern und Regionen. Zusätzlich war Paul für das Mapping der berechneten Kennzahl (Flüchtlinge pro Population) zuständig, um relative Flüchtlingszahlen geografisch vergleichbar darzustellen.
	•	Torsten
Schwerpunkt auf Regressionsanalysen und der Untersuchung von Zusammenhängen zwischen Variablen. Zusätzlich arbeitete er an der technischen Umsetzung und Interpretation der Regressionsmodelle.
	•	Valeria
Fokus auf die Hypothesentests und statistische Auswertung, inklusive Permutationstests, Effektgrössen, Interpretation der Ergebnisse sowie der inhaltlichen Einordnung der Resultate.

Während des gesamten Projekts haben wir uns regelmässig zusammengesetzt, um Zwischenergebnisse zu besprechen, Probleme gemeinsam zu lösen und das weitere Vorgehen abzustimmen. Dadurch sind viele Teile des Projekts nicht isoliert entstanden, sondern durch kontinuierlichen Austausch und gemeinsame Weiterentwicklung.

# Unsere Notebooks

# EDA
Unter dem Ordner EDA befinden sich explorative Analysen der verfügbaren UNHCR-Datensätze.
Diese Analysen dienten in erster Linie dazu, ein grundlegendes Verständnis der Datenstruktur, der zeitlichen Abdeckung sowie der enthaltenen Variablen zu gewinnen.

# Hypothese
Die statistischen Fragestellungen des Projekts sind in separaten Hypothesen-Ordnern organisiert.
Für jede Hypothese existiert ein eigenes Notebook sowie ein eigenes README, in dem die Fragestellung, das methodische Vorgehen und die wichtigsten Ergebnisse kurz beschrieben werden.

# Visualisieige
Die Visualisierungen des Projekts umfassen Karten, Flowmaps sowie zeitliche Darstellungen von Flüchtlingsbewegungen.
Dazu wurden UNHCR-Daten mit geografischen Informationen verknüpft, Länderbezeichnungen vereinheitlicht und Flüchtlingsströme zwischen Herkunfts- und Aufnahmeländern aggregiert.

Auf dieser Basis entstanden statische und animierte Weltkarten, die globale, kontinentale sowie länderbezogene Zu- und Abwanderungsströme darstellen.
Die detaillierten technischen und inhaltlichen Erklärungen zu den Visualisierungen befinden sich direkt in den jeweiligen Notebooks.

# kennzahle

# Regression


# Prompt Table

# Statistik_project_refugees
Statistik Projekt Flüchtlingsströme

Wie kann ich Ländernamen aus diesen beiden CSV files vereinheitlichen/mappen?
Wie lade ich GeoJSON-Weltdaten mit GeoPandas und bereite sie für Analysen vor gebe mir code Beispiele?
Wie kann ich geografische Mittelpunkte aus Polygon-Geometrien berechnen?
Wie verknüpfe ich tabellarische Daten mit GeoJSON-Geodaten?
Wie kann ich Flüchtlingsbewegungen als Pfeile auf einer Weltkarte darstellen?
Wie visualisiere ich gerichtete Flüsse zwischen Herkunfts- und Zielpunkten?
Wie kann ich große und kleine Flüsse visuell sinnvoll unterscheiden so dass die grossen Pfeile hervorstechen?
Wie verhindere ich Überlagerungen bei vielen gleichzeitigen Flussdarstellungen?
Wie kann ich Flüchtlingsströme nach Kontinenten aufteilen und jeweils mit einer eigenen Weltkarte visualisieren, gebe mir code Beispiel?
Wie visualisiere ich ausschliesslich Abwanderungsströme aus bestimmten Regionen?
Wie stelle ich Aufnahmeströme pro Kontinent getrennt dar?
Wie kann ich Flüchtlingsbewegungen über mehrere Jahre hinweg animieren?
Wie stelle ich zeitliche Entwicklungen mit animierten Karten dar und exportiese diese als gif?
Wie kann ich Partikel verwenden, um Bewegungen zwischen Ländern zu simulieren?
Wie erstelle ich eine Heatmap der Flüchtlingsaufnahme pro Land?
Wie visualisiere ich Abwanderungsintensitäten auf einer Weltkarte in verschieden starken rot Tönen?
Mache mir ein manuelles mapping dieser Länder zum jeweiligen Kontinent:['Afghanistan', 'Albania', 'Algeria', 'Angola', 'Antigua and Barbuda', 'Argentina', 'Armenia', 'Aruba', 'Australia', 'Austria', 'Azerbaijan', 'Bahrain', 'Bangladesh', 'Barbados', 'Belarus', 'Belgium', 'Belize', 'Benin', 'Bolivia (Plurinational State of)', 'Bosnia and Herzegovina', 'Botswana', 'Brazil', 'Brunei Darussalam', 'Bulgaria', 'Burkina Faso', 'Burundi', 'Cabo Verde', 'Cambodia', 'Cameroon', 'Canada', 'Cayman Islands', 'Central African Rep.', 'Chad', 'Chile', 'China', 'China, Hong Kong SAR', 'China, Macao SAR', 'Colombia', 'Comoros', 'Congo', 'Costa Rica', 'Croatia', 'Cuba', 'Curaçao', 'Cyprus', 'Czech Rep.', "Côte d'Ivoire", 'Dem. Rep. of the Congo', 'Denmark', 'Djibouti', 'Dominican Rep.', 'Ecuador', 'Egypt', 'El Salvador', 'Eritrea', 'Estonia', 'Ethiopia', 'Fiji', 'Finland', 'France', 'Gabon', 'Gambia', 'Georgia', 'Germany', 'Ghana', 'Greece', 'Grenada', 'Guatemala', 'Guinea', 'Guinea-Bissau', 'Guyana', 'Haiti', 'Honduras', 'Hungary', 'Iceland', 'India', 'Indonesia', 'Iran (Islamic Rep. of)', 'Iraq', 'Ireland', 'Israel', 'Italy', 'Jamaica', 'Japan', 'Jordan', 'Kazakhstan', 'Kenya', 'Kuwait', "Lao People's Dem. Rep.", 'Latvia', 'Lebanon', 'Lesotho', 'Liberia', 'Libya', 'Liechtenstein', 'Lithuania', 'Luxembourg', 'Madagascar', 'Malawi', 'Malaysia', 'Mali', 'Malta', 'Mauritania', 'Mauritius', 'Mexico', 'Micronesia (Federated States of)', 'Monaco', 'Mongolia', 'Montenegro', 'Morocco', 'Mozambique', 'Myanmar', 'Namibia', 'Nauru', 'Nepal', 'Netherlands', 'New Zealand', 'Nicaragua', 'Niger', 'Nigeria', 'Norway', 'Oman', 'Pakistan', 'Palau', 'Panama', 'Papua New Guinea', 'Paraguay', 'Peru', 'Philippines', 'Poland', 'Portugal', 'Qatar', 'Rep. of Korea', 'Romania', 'Russian Federation', 'Rwanda', 'Saint Kitts and Nevis', 'Saint Lucia', 'Saint Vincent and the Grenadines', 'Samoa', 'Saudi Arabia', 'Senegal', 'Seychelles', 'Sierra Leone', 'Singapore', 'Sint Maarten (Dutch part)', 'Slovenia', 'Solomon Islands', 'Somalia', 'South Africa', 'South Sudan', 'Spain', 'Sri Lanka', 'Sudan', 'Suriname', 'Swaziland', 'Sweden', 'Switzerland', 'Syrian Arab Rep.', 'Tajikistan', 'Thailand', 'The former Yugoslav Republic of Macedonia', 'Timor-Leste', 'Togo', 'Tonga', 'Trinidad and Tobago', 'Tunisia', 'Turkey', 'Turkmenistan', 'Turks and Caicos Islands', 'Uganda', 'Ukraine', 'United Arab Emirates', 'United Kingdom', 'United Rep. of Tanzania', 'United States of America', 'Uruguay', 'Uzbekistan', 'Vanuatu', 'Venezuela (Bolivarian Republic of)', 'Viet Nam', 'Zambia', 'Zimbabwe']
Wo finde ich einen geeigneten Datensatz welcher mir GDP-per-capita-Daten für alle Länder über mehrere Jahre angibt?
Wie wandle ich Wide-Format-Daten in ein Long-Format für Zeitreihenanalysen um?
Wie gehe ich mit unterschiedlichen Länderkennungen (Name vs. Code) um?
Wie berechne ich einen p-Wert für eine lineare Regression welche imports helfen mir dabei?
Wie führe ich eine Regression getrennt nach Kontinenten durch?


# Rückblick auf das Projekt

Während der Arbeit an diesem Projekt sind wir auf mehrere Herausforderungen gestossen. Eine zentrale Schwierigkeit war, dass der Flüchtlingsdatensatz keine klassischen absoluten Messreihen im statistischen Sinn darstellt. Die Daten beschreiben komplexe, stark verzerrte Strukturen, wodurch viele der in der Vorlesung behandelten statistischen Modelle nur eingeschränkt oder mit zusätzlichen Annahmen anwendbar waren.

Insbesondere war es oft nicht sinnvoll, einfache Kennzahlen wie den arithmetischen Mittelwert direkt zu verwenden, da einzelne Länder oder Jahre extreme Werte aufweisen und die Verteilungen stark schief sind. Dadurch mussten wir Methoden wie Permutationstests, robuste Kennzahlen oder Normalisierungen (zb. pro Bevölkerung) einsetzen, um aussagekräftige Resultate zu erhalten.

Zusätzlich hätten wir uns in gewissen Phasen klarere inhaltliche und methodische Richtlinien gewünscht. Teilweise war unklar, welche Tiefe der Analyse erwartet wird und welche statistischen Verfahren im Kontext der gegebenen Daten als angemessen gelten. Dies führte dazu, dass wir viel Zeit mit Diskussionen und Abwägungen verbracht haben.

Trotz dieser Herausforderungen war das Projekt sehr lehrreich. Wir haben gelernt, mit realen, unvollkommenen Datensätzen zu arbeiten, Annahmen kritisch zu hinterfragen und statistische Methoden nicht nur formal, sondern auch inhaltlich sinnvoll einzusetzen. Insgesamt hat das Projekt unser Verständnis für Statistik, Datenaufbereitung und Interpretation deutlich vertieft.
