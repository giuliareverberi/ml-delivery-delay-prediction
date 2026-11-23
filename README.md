#  RomaEats — Delivery Delay Ranking

Modello di Machine Learning per prevedere e ordinare (*ranking*) gli ordini di food delivery a rischio ritardo (>20 minuti) sotto un vincolo operativo fisso.

## Il Problema e la Metrica
* **Obiettivo:** Il Customer Care può chiamare esattamente **400 clienti su 4.000 ordini** (10%) per offrire un voucher preventivo.
* **Metrica:** Con un budget fisso di chiamate e classi sbilanciate (8,7% di ritardi), l'accuracy è fuorviante. Ottimizziamo la **Precision@10%**, valutando la qualità dell'ordinamento nella coda alta tramite `predict_proba`.

## Risultati Principali (5-Fold Stratified CV)

| Step | Precision@10% |
| :--- | :---: |
| Baseline casuale | `0.087` |
| **0.** Logistic Regression (solo numeriche, `hour` lineare) | `0.298 ± 0.004` |
| **1.** `+ zone` (One-Hot) | `0.337 ± 0.006` |
| **2.** `+ hour` come categoria (One-Hot) | `0.419 ± 0.005` |
| **3.** `- items`, `- basket_eur` (**Modello finale**) | `0.415 ± 0.004` |

### Scelte tecniche chiave
* **Preprocessing senza data leakage:** Imputazione mediana (per ~9% di NaN casuali in `prep_time_avg_min`), `StandardScaler` e `OneHotEncoder` incapsulati in una `Pipeline` `scikit-learn`.
* **Rappresentazione non lineare dell'ora:** Codificare `hour` in One-Hot cattura i due picchi di ritardo (pranzo alle 13:00 e cena alle 20:00–21:00).
* **Selezione del modello:** La `LogisticRegression` batte sia i `DecisionTree` (soggetti a overfitting) sia l'`HistGradientBoosting`, garantendo inoltre probabilità ben calibrate.

## Esecuzione
Apri il notebook `design_01_soluzione.ipynb` su **Google Colab** o **Jupyter** ed esegui tutte le celle per riprodurre l'analisi, visualizzare i grafici e generare il file `predictions.csv` per i 4.000 nuovi ordini.
