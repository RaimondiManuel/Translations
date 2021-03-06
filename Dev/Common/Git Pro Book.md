# Git Pro Book #

## 1.1 Getting Started - About Version Control ##

In questo capitolo, introdurremo Git, cominceremo illustrando il background dietro gli strumenti di versionamento, quindi ci sposteremo successivamente sulla procedura di avvio di Git nel vostro sistema, ed infine, come impostare Git per le sessioni di lavoro future.

### About Version Control ###

Che cos'è un VCS e perche dovreste preoccuparvene? Un VCS, Version Control System e un sitema di controllo di versione, creato allo scopo di tenere traccia dei cambiamenti su uno o più file, in modo tale da poter richiamare una versione specifica di questi in un secondo momento.

Se sei un grafico o un web designer, potresti voler tenere traccia di tutte le versioni di un immagine, oppure di un layout. In questo caso un VCS è la cosa più saggia da utilizzare. Un VCS ti consente di ripristinare lo stato uno o più file, che hai selezionato, ad una loro versione precedente, oppure, riportare l'intero progetto al suo stato iniziale, oppure, fare una comparazione dei cambiamenti avvenuti in corso d'opera. è possibile anche vedere chi ha effettuato l'ultima modifica. L'introduzione di un VCS nel proprio work flow, comporta anche tenere al sicuro il proprio progetto da un'eventuale corruzione dei file, poichè ne rende possibile il recupero.

### Local Version Control System ###

Molte persone utilizzano come metodo di controllo di versione, quello di copiare tutto il progetto in un'altra cartella. Questo approccio è molto comune, poichè di semplice da eseguire, tuttavia, è un'approccio incline ad errori. è facile dimenticare la directory in cui ci si trova al momento, e quindi scrivere sul file sbagliato, oppure, copiare un file errato senza che se ne avesse l'intenzione.

I VCS sono stati realizzati proprio allo scopo di risolvere questa problematica. I primi VCS erano locali alla macchina, con un database anchesso locale, il cui scopo, era quello di conservare le modifiche effettuate sotto VCS.

