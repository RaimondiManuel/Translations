# Git Pro Book #

## 1.1 Getting Started - About Version Control ##

In questo capitolo, introdurremo Git. Cominceremo illustrando il background dietro gli strumenti di versionamento, quindi ci sposteremo successivamente sulla procedura di avvio di Git nel vostro sistema, ed infine, come impostare Git per le sessioni di lavoro future.

### About Version Control ###

Che cos'è un VCS? perche dovreste preoccuparvene? Un VCS, Version Control System e un sitema di controllo di versione, creato allo scopo di tenere traccia dei cambiamenti su uno o più file, in modo tale da poter richiamare una versione specifica di questi in un secondo momento.

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

## 3.1 Git Branching - Branches in a Nutshell ##

Quasi ogni VCS ha qualche forma di supporto al branching. Per branching si intende, far divergere dalla linea principale di sviluppo, continuando a lavorare senza corrempere la solidita del progetto principale. In molti strumenti VCS, il branching è un processo molto costoso, in quanto richiede la copia dell'intero progetto, il che su progetti di grandi dimensioni, il prezzo in tempo e dimensioni potrebbero risultare davvero non trascurabili.

Alcune persone, si riferiscono al sistema di branching di Git come a una "Killer feature" e certamente distingue Git dal resto della comunity VCS. Il sistema di branching di Git è cosi speciale, grazie alla leggerezza, il che rendequasi istantaneo muoversi avanti e indietro fra di essi. A differenza di molti altri VCS, Git incoraggia l'utilizzo di un workflow basato sul branching e merging. Comprendere e padroneggiare questa funzione ti permetterà di avere a disposizione uno strumento molto potente, che cambierà il tuo modo di versionare.

### Branches in a Nutshell ###

Per comprendere veramente il modo in cui Git gestisce il branching, dobbiamo fare un passo indietro ed esaminare come Git immagazzina i suoi dati. 

Come potresti ricordare nella guida introduttiva, Git non memorizza i dati come una serie di changeset o di differenze, ma come una serie di snapshot.

Quando fai un commit, Git memorizza un'oggetto commit che contiene un puntatore allo snapshot del content che hai messo in stage. Questo progetto contiene anche il nome utentem la mail, il messaggio di commit, i puntatori e il puntatore al commit precedente a questo: Ciò significa che il commit iniziale non avrà puntatore, i commit successivi avranno un puntatore al commit precedente, il commit successivo ad un merge invece avrà più puntatori a diversi commits.

