# Lösungen

Aufgabe 1: `medv ~ lstat`: b0 = 34,554, b1 = −0,950, SE(b1) = 0,039, R² = 0,544, RSE = 6,216. scikit-learn liefert dieselbe Gerade (Trainings-MSE 38,48). `medv ~ rm`: Achsenabschnitt −34,671, Steigung 9,102, R² 0,484, `lstat` erklärt also mehr Varianz. Steigung −0,95 heißt: 1 Prozentpunkt mehr Bevölkerung mit niedrigem Status geht mit rund 950 $ weniger Medianwert einher.

Aufgabe 2: bei `lstat = 10`: ŷ = 25,05, KI (24,47; 25,63), PI (12,83; 37,28). Das PI enthält zusätzlich den Fehler ε eines einzelnen Bezirks. Mit `age`: lstat −1,032 (vorher −0,950), age 0,0345 (p = 0,005), R² 0,551. Die Änderung ist klein, weil `lstat` und `age` korreliert sind.

Aufgabe 3: R² 0,734, adjustiert 0,728, RSE 4,80, F 113,5. Nicht signifikant: indus (p = 0,83) und age (p = 0,79). Höchster VIF: tax 9,0 und rad 7,5 (beide über 5).

Aufgabe 4: Die Residuen zeigen eine Kurve. Mit `lstat²`: R² 0,641, F = 135,2, p < 0,001. Die Gerade ist zu einfach, der Zusammenhang ist gekrümmt.

## Hinweise zu Aufgabe 5
- Fehler 1: `sm.OLS(y, X)` ohne `sm.add_constant`, also kein Achsenabschnitt: Steigung 1,12 und R² 0,449 statt −0,95 und 0,544. Korrektur: Konstante ergänzen oder die Formelschnittstelle nutzen.
- Fehler 2: Der RSE teilt durch n statt durch n − 2 (6,20 statt 6,22). Korrektur: `np.sqrt(ssr / (n - 2))` oder `np.sqrt(fit.scale)`.
- Fehler 3: Das „Prognoseintervall“ nutzt `mean_ci_*`, das ist das Konfidenzintervall des Mittelwerts. Korrektur: `obs_ci_lower` und `obs_ci_upper` verwenden: (12,83; 37,28).

## Abschlussquiz: Antworten
1. Sie minimieren die Residuenquadratsumme RSS = Σ(yᵢ − ŷᵢ)².
2. Das Modell erklärt rund 54 % der Varianz von medv; 46 % bleiben unerklärt.
3. Die Linearität ist verletzt. Polynomterme wie lstat², eine Transformation oder ein anderes Modell probieren.
4. Das Prognoseintervall, denn es enthält zusätzlich den nicht reduzierbaren Fehler ε eines neuen Bezirks.
