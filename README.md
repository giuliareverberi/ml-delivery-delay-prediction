#  RomaEats — Delivery Delay Ranking

Modello di Machine Learning per prevedere e ordinare (*ranking*) gli ordini di food delivery a rischio ritardo (>20 minuti) sotto un vincolo operativo fisso.

## Il Problema e la Metrica
* **Obiettivo:** Il Customer Care può chiamare esattamente **400 clienti su 4.000 ordini** (10%) per offrire un voucher preventivo.
* **Metrica:** Con un budget fisso di chiamate e classi sbilanciate (8,7% di ritardi), l'accuracy è fuorviante. Ottimizziamo la **Precision@10%**, valutando la qualità dell'ordinamento nella coda alta tramite `predict_proba`.



## Esecuzione
Apri il notebook `design_01_soluzione.ipynb` su **Google Colab** o **Jupyter** ed esegui tutte le celle per riprodurre l'analisi, visualizzare i grafici e generare il file `predictions.csv` per i 4.000 nuovi ordini.
