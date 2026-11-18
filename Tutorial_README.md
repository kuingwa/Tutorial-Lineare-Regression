# Tutorial: Lineare Regression mit Python (20 Min.)

**Ziel:** Du passt eine lineare Regression an echte Daten an, liest die Ausgabe und prüfst, ob man dem Modell trauen kann. Am Ende findest du drei Fehler in einem kaputten Notebook.
Daten: Boston Housing (506 Zählbezirke), der Datensatz aus Lab 3.6 in *An Introduction to Statistical Learning*. Er liegt bei, ein Download ist nicht nötig.

## Dateien
| Datei | Zweck |
|---|---|
| `Tutorial_Lineare_Regression.ipynb` | Das Notebook, in dem ihr arbeitet (Aufgaben 1, 3 und 4 haben je eine Lücke) |
| `Tutorial_Lineare_Regression_solved.ipynb` | Dasselbe Notebook, ausgefüllt und ausgeführt |
| `Fehlerhaftes_Notebook.ipynb` | Läuft ohne Fehlermeldung, enthält aber **drei Fehler** (Aufgabe 5) |
| `Boston.csv`, `Boston_SOURCE.txt` | Daten und ihre Herkunft |
| `environment.yml`, `requirements.txt` | Software-Umgebung (feste Versionen) |
| `LOESUNGEN.md` | Antworten: erst nach dem Versuch ansehen |

## Vor der Sitzung (5 Min., zu Hause)
1. **Dateien holen.** Entpackt den Tutorial-Ordner an einen Ort ohne Leerzeichen und Sonderzeichen im Pfad, z. B. `C:\tutorial` oder `~/tutorial`.
2. **Miniforge installieren** (github.com/conda-forge/miniforge). Miniconda geht auch.
3. **Terminal öffnen:** unter Windows die *Miniforge Prompt*, unter macOS oder Linux ein beliebiges Terminal. In den Ordner wechseln:
```
cd pfad/zum/tutorial
```
4. **Umgebung anlegen** (einmalig, dauert einige Minuten):
```
conda env create -f environment.yml
```
5. **Aktivieren:**
```
conda activate linreg
```
**Checkpoint:** Die Eingabezeile beginnt jetzt mit `(linreg)`.
6. **Python prüfen:**
```
python --version
```
**Erwartet:** `Python 3.13.x`.
7. **JupyterLab starten:**
```
jupyter lab
```
**Checkpoint:** Der Browser öffnet JupyterLab, links stehen die Dateien dieses Ordners. (Ohne conda: `pip install -r requirements.txt` mit Python 3.13, dann `jupyter lab`.)

## Zeitplan
| Min. | Teil |
|---|---|
| 0–2 | Schritt 0: Prüfen |
| 2–8 | Teil A: Aufgaben 1–2 |
| 8–15 | Teil B: Aufgaben 3–5 |
| 15–19 | Abschlussquiz |
| 19–20 | Abschluss |

Arbeitet zu zweit: eine Person tippt, die andere liest den Checkpoint vor; nach Teil A wird gewechselt. **Kernaufgaben: 1, 2, 4.** Aufgaben 3 und 5 sind Zusatzaufgaben und dürfen bei Zeitnot entfallen. Meldet euch, wenn ihr länger als eine Minute feststeckt.

## Schritt 0: Prüfen (2 Min.)
Doppelklick auf `Tutorial_Lineare_Regression.ipynb` im linken Fenster. Fragt JupyterLab nach einem Kernel, wählt *Python 3 (ipykernel)*. Klickt in die erste Code-Zelle und drückt **Umschalt + Enter**.
**Erwartet:** Die Versionen von numpy, pandas, statsmodels und scikit-learn werden ausgegeben, danach `(506, 13)`. Links neben der Zelle erscheint eine Zahl in Klammern, z. B. `[1]`.

## Teil A: Einfache und multiple Regression
**Aufgabe 1: Einfache Regression anpassen und lesen**
Führt die Zellen von Teil 1 aus (`medv ~ lstat`). Passt danach in der Lücke `medv ~ rm` an.
**Erwartet:** Bei `lstat`: Achsenabschnitt 34,55, Steigung −0,95, R² 0,544 und ein Streudiagramm mit Gerade. Was bedeutet die Steigung −0,95 in Dollar? Welcher der beiden Prädiktoren erklärt mehr Varianz?

