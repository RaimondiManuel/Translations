# Git Pro Book #

### 1.1 Getting Started - About Version Control ###

In questo capitolo, introdurremo Git, cominceremo illustrando il background dietro gli strumenti di versionamento, quindi ci sposteremo successivamente sulla procedura di avvio di Git nel vostro sistema, ed infine, come impostare Git per le sessioni di lavoro future.

### About Version Control ###

Che cos'è un VCS e perche dovreste preoccuparvene? Un VCS, Version Control System e un sitema di controllo di versione, creato allo scopo di tenere traccia dei cambiamenti su uno o più file, in modo tale da poter richiamare una versione specifica di questi in un secondo momento.

Se sei un grafico o un web designer, potresti voler tenere traccia di tutte le versioni di un immagine, oppure di un layout. In questo caso un VCS è la cosa più saggia da utilizzare. Un VCS ti consente di ripristinare lo stato uno o più file, che hai selezionato, ad una loro versione precedente, oppure, riportare l'intero progetto al suo stato iniziale, oppure, fare una comparazione dei cambiamenti avvenuti in corso d'opera. è possibile anche vedere chi ha effettuato l'ultima modifica. L'introduzione di un VCS nel proprio work flow, comporta anche tenere al sicuro il proprio progetto da un'eventuale corruzione dei file, poichè ne rende possibile il recupero.

### Local Version Control System ###

Molte persone utilizzano come metodo di controllo di versione, quello di copiare tutto il progetto in un'altra cartella. Questo approccio è molto comune, poichè di semplice da eseguire, tuttavia, è un'approccio incline ad errori. è facile dimenticare la directory in cui ci si trova al momento, e quindi scrivere sul file sbagliato, oppure, copiare un file errato senza che se ne avesse l'intenzione.

I VCS sono stati realizzati proprio allo scopo di risolvere questa problematica. I primi VCS erano locali alla macchina, con un database anchesso locale, il cui scopo, era quello di conservare le modifiche effettuate sotto VCS.

Uno degli strumenti VCS più popolari era RCS, che viene ancora oggi, distribuito su molti computer. RCS funzionava mantenendo un set di patch, una raccolta di differenze tra file, in un formato apposito su disco. Poteva quindi ricreare l'aspetto di un qualsiasi file in qualsiasi momento, tramite l'aggiunta di tutte le patch.

### Centralized Version Control System ###

Il problema principale che le persone si trovano ad affrontare, è il bisogno di dover condividere il lavoro con altri sviluppatori, i quali lavorano su sistemi diversi. Per far fronte a questo problema, sono stati sviluppati VCS centralizzati, chiamati CVCS, Centralized Version Control System. Questi sistemi, come CVS, SVN, Preforce, sono basati su un singolo server, il quale è proprietario di tutti i file, nonche, un certo numero di client che gestiscono i file basandosi su quella posizione centrale. Per molti anni, questo è stato lo standardper i VCS.

Questo setup offre numerosi vantaggi, in particolare rispetto ai VCS locali. Ad desempio, in una certa misura, tutti sanno cio che fanno tutti all'interno del progetto. Gli amministratori hanno un controllo preciso su chi può fare cosa, ed è nolto più facile amministrare un CVCS che gestire un database locale per n client. Tuttavia, questo setup ha anche dei difetti. Uno dei più ovvi è il single point of failure che rappresnta un server centralizzato. Se quel server si interrompe per un'ora, nessuno può collaborare o salvare le modifiche effettuate. Se il progetto sul server centrale è danneggiato o corrotto, si perde ogni progresso fatto. Anche i server VCS locali soffrono di questo stesso problema. Ogni volta che la cronologia dei cambiamenti viene gestita in un singolo punto, è inesorabilmente presente, questo tipo di problematica. 

### Distributed Version Control System ###

è qui che entrano in gioco i DCVS, Distributed Control Version System. In un DVCS i client non controllano solamente l'ultimo snapshot del file. I client hanno il controllo sull'intero repository, inclusa tutta la sua cronologia. Pertanto, se il server viene compromesso in qualche modo, e questi client lavorano basandosi su questo server, ognuno dei client avrà a disposizione una versione sana del repository, con cui poter ripristinare lo stato del server. Pertanto ogni client è un vero e proprio backup di ciò che è contenuto nel server.

Inoltre i DCVS si comportano molto bene nel gestire diversi repository remoti, in modo tale da permettere a diversi gruppi con diversi work flow di poter lavorare sullo stesso progetto contemporaneamente. Ciò consente di impostare diversi work flow, cosa impossibile nei CVCS.

### 1.2 Getting Started - A Short History of Git ###

Come con molte grandi cose nella vita, Git ha iniziato con un po' di distruzione creativa, e di accese polemiche.

Il kernel linux è un progetto software open source di ambito abbastanza grande. Per la maggior parte della durata della manutenzione del kernel linux ( 1991 - 2002 ), le modifiche al software sono state passate come patch e file archiviati. Nel 2002, il progetto del kernel linux iniziò ad utilizzare un DVCS proprietario chiato BitKeeper.

Nel 2005 la relazione tra la comunità che ha sviluppato il kernel linux e la socità commerciale che ha sviluppato BitKepper si è rotta, e lo stato di libero utilizzo dello strumento è stato revocato. Ciò ha spinto la comunità di sviluppo ( e in particolare Linus Torvalds, il creatore di linux ) a sviluppare il proprio strumentobasato su alcune delle lezioni apprese durante l'utilizzo di BitKeeper. Alcuni degli obbiettivi del nuovo sistema erano

1. Velocità.
2. Design semplice.
3. Forte supporto per lo sviluppo non lineare ( migliaia di branch paralleli ).
4. Completamente distribuito.
5. In grado di gestire in modo efficente grandi progetti come il Kernel Linux ( velocità e gestione dei dati ).

Dalla sua neìascita nel 2005, Git si è evoluto ed è maturato per essere facile da usare e tuttavia mantenere queste qualità iniziali.

è incredibilmente veloce, è molto efficente con progetti di grandi dimensioni e ha un incredibile sistema di braching per lo sviluppo non lineare. 

### 1.3 Getting Started - Git Basics ###