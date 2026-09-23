**TEST TECNICO AI ENGINEER**

# Introduzione

Il candidato dovrà realizzare una API ad alte performance per la messa in produzione di un modello predittivo.

Il modello (classificazione propensione all\'acquisto) è stato sviluppato dal team di Data Science.

Il compito è quello creare un\'architettura API robusta che possa gestire alti volumi di richieste e salvare lo storico delle predizioni.

## Materiale fornito

Insieme a questo documento viene fornito:

- Model.pkl: il classificatore RandomForestClassifier in formato pickle (fatto tramite Scikit-Learn)
- Allegato A (Training Report): Documento tecnico contenente le logiche di preprocessing e business fondamentali.
- Requirements.txt: Dipendenze di base

# Specifiche

Deve essere creata una API scritta in FastAPI containerizzata che esponga un endpoint

> **POST /predict**

E' necessario andare a replicare le logiche descritte nell'Allegato A per poter effettuare le prediction in modo corretto.

Questo endpoint verrà utilizzato sia per le chiamate singole, sia per le chiamate Batch (al massimo 1000 record in una singola chiamata).

Il sistema deve essere orchestrato tramite Docker Compose e includere un database MongoDB.

## INPUT

E' un endpoint in modalità POST che prende in input il seguente formato di dati (in formato JSON), per un processamento singolo e a batch (fino a 1000 record in una sola chiamata):

caso singolo:
``` JSON
{
    "nome": "Mario",
    "eta": 30,
    "cliente_attivo": "SI"
}
```

caso batch:

``` JSON
[
    {
        "nome": "A",
        "eta": 20,
        "cliente_attivo": "NO"
    },
    {
        "nome": "B",
        "eta": 50,
        "cliente_attivo": "SI"
    }
] 
```

## OUTPUT

In output ci si aspetta un JSON (per il caso singolo) o una lista di JSON (per il caso batch) con il seguente formato

Caso singolo:
``` JSON
{
    "probability": 0.2134,
    "label": "OK"
}
```


Caso batch:
``` JSON
[
    {
        "probability": 0.2134,
        "label": "OK"
    },
    {
        "probability": 0.0134,
        "label": "NO_ACQUISTO"
    }
]
```

I possibili valori della "label" sono OK e NO_ACQUISTO

## DATABASE

Ogni richiesta deve essere salvata su un database MongoDB. La persistenza dei documenti deve essere ottimizzata nel caso di chiamate single o batch. Si lascia al candidato la scelta della migliore struttura da utilizzare.

Sul database dovranno essere salvate le seguenti informazioni:

- timestamp: data della predizione
- input_data: Dati di input della richiesta di predizione
- output_data: Dati di output della richiesta

È possibile andare ad utilizzare la forma che più si ritiene opportuna, basta che siano presenti le informazioni precedentemente illustrate.

## DOCKER

Il candidato dovrà fornire un Dockerfile compose che permetta di eseguire l'applicazione sviluppata.

Il compose deve contenere:

- Il servizio API
- Il database MongoDB
- Comunicazione di rete affinché i servizi comunichino e il servizio API sia esposto sulla porta 5000


# Operatività

## Requisiti

- Deve essere usato Python 3.11+
- Usare un framework a scelta tra FastAPI
- Il salvataggio dei dati deve essere fatto su MongoDB
- Il servizio dovrà esporre la porta operativa 5000

# Consegna

La consegna deve avvenire al più una settimana dopo dalla consegna del test. Deve essere creata un repository Github con tutto il codice prodotto e fornito una **documentazione** in cui vengono mostrate le scelte effettuate implementative e i comandi per lanciare l'applicativo stesso.

# Valutazione

Il test verrà valutato secondo i seguenti criteri:

- Correttezza del codice generato
- Qualità del codice stesso (organizzazione, commenti, test, ecc)
- Performance generali
- Correttezza delle assunzioni riguardanti la pipeline di ML 
(preprocessing dei dati, prediction, caricamento del modello, ...)
