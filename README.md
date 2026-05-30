# Analiza czasu trwania - projekt ACT

Repozytorium zawiera materiały do projektu z analizy czasu trwania na danych `heart_failure_clinical_records_dataset.csv`.

## Zawartość

- `Data/` - dane wejściowe używane w notebookach.
- `01_modele_nieparametryczne_official.ipynb` - analiza nieparametryczna: cenzurowanie, Kaplan-Meier, Nelson-Aalen, podgrupy i testy.
- `02_modele_parametryczne_i_bayes_official.ipynb` - modele parametryczne AFT oraz rozszerzenie bayesowskie.
- `03_model_coxa_i_diagnostyka_official.ipynb` - model Coxa, diagnostyka PH, reszty Schoenfelda, obserwacje wpływowe i interakcja czasowa.
- `Tables/` - tabele wynikowe użyte w prezentacji.
- `Wykresy/` - wykresy użyte w prezentacji.
- `latex/main.tex` oraz `latex/main.pdf` - źródło i gotowa prezentacja Beamer.
- `run_summary_v1.json` - krótkie podsumowanie liczby obserwacji, zdarzeń i slajdów.

## Uruchomienie

Notebooki zakładają uruchomienie z katalogu głównego repozytorium. Dane są czytane ze ścieżki `Data/heart_failure_clinical_records_dataset.csv`.

Aby odtworzyć środowisko Pythona:

```bash
pip install -r requirements.txt
```

Prezentacja PDF znajduje się w `latex/main.pdf`. Źródło `latex/main.tex` korzysta z relatywnych ścieżek do `Tables/` i `Wykresy/`.
