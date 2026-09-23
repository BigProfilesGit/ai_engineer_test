Autore: Data Science Team\
Data: 15 Gennaio 2025\
Status: CONFIDENTIAL / INTERNAL USE ONLY\

1. DATASET & OBIETTIVO\
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\
Il modello prevede la probabilità che un cliente acquisti un prodotto.\
Target: \'acquisto_effettuato\' (1 = ha comprato, 0 = non ha comprato).\
\
NOTA IMPORTANTE SUL CONVERSION RATE:\
Il dataset è fortemente sbilanciato. Il tasso di conversione (classe positiva) osservato nel training set è del 10%.


2. FEATURE ENGINEERING & PREPROCESSING\
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\
Prima del training, i dati grezzi sono stati trasformati come segue.\
Questa pipeline DEVE essere replicata in inferenza.\
\
A. Feature \'nome\' (stringa)\
- Azione: Rimosso (Drop).\
- Motivo: Alta cardinalità, rischio overfitting.\
\
B. Feature \'eta\' (numerica)\
- Azione: Nessuna trasformazione (Pass-through).\
- Motivo: Il modello gestisce nativamente i valori numerici.\
\
C. Feature \'cliente_attivo\' (stringa)\
- Valori raw: \'SI\', \'NO\', null.\
- Azione: Binarizzazione custom.\
- Logica:\
Se valore == \"SI\" -\> Mappa a 1.\
Altrimenti (incluso \"NO\", null o altri) -\> Mappa a 0.
