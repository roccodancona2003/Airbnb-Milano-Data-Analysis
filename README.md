# 🏠 Airbnb Milano: Analisi Spaziale e Modelli Predittivi di Prezzo

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Data Science](https://img.shields.io/badge/Domain-Data_Science-orange.svg)
![Machine Learning](https://img.shields.io/badge/Machine_Learning-Random_Forest-success.svg)

Questo repository contiene il codice sorgente (R) e il report completo della mia tesina per l'esame di Data Science. L'obiettivo del progetto è analizzare le dinamiche del mercato immobiliare turistico di **Airbnb nella città di Milano** e sviluppare modelli statistici e di Machine Learning per prevedere il prezzo per notte degli alloggi.

## 🎯 Obiettivi del Progetto
1. Esplorare i driver principali (strutturali, geografici e comportamentali) che determinano il prezzo degli Airbnb a Milano.
2. Dimostrare l'esistenza di un mercato "monocentrico" attraverso l'analisi spaziale.
3. Confrontare le performance predittive e la capacità esplicativa di modelli parametrici classici (OLS) e algoritmi non lineari (Tree-based).

## 🛠️ Struttura dell'Analisi e Metodologia

Il progetto segue una pipeline rigorosa di Data Science, articolata nelle seguenti fasi:

### 1. Data Pre-Processing & Feature Engineering
* **Gestione Missing Values:** Imputazione statistica (mediana) per le variabili discrete e regole euristiche per lo status di Superhost.
* **Trasformazioni:** Trasformazione logaritmica del prezzo (Y) per normalizzare la distribuzione e mitigare la forte asimmetria positiva (segmento luxury).
* **Geolocalizzazione:** Sostituzione delle quasi 80 variabili dummy dei quartieri con una singola feature continua (`distanza_centro_km`), calcolata tramite la formula di Haversine a partire dalle coordinate esatte di Piazza del Duomo.

### 2. Modellazione Econometrica (OLS)
* Stima di un modello Log-Lineare con effetti di interazione.
* Gestione della multicollinearità (VIF) e dell'eteroschedasticità (Test di Breusch-Pagan).
* Applicazione degli **Standard Error Robusti di White (Stimatore HC3)** per depurare le stime e ottenere p-value attendibili.

### 3. Riduzione Dimensionale (PCA e PCR)
* Esecuzione dell'**Analisi delle Componenti Principali (PCA)** per risolvere problemi di collinearità tra recensioni e metratura, estraendo tre dimensioni latenti principali:
  1. *Indice di Capacità Strutturale*
  2. *Indice di Popolarità*
  3. *Esclusività Centrale*
* Addestramento di un modello **Principal Component Regression (PCR)** per verificare l'impatto della compressione dei dati sulle previsioni.

### 4. Machine Learning Non-Lineare
* **Regression Tree:** Costruzione di un albero di decisione potato tramite *Cost Complexity Pruning* (Cross-Validation) per individuare le soglie spaziali nette che dividono il mercato.
* **Random Forest:** Addestramento di una foresta di 500 alberi per catturare complesse relazioni non lineari.
* Estrazione della *Feature Importance* e utilizzo dei **Partial Dependence Plots (PDP)** per visualizzare gli effetti marginali non lineari (es. il crollo asintotico dei prezzi allontanandosi dal centro).

## 📈 Risultati Principali
* **Il gradiente spaziale:** Il modello econometrico ha stimato un deprezzamento del **14.7% per ogni chilometro** di lontananza dal Duomo per le case intere. Le stanze condivise, invece, essendo già al limite inferiore di prezzo, risultano immuni a questo deprezzamento.
* **Linearità vs Non-Linearità:** Il modello OLS robusto ha ottenuto una varianza spiegata del 43.3%. Tuttavia, il mercato presenta forti dinamiche a gradoni (non lineari) catturate con successo dalla **Random Forest**, che ha elevato la varianza spiegata (Pseudo-$R^2$ OOB) al **51.7%**.

## 🧰 Stack Tecnologico
* **Linguaggio:** `R`
* **Manipolazione Dati:** `dplyr`, `tidyr`, `readr`, `stringr`
* **Analisi Geospaziale:** `geosphere`
* **Visualizzazione:** `ggplot2`, `GGally`, `patchwork`, `corrplot`
* **Econometria:** `car`, `lmtest`, `sandwich`, `tseries`
* **Machine Learning & PCA:** `factoextra`, `tree`, `randomForest`

## 📁 Contenuto del Repository
* `AIRBNB MILANO TESINA.Rmd`: Il codice sorgente commentato.
* `AIRBNB MILANO TESINA.pdf` / `.html`: Il report finale formattato e pronto per la lettura.
* `listings.csv`: Dataset originale.

---
*Progetto realizzato da Rocco D'Ancona per il corso di Data Science.*