**Aufgabe 2 (Kern): Intervalle und ein zweiter Prädiktor**
Führt die Zellen von Teil 2 aus.
**Erwartet:** Bei `lstat = 10` liegt der mittlere Hauswert bei 25,05 mit KI (24,47; 25,63), das Prognoseintervall ist (12,83; 37,28). Warum ist das zweite Intervall so viel breiter? Mit `age` ändert sich der Koeffizient von `lstat`: um wie viel, und warum kann das passieren?

## Teil B: Ist das Modell gut?
**Aufgabe 3 (Zusatz): Alle Prädiktoren und Kollinearität**
Füllt die Lücke: `medv` auf alle 12 übrigen Spalten anpassen und den VIF jeder Spalte berechnen.
**Erwartet:** R² nahe 0,73. Welche Prädiktoren sind nicht signifikant (p > 0,05)? Welche zwei haben den höchsten VIF?

**Aufgabe 4 (Kern): Residuen und ein quadratischer Term**
Führt den Residuenplot aus, ergänzt dann `I(lstat**2)` und vergleicht beide Modelle mit `anova_lm`.
**Erwartet:** Der erste Plot zeigt eine Kurve statt Rauschen. Mit dem quadratischen Term ist R² etwa 0,64 und F etwa 135. Wird die Anpassung besser, und was sagt das über die Linearität?

**Aufgabe 5 (Zusatz): Fehlersuche**
Öffnet `Fehlerhaftes_Notebook.ipynb` und führt es aus. Alle Zellen laufen, aber drei Ergebnisse sind falsch. Vergleicht sie mit den Zahlen aus Aufgabe 1 und 2, findet die Ursachen und behebt sie.

## Geschafft? (Checkliste)
- [ ] Schritt 0 hat die Versionen und `(506, 13)` ausgegeben
- [ ] Steigung, R² und Intervalle für `medv ~ lstat` gelesen
- [ ] Die Kurve im Residuenplot und die Verbesserung mit `lstat²` gesehen
- [ ] Ihr könnt erklären, warum das Prognoseintervall breiter ist

## Abschlussquiz (3 Min.)
1. Was minimieren die kleinsten Quadrate?
2. R² = 0,544 bei `medv ~ lstat`. Was bedeutet das?
3. Ein Residuenplot zeigt eine deutliche Kurve. Welche Annahme ist verletzt, und was kann man tun?
4. Welches Intervall ist breiter, Konfidenz- oder Prognoseintervall, und warum?

Antworten: Ende von `LOESUNGEN.md`.

## Häufige Fehler und schnelle Lösungen
| Meldung / Symptom | Lösung |
|---|---|
| `FileNotFoundError: Boston.csv` | JupyterLab in diesem Ordner starten; Notebook und `Boston.csv` müssen zusammenliegen. |
| `conda activate` funktioniert nicht | Unter Windows die **Miniforge Prompt** benutzen. |
| `jupyter` nicht gefunden | Zuerst `conda activate linreg` ausführen. |
| `ModuleNotFoundError` | Die Umgebung ist nicht aktiv: `conda activate linreg`, dann JupyterLab neu starten. |
| `PatsyError` in einer Formel | `I(lstat**2)` schreiben, nicht `lstat^2`. |
| Kernel tot oder seltsame Ergebnisse | Menü *Kernel → Restart Kernel and Run All Cells*. |
| Zahlen weichen in der letzten Stelle ab | Andere Bibliotheksversionen: mit den Versionen aus Schritt 0 vergleichen. |

In den Notebooks kommen keine Zufallszahlen vor; `SEED = 42` ist trotzdem gesetzt, damit spätere Erweiterungen reproduzierbar bleiben.

## Abschluss (1 Min.)
Eine Regression ist schnell gerechnet und schnell falsch gelesen. Schaut immer auf die Residuen und sagt dazu, welche Annahme ihr geprüft habt.

## Quellen und Hilfsmittel
James et al., *An Introduction to Statistical Learning*, Kap. 2.1, 3.1, 3.6: https://www.statlearning.com/  
ISLP-Python-Lab: https://phonchi.github.io/SLDM_Book/Chapter_3_Lab.html  
GeeksforGeeks, Linear Regression: https://www.geeksforgeeks.org/machine-learning/ml-linear-regression/  
StatQuest-Video: https://www.youtube.com/watch?v=7ArmBVF2dCs  
Hilfsmittel: Claude (Anthropic) wurde für Textentwürfe und Code-Hilfe genutzt. Das Team hat die Inhalte geprüft, die Notebooks ausgeführt und verantwortet das Ergebnis.
