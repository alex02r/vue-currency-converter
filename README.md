# Vue Currency Converter

Stiamo organizzando dei viaggi all’estero e ci farebbe tanto comodo un convertitore di valute molto veloce da usare all’occorrenza.

In una versione di base, abbiamo due input numerici e due select. L’utente può scrivere in entrambi gli input e convertire nelle valute impostate nelle select.
Le valute presenti come options nelle select sono prese dall’API Frankfurter, gratuita e utilizzabile senza API key. Ogni cambiamento in uno degli input chiama l’endpoint relativo alla conversione tra valute.

Per una versione più avanzata possiamo:

- disabilitare currency nella select in relazione all’altra selezionata (evitare conversione su due currency uguali)
- aggiungere un’intestazione sfruttando la classe Intl di JS per la formattazione delle currency

Se neanche la versione avanzata ci basta, possiamo aggiungere un grafico con Apex Charts (o chart.js o vue-chart-js), da customizzare a piacere.

La grafica nell’anteprima è di esempio, potete realizzarla come preferite.