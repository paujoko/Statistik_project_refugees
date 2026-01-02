Forschungsfrage / Hypothese

Hypothese H1:
Früher (2006–2010) sind global mehr Menschen geflüchtet als später (2011–2016).

Nullhypothese H0:
Es gibt keinen Unterschied zwischen den Perioden.

⸻

Datengrundlage: Globale jährliche Flüchtlingszahlen

Die Jahreszahlen stammen aus der Aggregation über alle Herkunftsländer.

Frühe Jahre (2006–2010):

2006: 10,618,994
2007: 12,312,040
2008: 11,314,855
2009: 11,385,707
2010: 11,387,126

Mittelwert früh: 11,803,744

Spätere Jahre (2011–2016):

2011: 11,301,825
2012: 11,440,754
2013: 12,863,728
2014: 16,189,781
2015: 19,336,251
2016: 19,900,103

Mittelwert spät: 15,172,407

⸻

Ergebnis 1: Permutationstest

Fragestellung: Sind frühere Jahre > spätere Jahre?

Beobachtete Differenz (früh – spät):

T_obs = -3,804,329

Die mittleren Flüchtlingszahlen sind später deutlich höher.

Permutationstest (5.000 Permutationen):

p-Wert (zweiseitig) = 0.0758

Interpretation:
	•	Auf 5%-Niveau nicht signifikant.
	•	Auf 10%-Niveau schwach signifikant.
	•	Der Unterschied geht klar in Richtung: spätere Jahre haben höhere Werte.

Die ursprüngliche Hypothese wird eher widerlegt.

⸻

Ergebnis 2: Effektgröße (Cohen’s d)

Cohen’s d = 1.31

Interpretation:
	•	d > 0.8: großer Effekt
	•	d > 1.2: sehr großer Effekt

Der Unterschied zwischen frühen und späten Jahren ist praktisch stark ausgeprägt, unabhängig von Signifikanztests.

⸻

Ergebnis 3: Chi-Quadrat-Test (hohe vs. niedrige Flüchtlingsjahre)

Schwelle (Median):

11,440,754

Einteilung der Jahre in high und low:

Früh: High = 1, Low = 4
Spät: High = 5, Low = 1

Kontingenztabelle:
            High    Low

Early         1     4
Late          5     1

Ergebnis:

Chi² = 2.227
p = 0.1355

Interpretation:

Kein signifikanter Zusammenhang zwischen Zeitraum und Häufigkeit hoher Werte.
Trend aber sichtbar: späte Jahre haben häufiger hohe Flüchtlingszahlen.

⸻

Ergebnis 4: Risk Ratio und Odds Ratio

Risk early = 0.2
Risk late = 0.833
Risk Ratio = 0.24

Odds early = 0.25
Odds late = 5
Odds Ratio = 0.05

Interpretation:
	•	Ein spätes Jahr ist über viermal so wahrscheinlich ein Hoch-Flüchtlingsjahr zu sein wie ein frühes Jahr.
	•	Die Odds sind sogar etwa zwanzigmal höher.

Dies bestätigt erneut: spätere Jahre weisen deutlich höhere Flüchtlingszahlen auf.

⸻

Gesamtfazit

Alle statistischen Methoden führen zum gleichen Ergebnis:
	•	Der Mittelwert der späteren Jahre ist deutlich höher.
	•	Die Effektgröße ist sehr groß (d = 1.31).
	•	Der Permutationstest zeigt einen grenzwertigen Hinweis auf eine echte Differenz.
	•	Risk Ratio und Odds Ratio zeigen einen starken Trend zugunsten späterer Jahre.

Ergebnis:
Die Hypothese „Früher sind mehr Menschen geflüchtet als heute“ wird klar widerlegt.

⸻

Projektstruktur

refugee_vl8_analysis.ipynb – vollständige Analyse
refugees_by_origin_per_year.csv – Datengrundlage
README.md – Dokumentation