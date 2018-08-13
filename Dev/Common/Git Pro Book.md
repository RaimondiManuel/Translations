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

Nel 2005 la relazione tra la comunità che ha sviluppato il kernel linux e la socità commerciale che ha sviluppato BitKepper si è rotta, e lo stato di libero utilizzo dello strumento è stato revocato. Ciò ha spinto la comunità di sviluppo (e in particolare Linus Torvalds, il creatore di linux) a sviluppare il proprio strumentobasato su alcune delle lezioni apprese durante l'utilizzo di BitKeeper. Alcuni degli obbiettivi del nuovo sistema erano

1. Velocità.
2. Design semplice.
3. Forte supporto per lo sviluppo non lineare (migliaia di branch paralleli).
4. Completamente distribuito.
5. In grado di gestire in modo efficente grandi progetti come il Kernel Linux (velocità e gestione dei dati).

Dalla sua neìascita nel 2005, Git si è evoluto ed è maturato per essere facile da usare e tuttavia mantenere queste qualità iniziali.

è incredibilmente veloce, è molto efficente con progetti di grandi dimensioni e ha un incredibile sistema di braching per lo sviluppo non lineare. 

### 1.3 Getting Started - Git Basics ###

Quindi, cos'è in poche parole Git? questa è una sezione importante da assimilare perchè se capisci cos'è Git el le basi del funzionamento sarà possibile utilizzare Git in modo efficace e probabilmente molto più facile. Mentre apprendi Git è necessario dimenticare gli altri sistemi di versioning. In questo modo eviterai confusione durante l'utilizzo dello strumento. Anche se l'interfaccia Git è molto simile agli altri strumenti in commercio , Git memorizza e pensa alle informazioni in modo molto diverso, e la comprensione di queste differenze ti aiuterà ad evitare confonderti durante l'utilizzo.

## Snapshot, Not Differences ##

La principale differenza tra Git e qualsiasi altro VCS( Subversion ecc... ) è il modo in cui Git pensa ai suoi dati. Concettualmente la maggior parte dei sistemi memorizza le informazioni come un elenco di modifiche basato su file. Questi altri sistemi(CVS, Subversion, Preforce, Bazaar e cosi via) pensano alle informazioni che memorizzano come un insieme di file e modifiche apportate a ciascun file nel tempo(questo è comunemente descritto come VCS delta based).

Git non pensa o conserva i suoi dati in questo modo. Invece Git pensa ai suoi dati più come ad una serie di snapshot di un filesystem in miniatura. Con Git, ogni volta che si esegue un commit o si salva lo stato del proprio progetto, Git fa sostanzialmente uno snapshot di come appaiono i tutti file in quel momento e memorizza un riferimento a quello snapshot. Per essere efficente, se i file non sono stati modificati, Git non memorizza nuovamente i file, ma solo un collegamento al file precedente. Git pensa ai sui dati più come un flusso di snapshot.

Questa è una distinzione importante tra Git e quasi tutti gli altri VCS. Ciò ha causato a Git di dover riconsiderare quasi ogni aspetto del controllo di versione che la maggior parte degli altri sistemi hanno copiato dalla generazione precedente. Questo rende Git più simile ad un mini filesystem con alcuni incredibili strumenti costruiti attorno ad esso, piuttosto che un semplice VCS. Esploreremo alcuni dei vantaggi cheottieni pensando ai tuoi dati in questa maniera, quando parleremo di branching.

## Nearly Every Operation is Local ##

La maggior parte delle operazioni in Git necessitano solo di file o risorse locali per funzionare, in genere non sono necessarie informazioni da un altro computer per funzionare. Se sei abituato ad un CVCS in cui la maggior parte delle operazioni ha una tale latenza di rete, ciò torna molto utile, poichè hai a disposizione l'intera cronologia del progetto sul tuo disco locale, la maggior parte delle operazioni sembrano quasi istantanee. Ad esempio, per esplorare la cronologia del progetto, Git non ha bisogno di uscire sul server per mostrarla, semplicemente, legge dal tuo database locale.

Ciò significa anche che ci sono poche cose che non si possono fare se non si è online o fuori VPN.

## Git Has Integrity ##

Tutto in Git viene verificato prima del commit, verifica definita in un checksum. Ciò significa che è impossibile effettuare un cambiamento di contenuto di un file o di una directory senza che Git ne sia a conoscenza. Questa feature è integrata in Git a basso livello ed è parte integrante della sua filosofia. Non è possibile perdere le informazioni in transito e ottenere la corruzione dei file senza che Git se ne accorga.

Il meccanismo che Git usa per il checksum è chiamato SHA-1. Questa è una stringa di 40 caratteri esadecimali (0-9 e a-f) e calcolata in base al contenuto di un file e dalla struttura delle directory nel progetto Git. Un hash SHA-1 ha un aspetto simile:

24b9da6552252987aa493b52f8696cd6d3600373

Bedrai questi valori hash ovunque in Git, infatti, Git memorizza tutto nel suo database. Non per nome del file ma per valore di hash. Git in genere aggiunge solo dati.

Quando esegui azioni in Git, quasi tutte aggiungono dati. è difficile far compiere a Git un'azione non annullabile o cancellare dati in qualsiasi modo. Come con qualsiasi VCS, puoi perdere o rovinare le modifiche che non hai ancora eseguito, ma dopo aver effettuato uno snapshot in Git, è molto difficile perdere le modifiche, specialmente se si esegue regolarmente il push sul database in un altro repository.

Git ha tre stati principali nel quale possono trovarsi i tuoi file: Commit, Modified, Staged:

1. Committed: Significa che i dati sono memorizzati in modo sicuro nel database locale.
2. Modified: Significa che i dati sono stati modificati ma ancora non è stato effettuato il commit.
3. Staged: Significa che i dati sono stati contrassegnati come modificati e sono pronti per essere committati come snapshot.

Questo ci porta alle tre sezioni principalidi un progetto Git:

1. La directory Git.
2. La Working Tree.
1. La Staging Area.

La directory Git è una directory dove Git memorizza i metadati e il database degli oggetti per il tuo progetto. Questa è la parte più importante di Git, ed è ciò che viene copiato quando cloni un repository da un'altro computer.

Il Working Tree è un singolo checkout di una versione del progetto. Questi file vengono estratti dal database compresso nella directory Git e posizionato su disco per essere utilizzato e modificato.

La Staging Area è un file, generalmente contenuto nella directory Git, che memorizza le informazioni su ciò che verrà inserito nel prossimo commit. Il suo nome tecnico nel gergo Git è "index", ma la frase "Staging Area" funziona altrettanto bene.

Il work flow Git è:

1. Modifica dei file nel Working Tree.
2. Stage selettivo dei singoli cambiamenti effettuati e/o che vuoi che facciano parte del commit. Aggiunge solamente cambiamenti nella Staging Area.
3. Fare un commit, prendendo i dati cosi come sono nella Staging Area. Memorizza nella tua directory Git in modo permanente, uno snapshot.

Se una particolare versione si trova nella directory Git, viene considerata Committed. Se è stata modificata ed è stata aggiunta nella Staging Area viene considerata Staged. Se è stata modificata rispetto al checkout ma non è ancora nella Staging Area, viene considerata Modified.