Per esempio, supponiamo di avere una directory contenente tre file, tutti inseriti nella staging area e successivamente committati. Per ogni file portato in stage verrà creato da Git un checksum (l'hash SHA-1 menzionato nella guida introduttiva), memorizzando poi la versione del file nel repository Git (riferendosi ad essi come blob) e aggiunge tale checksum all'area di staging.

```
$ git add README test.rb LICENSE
$ git commit -a -m "The initial commit of my project."
```
Quando si crea un commit effettuando `git commit`, Git fà il checksum di ogni subdirectory(in questo caso solo della root directory del progetto) e immagazzina gli oggetti dell'albero nel repository. Quindi, Git crea un oggetto commit contenente i metadati e un puntatore alla root del progetto, in modo tale da che possa ricreare quello snapshot quando necessario.

Il tuo repository Git ora contiene 5 oggetti: tre blob (ognuno rappresenta il contenuto di uno dei tre file), un albero che elenca il contenuto della directory e specifica quali nomi di file reppresentano quale blob, un puntatore alla root del progetto e tutti i metadati del commit.

Se si apportano modifiche e si esegue nuovamente un commit, il commit successivo memorizza un puntatore al commit immediatamente precedente.

Un branch Git è semplicemente un puntatore, mobile e leggero, ad uno di questi commits. Il nome del branch di default in Git è "master". Quando inizi a fare commit ti viene assegnato il branch master che punta all'ultimo commit effettuato. Ogni volta che si esegue un commit, il puntatore del ramo master si sposta in avanti automaticamente.

> Il branch "master" in Git non è un ramo speciale. E' esattamente come un qualsiasi altro branch. L'unica ragione per cui ogni altro repository ne ha uno è che il comando `git init` lo crea di default, e la maggior parte delle persone non si preoccupa di cambiarli.

Cosa succede se create un nuovo branch? crea semplicemente un nuovo puntatore per permetterti di muoverti lungo l'albero.

```
$ git branch testing
```
Questo crea un nuovo puntatore allo stesso commit sul quale sei attualmente. Quindi ora ci saranno due branch che puntano allo stesso commit.

Come fà Git a sapere su quale branch si sta puntando attuamente? Git mantiene un puntatore chiamato HEAD. Nota per HEAD non ha alcuna similitudine con il concetto di HEAD presente negli altri sistemi VCS come Subversion o CVS. In Git, HEAD è un puntatore al branch locale in cui ti trovi attualmente, in questo caso sarà "master". Il comando `git branch testing` ha creato solamente un nuovo branch, ma non ha spostato il puntatore HEAD su di esso. Potete vedere dove HEAD sta puntando con il comando `git log --decorate`

```
$ git log --oneline --decorate
 f30ab (HEAD->master, testing) Add feature #32
 34ac2 Fixed bug #1328 - Stack overflow under centain condition.
 98ca9 The initial commit of my project.
```

Potete vedere che i branch "master" e "testing" si trovano li nel commit f30ab.

### Switching Branches ###

Per passare ad un branch esistente, si esegue il comando `git checkout <branch>`

```
$ git checkout testing
```
In questo modo HEAD si sposterà sul branch "testing".

```
$ vim test.rb
$ git commit -a -m "Made a change."
```

Quando viene eseguito un commit il puntatore HEAD si sposta si sposta in avanti di un commit.

Ciò è interessante perchè ora il tuo branch "testing" si è spostanto in avanti, mentre il branch "master" punta ancora al commit cui ti trovavi quando hai eseguito il checkout. Ora torneremo al branch "master":

```
$ git checkout master
```

HEAD si è spostato indietro per puntare al branch "master", contemporaneamente si sono ripristinati i files nella working directory, allineandosi con lo snapshot a cui puntava master. Ciò significa che le modifiche apportate da questo punto in avanti divergeranno dalla versione precedente del progetto. In sostanza riavvolge il lavoro che hai svolto nel branch di "testing" in modo tale da poter andare in una direzione diversa.

> Il cambio di branch cambia i file nella vostra working directory. E' importante notare che quando cambiate branch in Git, i file nella vostra directory cambiano. Se passate ad un branch più vecchio, la vostra working directory verrà ripristinata in modo che assomigli all'ultima volta che è stato eseguito il commit su quel branch. Se Git non può farlo in modo pulito, Git si interromperà non permettendovi di compiere questa azione.

Facciamo alcune modifiche ed eseguiamo il commit ancora:

```
$ vim test.rb
$ git commit -a -m "Made other changes."
```
Da ora in poi la cronologia del progetto divergerà ( vedi Divergent history ), hai creato e sei passato ad un branch, lavorato su di esso, quindi tornato indietro al branch "master", e lavorato ancora. Entrambi questi cambiamenti sono isolati nel proprio branch. E' possibile spostarsi avanti e indietro fra i branches ed unirli una volta che lo vorrai, con i semplici comandi `branch`, `checkout`, `commit`.

Potete facilmente vedere cosa succede con il comando `git log`. Se eseguite il comando `git log --oneline --decorate --graph --all`, verrà stampata la history dei commits, mostrandovi dove si trova il vostro puntatore e come:

```
$ git log --oneline --decorate --graph --all
* cab9e (HEAD, master) Made other change.
| * 87ab2 (testing) Made a change.
| /
*  f30ab (HEAD->master, testing) Add feature #32
*  34ac2 Fixed bug #1328 - Stack overflow under centain condition.
*  98ca9 The initial commit of my project.
```

Poichè un branch in Git è in realtà un semplice file che contiene il checksum SHA-1 di 40 caratteri del commit a cui punta, i branch sono economici da creare e da distruggere. Creare un nuovo branch è semplice e veloce come scrivere 41 byte in un file.

Ciò è molto in contrasto con il modo in cui la maggior parte dei vecchi sistemi VCS gestiscono i branches, la qualo creano una copia di tutti i file del progetto in una seconda directory. Questo può richiedere un dispendio di tempo e spazio nella memoria nono indifferente, a seconda delle dimensioni del progetto. In Git questo processo è quasi istantaneo. Inoltre poichè poichè registriamo il genitore quando eseguiamo un commit, Git trova automaticamente una base per il merging. In caso debba essere fatto manualmete risulta comunque un compito facile. Queste funzionalità invogliano gli sviluppatori a creare e utilizzare branch più spesso.

## 3.2 Git Branching - Basic Branching an Merging ##

## 6.1 GitHub - Account Setup and Configuration ##

GitHub è il pù grande Host per i repository Git, ed è il punto centrale di collaborazione per molti sviluppatori e progetti. Una grande percentuale di tutti i repository Git è ospitata su GitHub e molti progetti open source la utilizzano per l'hosting Git, il monitoraggio, la revisione, e altre cose. Quindi, anche se non è una parte direttamente connessa a Git, molto probabilmente avrai bisogno di utilizzarlo in sinergia con Git.

Questo capitolo tratta l'uso efficace di GitHub. Ci occuperemo della registrazione di un account, nonchè della sua gestione, della creazione e dell uso di un repository Git, e dei work-flow comuni per contribuire ad un progetto e accettare un contributo ai tuoi progetti. Inoltr vedremo in dettaglio il funzionamento dell'interfaccia grafica e di tutti i trucchi per semplificarti la vita durante questi processi.

### Account Setup and Configuration ###

La prima cosa che bisogna fare è impostare un account utente gratuito. Basta visitare il sito https://github.com, scegliere un nome utenteche non sia già stato registrato, quindi fornire mail e password, facendo poi click sul pulsante "Iscriviti a GitHub".

La prossima cosa che vedrai sarà la pagina dei prezzi per i piani aggiornati, ma per ora sarà più comodo ignorarla. GitHub ti invierà una mailper verificare l'indirizzo che hai fornito. Esegui dunque la verifica.

> Nota: GitHub fornisce tutte le sue funzionalità con account gratuiti, con la limitazione che tutti i tuoi progetti sono pubblici (tutti avranno accesso in sola lettura.) I piani a pagamento di GitHub includono l'opzione di poter creare progetti privati.

 Facendo click sul logo octocat in alto a sinistra dello schermo, potrai accedere alla tua dashboard. Orai sei pronto per utilizzare GitHub

### SSH Access ###

A partire da ora, sei completamente in grado di connetterti con il repository Git utilizzando il protocollo https://, autenticandoti con il nome utente e la password cha hai appena configurato. Tuttavia per clonare progetti pubblici non è necessario nemmeno registrarsi. L'account appena creato entra in gioco quando dobbiamo fare un Fork di un progetto o facciamo una Pull Request di un progetto successivamente.

Se si desidera utilizzare SSH da remoto, avrete bisogno di configurare una chiave pubblica. (Se non se ne possiede una, consultare la generazione di chiavi pubbliche SSH.) Apri le impostazioni dell'account utilizzando il link in alto a destra della finestra.

img..

Quindi selezionare la SSH key sul lato sinistro.

img..

Da qui, clicckate sul pulsante "Add SSH Key" che vi restituirà il nome della chiave, quindi copiate il contenuto della vostra chiave pubblica ~/.ssh/id_rsa.pub (o come la avete chiamata) nella text area, quindi fate click su "Add Key".
> Assicuratevi di nominare le vostre chiavi SSH in modo che siano facili da ricordare. Potete assegnare un nome a ciascuna delle chiavi ( ad esempio "Il mio portatile" o "Account di lavoro") in modo tale che, nel caso si avesse bisogno di revocare una chiave in un secondo momento, sia possibile reperirle facilmente.

### Your Avatar ###

Officia deserunt eiusmod magna excepteur cupidatat occaecat excepteur. Ullamco dolor cupidatat minim do pariatur velit consectetur ut ad quis exercitation cillum. Esse ullamco excepteur amet ipsum Lorem sint occaecat.

Mollit tempor quis minim voluptate officia mollit pariatur excepteur aliqua. Minim nisi ex culpa nostrud exercitation officia aute est exercitation consequat excepteur nulla. Aliqua laborum exercitation aliqua in nisi velit Lorem tempor fugiat est et sit excepteur. Sit id et sunt culpa dolore sunt laboris elit. Laborum aliquip eu est ex non est elit eu ex sunt eiusmod sunt.

### Your Email Addresses ###

Il modo in cui GitHub mappa i Git commit, è legato alla mail della tua utenza, se utilizzate più indirizzi mail nei vostri commits e volete che GitHub li linki in maniera corretta, avrete bisogno di aggiungerli alla scheda mail della sezione admin.

img...

In Admin Email addresses possiamo vedere i diversi stati possibili. L'indirizzo in cima è verificato e impostato come indirizzo primario, ciò significa che riceverete a questa mail notifiche e ricevute. L'indirizzo secondario è verificato e può rimpiazzare il primario. L'ultimo indirizzo non è verificato quindi non potrete renderlo il vostro indirizzo primario. Se GitHub non vede nessuno di questi nei commit, i vostri commit verranno linkati al vostro nome utente attuale.

Pariatur enim tempor ea labore anim nostrud tempor dolor est tempor sit do eu. Esse ea ullamco consectetur nisi ullamco esse esse officia laborum commodo. Nisi dolor enim magna elit nisi reprehenderit elit occaecat quis laboris dolor. Lorem tempor eiusmod nostrud aliqua adipisicing id minim et occaecat. Commodo voluptate qui nulla pariatur magna incididunt sint pariatur ea. Consectetur ea cillum et do duis magna aliqua occaecat voluptate quis officia veniam.

Mollit velit laborum nisi pariatur. Amet veniam ea amet mollit duis ipsum aliqua elit magna eu nostrud eu. Quis consequat magna nulla duis culpa nulla irure ea ad commodo et. Laborum excepteur consequat id eiusmod sint officia ad occaecat occaecat sunt sunt minim ea voluptate. Reprehenderit ipsum qui aliquip consequat voluptate in aliqua officia eiusmod laboris tempor in.