![Local version control system.](https://git-scm.com/book/en/v2/images/local.png)

Uno degli strumenti VCS più popolari era RCS, che viene ancora oggi, distribuito su molti computer. RCS funzionava mantenendo un set di patch, una raccolta di differenze tra file, in un formato apposito su disco. Poteva quindi ricreare l'aspetto di un qualsiasi file in qualsiasi momento, tramite l'aggiunta di tutte le patch.

### Centralized Version Control System ###

Il problema principale che le persone si trovano ad affrontare, è il bisogno di dover condividere il lavoro con altri sviluppatori, i quali lavorano su sistemi diversi. Per far fronte a questo problema, sono stati sviluppati VCS centralizzati, chiamati CVCS, Centralized Version Control System. Questi sistemi, come CVS, SVN, Preforce, sono basati su un singolo server, il quale è proprietario di tutti i file, nonche, un certo numero di client che gestiscono i file basandosi su quella posizione centrale. Per molti anni, questo è stato lo standardper i VCS.

![Centralized version control system.](https://git-scm.com/book/en/v2/images/centralized.png)

Questo setup offre numerosi vantaggi, in particolare rispetto ai VCS locali. Ad desempio, in una certa misura, tutti sanno cio che fanno tutti all'interno del progetto. Gli amministratori hanno un controllo preciso su chi può fare cosa, ed è nolto più facile amministrare un CVCS che gestire un database locale per n client. Tuttavia, questo setup ha anche dei difetti. Uno dei più ovvi è il single point of failure che rappresnta un server centralizzato. Se quel server si interrompe per un'ora, nessuno può collaborare o salvare le modifiche effettuate. Se il progetto sul server centrale è danneggiato o corrotto, si perde ogni progresso fatto. Anche i server VCS locali soffrono di questo stesso problema. Ogni volta che la cronologia dei cambiamenti viene gestita in un singolo punto, è inesorabilmente presente, questo tipo di problematica. 

### Distributed Version Control System ###

è qui che entrano in gioco i DCVS, Distributed Control Version System. In un DVCS i client non controllano solamente l'ultimo snapshot del file. I client hanno il controllo sull'intero repository, inclusa tutta la sua cronologia. Pertanto, se il server viene compromesso in qualche modo, e questi client lavorano basandosi su questo server, ognuno dei client avrà a disposizione una versione sana del repository, con cui poter ripristinare lo stato del server. Pertanto ogni client è un vero e proprio backup di ciò che è contenuto nel server.

![Distributed version control system.](https://git-scm.com/book/en/v2/images/distributed.png)

Inoltre i DCVS si comportano molto bene nel gestire diversi repository remoti, in modo tale da permettere a diversi gruppi con diversi work flow di poter lavorare sullo stesso progetto contemporaneamente. Ciò consente di impostare diversi work flow, cosa impossibile nei CVCS.

## 1.2 Getting Started - A Short History of Git ##

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

## 1.3 Getting Started - Git Basics ##

Quindi, cos'è in poche parole Git? questa è una sezione importante da assimilare perchè se capisci cos'è Git el le basi del funzionamento sarà possibile utilizzare Git in modo efficace e probabilmente molto più facile. Mentre apprendi Git è necessario dimenticare gli altri sistemi di versioning. In questo modo eviterai confusione durante l'utilizzo dello strumento. Anche se l'interfaccia Git è molto simile agli altri strumenti in commercio , Git memorizza e pensa alle informazioni in modo molto diverso, e la comprensione di queste differenze ti aiuterà ad evitare confonderti durante l'utilizzo.

### Snapshot, Not Differences ###

La principale differenza tra Git e qualsiasi altro VCS( Subversion ecc... ) è il modo in cui Git pensa ai suoi dati. Concettualmente la maggior parte dei sistemi memorizza le informazioni come un elenco di modifiche basato su file. Questi altri sistemi(CVS, Subversion, Preforce, Bazaar e cosi via) pensano alle informazioni che memorizzano come un insieme di file e modifiche apportate a ciascun file nel tempo(questo è comunemente descritto come VCS delta based).

![Storing data as changes to a base version of each file.](https://git-scm.com/book/en/v2/images/deltas.png)

Git non pensa o conserva i suoi dati in questo modo. Invece Git pensa ai suoi dati più come ad una serie di snapshot di un filesystem in miniatura. Con Git, ogni volta che si esegue un commit o si salva lo stato del proprio progetto, Git fa sostanzialmente uno snapshot di come appaiono i tutti file in quel momento e memorizza un riferimento a quello snapshot. Per essere efficente, se i file non sono stati modificati, Git non memorizza nuovamente i file, ma solo un collegamento al file precedente. Git pensa ai sui dati più come un flusso di snapshot.

![Storing data as snapshots of the project over time.](https://git-scm.com/book/en/v2/images/snapshots.png)

Questa è una distinzione importante tra Git e quasi tutti gli altri VCS. Ciò ha causato a Git di dover riconsiderare quasi ogni aspetto del controllo di versione che la maggior parte degli altri sistemi hanno copiato dalla generazione precedente. Questo rende Git più simile ad un mini filesystem con alcuni incredibili strumenti costruiti attorno ad esso, piuttosto che un semplice VCS. Esploreremo alcuni dei vantaggi cheottieni pensando ai tuoi dati in questa maniera, quando parleremo di branching.

### Nearly Every Operation is Local ###

La maggior parte delle operazioni in Git necessitano solo di file o risorse locali per funzionare, in genere non sono necessarie informazioni da un altro computer per funzionare. Se sei abituato ad un CVCS in cui la maggior parte delle operazioni ha una tale latenza di rete, ciò torna molto utile, poichè hai a disposizione l'intera cronologia del progetto sul tuo disco locale, la maggior parte delle operazioni sembrano quasi istantanee. Ad esempio, per esplorare la cronologia del progetto, Git non ha bisogno di uscire sul server per mostrarla, semplicemente, legge dal tuo database locale.

Ciò significa anche che ci sono poche cose che non si possono fare se non si è online o fuori VPN.

### Git Has Integrity ###

Tutto in Git viene verificato prima del commit, verifica definita in un checksum. Ciò significa che è impossibile effettuare un cambiamento di contenuto di un file o di una directory senza che Git ne sia a conoscenza. Questa feature è integrata in Git a basso livello ed è parte integrante della sua filosofia. Non è possibile perdere le informazioni in transito e ottenere la corruzione dei file senza che Git se ne accorga.

Il meccanismo che Git usa per il checksum è chiamato SHA-1. Questa è una stringa di 40 caratteri esadecimali (0-9 e a-f) e calcolata in base al contenuto di un file e dalla struttura delle directory nel progetto Git. Un hash SHA-1 ha un aspetto simile:

`24b9da6552252987aa493b52f8696cd6d3600373`

Vedrai questi valori hash ovunque in Git, infatti, Git memorizza tutto nel suo database. Non per nome del file, ma per valore di hash. Git in genere aggiunge solo dati.

### Git Generally Only Adds Data ###

Quando esegui azioni in Git, quasi tutte aggiungono dati. è difficile far compiere a Git un'azione non annullabile o cancellare dati in qualsiasi modo. Come con qualsiasi VCS, puoi perdere o rovinare le modifiche che non hai ancora eseguito, ma dopo aver effettuato uno snapshot in Git, è molto difficile perdere le modifiche, specialmente se si esegue regolarmente il push sul database in un altro repository.

Git ha tre stati principali nel quale possono trovarsi i tuoi file: Commit, Modified, Staged:

1. Committed: Significa che i dati sono memorizzati in modo sicuro nel database locale.
2. Modified: Significa che i dati sono stati modificati ma ancora non è stato effettuato il commit.
3. Staged: Significa che i dati sono stati contrassegnati come modificati e sono pronti per essere committati come snapshot.

Questo ci porta alle tre sezioni principalidi un progetto Git:

1. La directory Git.
2. La Working Tree.
1. La Staging Area.

![Working tree, staging area, and Git directory.](https://git-scm.com/book/en/v2/images/areas.png)

La directory Git è una directory dove Git memorizza i metadati e il database degli oggetti per il tuo progetto. Questa è la parte più importante di Git, ed è ciò che viene copiato quando cloni un repository da un'altro computer.

Il Working Tree è un singolo checkout di una versione del progetto. Questi file vengono estratti dal database compresso nella directory Git e posizionato su disco per essere utilizzato e modificato.

La Staging Area è un file, generalmente contenuto nella directory Git, che memorizza le informazioni su ciò che verrà inserito nel prossimo commit. Il suo nome tecnico nel gergo Git è "index", ma la frase "Staging Area" funziona altrettanto bene.

Il work flow Git è:

1. Modifica dei file nel Working Tree.
2. Stage selettivo dei singoli cambiamenti effettuati e/o che vuoi che facciano parte del commit. Aggiunge solamente cambiamenti nella Staging Area.
3. Fare un commit, prendendo i dati cosi come sono nella Staging Area. Memorizza nella tua directory Git in modo permanente, uno snapshot.

Se una particolare versione si trova nella directory Git, viene considerata Committed. Se è stata modificata ed è stata aggiunta nella Staging Area viene considerata Staged. Se è stata modificata rispetto al checkout ma non è ancora nella Staging Area, viene considerata Modified.

## 1.4 Getting Started - The Command Line ##

Ci sono molti modi diversi di utilizzare Git. C'è la linea di comando, e molte interfacce grafiche dotate di molte features. Per questo libro, utilizzeremo Git da linea di comando, poichè, dalla linea di comando è possibile eseguire tutti i comandi Git, mentre, le GUI, per semplicità, implementano solo un parziale sottoinsieme delle features di Git. Se si è in grado di utilizzare la command-line, si sarà molto probabilmente anche in grado di utilizzare la maggior parte delle GUI. Inoltre la linea di comando è uno strumento disponibile a tutti.

## 1.6 Getting Started - First Time Git Setup ##

Ora che avete Git nel vostro sistema, ti consigliamo di fare alcune cose per personalizzareil tuo ambiente Git. Dovrebbe essere fatto una sola volta su un dato computer. è possibile comunque cambiare le impostazioni in qualsiasi momento.

Git viene fornito con uno strumento chiamato `git config` che consente di leggere e scrivere variabili di configurazioni che controllano come Git appare e opera. Queste variabili possono essere memorizzate in tre punti diversi.

`/etc/config` file: Contiene valori applicati ad ogni utente sul sistema e su tutti i relativi repository. Se si passa l'opzione `--system` a `git config` esso legge e scrive direttamente su questo file. Poichè si tratta di un file di configurazione di sistema è necessario avere i privilegi di amministratore o super utente per apportare modifiche a questo file.

`~/.gitconfig` o `~/.config/git/config` file: Contiene valori applicati al singolo utente sui relativi repository. Perchè l'utente legga e scriva su di un file è necessario passare l'opzione `--global`. Questo ha effetto su tutti i repository su cui lavori all'interno del sistema.

Il file di configurazione nella directory di Git, specifico per quel repository. Puoi forzare Git a leggere e scrivere su questo file passando l'opzione `--local`. Di fatto `--local` è l'opzione predefinita. Non sorprendentemente, è necessario trovarsi da qualche parte in un repository Git perchè questa opzione sia valida.

Ogni livello sovrascrive i valori il livello precedente, quindi, i valori in `~git/config` sovrascriveranno quelli di `/etc/config`.

Sui sistemi WindowsGit cerca i file `.gitconfig` nella directory `$HOME`. Cerca anche `/etc/config` anche se è relativo alla root msys, che è ovuque tu decida di installare Git.

Questo file può essere modificato solo da `git config -f <file>` come amministratore.

### Your Identity ###

La prima cosa che dovresti fare quando installi Git è impostare il tuo nome utente e l'indirizzo mail. Questo è importante poichè ogni commit Git usa queste informazioni. Inoltre queste informazioni sono incluse nei commit che farai.
```
$ git config --global user.name "Jhon Doe"
$ git config --global user.mail "jhondoe@example.com"
```

è necessario farlo solamente se l'opzione `--global` viene passata. Git userà sempre quell'informazione per qualsiasi cosa tu faccia su quel sistema. Se si desidera eseguire l'override di questi con un nome diverso o un'indirizzo mail diverso per progetti specifici, è possibile eseguire l'operazione senza l'utilizzo dell'opzione `--global` quando ci si trova in quel progetto.

Molti degli strumenti della GUI vi aiuteranno a fare il login al primo avvio.

### Your Editor ###

Ora che la vostra identità è stata impostata, potete configurare un text-editor di default che sarà utilizzato quando Git avrà bisogno di digitare un messaggio. Se non configurato, Git utilizza l'editor predefinito del sistema.

Se si desidera utilizzare un'editor di testo diverso, è possibile effettuare le seguenti operazioni.
```
$ git config --global core.editor <editor>
```

Su un sistema Windows, se si desidera utilizzare un'editor diverso, è necessario specificare il percorso completo del file eseguibile.

### Checking Your Settings ###

Se si desidera verificare le impostazioni di configurazione, è possibile utilizzare il comando `git config --list` per elencare tutte le impostazioni che Git può trovare in quel punto.
```
$ git config --list
    user.name=Jhon Doe
    user.mail=jhondoe@example.com
    color.status=auto
    color.branch=auto
    color.interactive=auto
    color.diff=auto
    ...
```
è possible trovare le chiavi più di una volta poichè Git legge la stessa chiave da diversi file(per esempio `/etc/config` e `~/.gitconfig`) In questo caso Git da valore solamente all'ultima volta che la chiave è stata definita.

Puoi anche controllare cosa pensa Git su di uno specifico `git config <key>`:
```
$ git config user.name
 Jhon Doe
```

> Poichè Git potrebbe trovare la stessa chiave definita più volte, in più file, è possibile trovarsi con un valore imprevisto, senza saperne il motivo. In casi come questo puoi interrogare Gitsull'origine di quel valore utilizzando: `git config --show-origin <key>`.

## 1.7 Getting Started - Getting Help ##

Potresti occasionalmente avere bisogno di aiuto mentre utilizzi Git, ci sono due modi equivalenti per ottenerlo.
```
$ git help <verb>
$ man git-<verb>
```
Per sempio potete visionare l'help manpage per il comando `git config`:
```
$ git config help
```

Questi comandi sono interessanti perchè vi si può accedere ovunque, anche offline.

## 2.1 Git Basics - Getting a Git Repository ##

Se avete la possibilitàdi leggere solo un capitolo, dovreste leggere questo. Questo capitolo offre una panoramica su tutti i comandi necessari a compiere la maggior parte delle azioni utili in Git. Entro la fine del capitolo dovresti essere in grado di:

1. Configurare e analizzare un repository.
2. Avviare e arrestare il tracking di uno o più file.
3. Portare in stage e committare i cambiamenti.

Ti mostrerò anche come impostare Git perchè ignori determinati file e/o file pattern. Come annullare gli errori in modo facile e veloce, come sfogliare la cronologia del tuo progetto e visualizzare le modifiche fra i commit e come effettuare push e pull da e verso i repository remoti.

### Getting a Git Repository ###

Solitamente è possibile ottenere un repository Git in due modi.

1. Puoi prendere una directory locale che al momento non è ancora versionata e trasformarlo in un repository Git.
2. Potete clonare un repository esistente.

In entrambi i casi si ottiene un repository Git in locale sulla propria macchina pronto all'uso.

### Initializing  a Repository in Any Existing Directory ###

Se avrete una directory di un progetto che al momento non è sotto version control e volete iniziare a gestirlo con Git, avrete prima bisogno di andare nella directory di quel progetto:
```
$ cd /user/user/my-project
```
e digitare..
```
$ git init
```
Ciò crea una nuova subdirectory chiamata `.git` che contiene uno scheletro di repository. A questo punto però, il vostro repository non è ancora stato tracciato.

Se volete avviare il versioning di file già esistenti dovete iniziale a tracciare quei file a fare un commit iniziale in questo modo
```
$ git add *
$ git add LICENCE
$ git commit -m "Initial project version"
```
Vedremo cosa fanno questi comandi in un minuto. A questo punto, hai un repository Git con file tracciati e un commit iniziale.

### Cloning an Existing Repository ###

Se volete avere la copia di un repository già esistente, il comando necessario è `git clone`. Se hai familiarità con altri sistemi di versioning, noterai che è il comandi di clone e non checkout, questa è una distinzione importante: invece di ottenere solo una copia funzionante, Git riceve una copia completa di quasi tutti i dati sul server. Ogni revisione di ogni file per la history del progetto, viene eseguito un pull di default quando eseguite un clone, infatti, se il disco del tuo server viene danneggiato, puoi nella maggior parte dei casi, utilizzare il clone nel client per riportare il server allo stato in cui era, quando è stato clonato.

Si clona un repository Git utilizzando il comando 
```
$ git clone https://github.com/libgit2/libgit2`
```
Ciò crea una directory chiamata in qualche modo diverso da libgit2. Volendo puoi specificare il nome della directory.
```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```
Quel comando fà la stessa cosa del precedente ma la directory di destinazione verrà chiamata mylibgit.

sasdasdsadasdsa