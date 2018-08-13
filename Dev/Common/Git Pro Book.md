# Git Pro Book #

In questo capitolo, introdurremo Git, cominceremo illustrando il background dietro gli strumenti di versionamento, quindi ci sposteremo successivamente sulla procedura di avvio di Git nel vostro sistema, ed infine, come impostare Git per le sessioni di lavoro future.

## About Version Control ##

Che cos'è un VCS e perche dovreste preoccuparvene? Un VCS, Version Control System e un sitema di controllo di versione, creato allo scopo di tenere traccia dei cambiamenti su uno o più file, in modo tale da poter richiamare una versione specifica di questi in un secondo momento.

Se sei un grafico o un web designer, potresti voler tenere traccia di tutte le versioni di un immagine, oppure di un layout. In questo caso un VCS è la cosa più saggia da utilizzare. Un VCS ti consente di ripristinare lo stato uno o più file, che hai selezionato, ad una loro versione precedente, oppure, riportare l'intero progetto al suo stato iniziale, oppure, fare una comparazione dei cambiamenti avvenuti in corso d'opera. è possibile anche vedere chi ha effettuato l'ultima modifica. L'introduzione di un VCS nel proprio work flow, comporta anche tenere al sicuro il proprio progetto da un'eventuale corruzione dei file, poichè ne rende possibile il recupero.

## Local Version Control System ##

Molte persone utilizzano come metodo di controllo di versione, quello di copiare tutto il progetto in un'altra cartella. Questo approccio è molto comune, poichè di semplice da eseguire, tuttavia, è un'approccio incline ad errori. è facile dimenticare la directory in cui ci si trova al momento, e quindi scrivere sul file sbagliato, oppure, copiare un file errato senza che se ne avesse l'intenzione.

I VCS sono stati realizzati proprio allo scopo di risolvere questa problematica. I primi VCS erano locali alla macchina, con un database anchesso locale, il cui scopo, era quello di conservare le modifiche effettuate sotto VCS.

Uno degli strumenti VCS più popolari era RCS, che viene ancora oggi, distribuito su molti computer. RCS funzionava mantenendo un set di patch, una raccolta di differenze tra file, in un formato apposito su disco. Poteva quindi ricreare l'aspetto di un qualsiasi file in qualsiasi momento, tramite l'aggiunta di tutte le patch.

## Centralized Version Control System ##

