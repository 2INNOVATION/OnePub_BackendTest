# ⚡️ Scrivere una libreria su una repo privata Onepub


Da terminale inserire i seguenti comandi:

```bash
$ dart pub global activate onepub  #installare onepub
$ export PATH="$PATH":"$HOME/.pub-cache/bin"  #esportare il percorso della directory dove è installato 
$ onepub login   #faccio il login
$ dart create packagetest1 #creare una repo in Dart all'interno della quale scrivero le mie librerie
$ cd packagetest1 #entrare dentro la repo 
$ onepub pub private  #rendere privata la repo, questa sarà accessibile dal propietario e dagli altri account che fanno parte dell'organizzazione, aggiunge il comando 'publish_to: `https://onepub.dev/api/myPrivateRepo/` al file pubspec.yaml

# Prima della pubblicazione della repo assicurarsi di aver seguito le Best Practice

$ dart pub publish   #pubblico la repo
```

Best Practice da seguire quando si crea una libreria 


1. Rivedi il nome del tuo pacchetto nel file `pubspec.yaml`. Se prevedi di pubblicare su pub.dev, il nome deve essere univoco. Se hai intenzione di pubblicare su OnePub, il nome deve essere univoco solo all'interno della tua organizzazione.

2. Aggiorna il numero di versione del pacchetto. Dovresti impostarlo su una versione pre-rilasciata (a meno che il tuo pacchetto non sia già stabile), come "0.0.1-beta.1".

3. Aggiorna l'attributo della descrizione nel tuo file `pubspec.yaml` per riflettere l'uso previsto del tuo pacchetto.

4. Aggiorna il file `README.md` e fornisci della documentazione utile su come utilizzare il tuo pacchetto.

5. Aggiorna il file `CHANGELOG.md`. Deve menzionare il numero di versione che appare nel tuo file `pubspec.yaml`.

6. Se hai intenzione di pubblicare su pub.dev, aggiungi un file `LICENSE.md`. Se utilizzi GitHub, ha una funzione per aggiungere la maggior parte dei tipi di licenza comuni al tuo pacchetto. Nella scheda 'Code', clicca sul pulsante 'Add File', chiama il file LICENSE.md e GitHub ti chiederà di scegliere un modello di licenza. 
Se la repo viene pubblicata su Onepub basta inserire nella root un file chiamato LICENSE.

7. Dentro la cartella lib, si trova il file principale omonino (packagetest1.dart) dove inserire gli import di tutti i file secondari presenti nella cartella src.
Il file packagetest1.dart chiamato barrell file, sarà così scritto:

library packagetest1;
export 'src/add.dart' show add;
export 'src/greetUser.dart' show greetUser;

int calculate() {
  return 6 * 7;
}

Dentro la cartella src avrò add.dart e greetUser.Dart


# ⚡️ Caricare una libreria da una repo privata Onepub

Nel caso in cui l'utente non conincide con il proprietario della repo privata, bisogna assicurarsi di aver ricevuto ed accettato l'invito da parte del proprietario della repo per far parte dell'organizzazione, l'invito si invia dalla pagina (https://onepub.dev/members) di Onepub.

Da terminale inserire i seguenti comandi:

```bash
$ dart pub global activate onepub  #installo onepub
$ export PATH="$PATH":"$HOME/.pub-cache/bin"  #esporto il percorso della directory dove è installato 
$ onepub login   #faccio il login
$ cd myproject  #entro dentro la cartello del mio progetto
$ onepub pub add packagetest1  #aggiungo all mia lista delle dipendenze del mi progetto la repo packagetest1
$ dart pub get    #aggiorno tutte le librerie da cui dipende il mio progetto
```


# ⚡️ Workflow Github

All'interno del Workflow di Github è previsto l'implementazione di Onepub. In questo caso il proprietario della repo deve creare un Account CI/CD dalla pagina (https://onepub.dev/members) di Onepub, dopo bisogna esportare il token e salvarlo su GitHub Secret. Il workflow di Github si trova dentro il file main.yaml nel percorso `./.github/workflows` .


## ℹ️  Informazioni Aggiuntive

1. Per utilizzare il sistema Onepub su flutter, i comandi e le procedure sono le medesime, basta soltanto sostituire la stringa `dart` con `flutter` all'interno dei comandi.
2. Una volta pubblicata una repo, che sia sua Dart o Onepub, questa non potrà essere più eliminata, si potrà solamente contrassegnare come deprecata.
3. Per pubblicare una repo e renderla disponibile a tutti gli utenti Dart, bisgogna assicurarsi che nel file pubspec.yaml sia presente questo comando: `publish_to: none`, testare e validare la libreria quindi eseguire i seguenti comandi: 

```bash
$ cd myproject  #entro dentro la cartello del mio progetto
$ dart pub publish  #aggiorno tutte le librerie da cui dipende il mio progetto
```
