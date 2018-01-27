# FixIt

* Ruby version
    ruby 2.5.0
    Rails 5.1.4
    
* System dependencies
    E' necessarrio installare minimagic
    In ambiente linux usare i sueguenti comandi
    ```
    sudo apt-get update
    sudo apt-get install imagemagick
    
    ```

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...





L’obiettivo del progetto è quello di creare un sistema che possa raccogliere informazioni riguardanti disagi e disservizi presenti nel territorio pubblico. Queste informazioni vengono inserite dai cittadini, purché essi abbiano un profilo riconosciuto dal sistema (chiameremo questa tipologia di utenti Notifier), attraverso un modulo che definiremo più avanti e che chiameremo Report. Il sistema, oltre ai profili degli utenti e ai Report, deve gestire quelli che sono i destinatari di tali Report. Questi ultimi sono gruppi, Division, e sottogruppi di dipendenti, Employee, che gestiscono diverse categorie di Report e appartengono ciascuno a un determinato ente pubblico o privato di interesse pubblico (Organization).
Attraverso le coordinate polari associate a ciascun Report, il sistema deve identificare la Division specifica destinataria del Report stesso. Quest’ultima mantiene le informazioni necessarie per tracciare i confini del proprio territorio di competenza per ciascuna categoria di Report.
Ciascun Report attraversa diversi stati dal momento della creazione al momento in cui viene archiviato (operazione fatta dagli Employee). In particolare e in prima analisi definiamo i seguenti stati:
    • Waiting. Indica che il Report deve essere approvato. In questo stato può essere commentato, aggiornato dagli Operative (un particolare tipo di Signaler) o indicare, attraverso un valore, l’urgenza d’intervento.
    • Running. Indica che il Report è stato approvato e resta in questo stato fino alla conclusione dell’intervento sul territorio.
    • Complete. Indica che l’intervento è stato concluso per cui il disagio rappresentato Report non è più tale.
Poiché nei primi due stati un Report rappresenta un problema, esso è visibile a qualsiasi tipologia di utente del sistema, mentre nell’ultimo stato esso è visibile solo nello storico del suo creatore e dagli Employee.
    1. Funzionalità offerte agli utenti. In primo luogo, ogni cittadino per inviare un Report deve poter creare un profilo con il quale può accedere a determinate funzionalità, fra le quali, quella di creare un Report. Inoltre, un profilo aiuta a proteggere il sistema da un uso sconsiderato. Quindi ogni Notifier o Operative può creare e inviare Report. Inoltre queste tipologie di utenti possono aggiungere informazioni ai Report attraverso i commenti e i tag, e possono accedere allo storico delle proprie attività nel sistema.

La funzione principale offerta al generico utente del sistema, che sia registrato o meno, è effettuare ricerche di Report su percorsi che possono rappresentare ostacoli o rallentamenti al passaggio. Inoltre, il generico utente, può accedere alle informazioni contenute nel sistema attraverso strumenti di ricerca come i filtri e i tag, e di strumenti di visualizzazione come mappe.

La controparte dei segnalatori (ovvero l’insieme degli Employee), accedono ad un’area diversa del sistema appositamente creata, che permette loro di gestire i Report in “back-and”. Poiché l’applicazione da questo punto di vista ha scopo prevalentemente informativo, ci si limita a offrire loro alcune funzionalità come quella di definire i territori di competenza in base ai quali si determina il gruppo destinatario di ciascun Report, le funzionalità necessarie per la corretta gestione dei gruppi e dei suoi membri, la possibilità di interagire con membri dello stesso gruppo, aggiungere contenuti informativi ai Report, definire nuove categorie di problemi.

    2. Interazione con i servizi esterni. Per creare una mappatura dei Report visibile all’utente e per ottenere le coordinate polari del luogo del disaggio da inserire nel relativo Report, ci si appoggia ai servizi offerti da Google Maps. In particolare vengono usate le API: Google Maps Directions e Google Maps Geocoding.
    • Google Maps Directions API viene usato per calcolare percorsi stradali fra due luoghi distinti sui quali verranno indicati i Report.
    • Google Maps Geocoding API viene usata per la geo-codifica.

    3. Descrizione dei dati gestiti. Report. Le informazioni inserite dagli utenti avvengono attraverso questo modulo che prevede in prima analisi alcuni campi di base come il luogo, un oggetto, una tipologia, una breve descrizione, un campo che indica lo stato corrente in cui il Report stesso si trova, le coordinate polari che indicano la posizione esatta del disagio sulla mappa, ed eventualmente degli allegati (prevalentemente immagini).

Division. I gruppi di Employee e Operative devono avere un nome, una descrizione, un Leader fra gli Employee un eventuale logo e un riferimento fra l’ente di appartenenza e un Division padre.

Notifier, Operative ed Employee. Il sistema tiene traccia delle identità dei cittadini che effettuano i Report e di coloro che li gestiscono. In particolare prevede alcuni campi in comune ad entrambi come email e password. Inoltre, ai Notifier si aggiungono i campi username e immagine profilo, ai Operative ed Employee si aggiungono i campi nome, cognome, la Division di appartenenza ed eventualmente una matricola.

Maps. Contengono le informazioni sulle territori di competenza delle Division

Organizzation. Ogni ente deve avere un nome ed eventualmente un logo e una descrizione.
Altri dati come commenti, note, avvisi, notifiche, tag e allegati devono essere gestiti dal sistema.

    4. Ruoli. E’ possibile individuare i seguenti ruoli:
    • Notifier: ha i permessi di accedere in scrittura e lettura a Report e commenti.
    • Operative: ha i permessi di accedere in scrittura, aggiornamento e lettura ai Report. Inoltre come i Notifier possono accedere in scrittura e lettura ai commenti
    • Employee. Ha tutti i permessi di sui Report
    • Leader. Hai tutti i permessi di Employee e tutti i permessi sui propri Division e le relative mappe
    • Admin. Gli vengono assegnati tutti i permessi su tutte le informazioni nel database.
