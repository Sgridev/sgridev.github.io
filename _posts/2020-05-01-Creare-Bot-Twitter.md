---
layout: post
title: "Come creare un bot di Twitter in C#"
date: 2020-05-01
excerpt: "Utilizzare le API Twitter per creare un bot"
tags: [Twitter, Twitter Bot, Bot, Andrea Grisafi, .NET, C#]
feature: https://media.wired.com/photos/5a55b72db1cfb87f3206aa5b/master/w_582,c_limit/Twitter-Hole-featured.jpg
comments: false
---
Tutti i giorni ripetiamo le stesse azioni quasi in modo automatico: ad esempio quando ci si laviamo i denti o mangiamo.  
Ciò che ci sfugge è tutto il tempo perso nel farlo.  
Lavandoci i denti per 5 minuti al giorno, alla fine dell'anno avremo occupato più di 30 ore del nostro tempo.  
Fortunatamente, nel mondo informatico molte azioni sono programmabili e di conseguenza automatizzabili.  
Ad esempio: nella noia di un giorno estivo dello scorso anno, decisi di creare un account di Twitter con il solo scopo di ricordare alla mia ragazza quanto fosse bella.  
Non fidandomi della scarseggiante costanza che possiedo, scartai subito l'opzione di fare i post a mano ogni giorno.  
Dopo un averci riflettuto su, decisi di creare un piccolo programma in C# che comunicasse con le [API](https://en.wikipedia.org/wiki/Application_programming_interface) di Twitter per creare un nuovo post.  
Per far avviare l'applicazione ogni 24 ore scelsi di utilizzare il Task Scheduler di Windows, hostato su un'istanza EC2 gratuita fornita da AWS.  
Il risultato fu [questo](https://twitter.com/sarabellxmbot).  
Ora basta con le premesse, mettiamoci all'opera.




# 1) Ottenere un account Twitter developer
![_config.yml]({{ site.baseurl }}/assets/img/twitterPost/twitter1.png)  
Per prima cosa dobbiamo richiedere ed ottenere un account Twitter Developer per entrare in possesso dei token necessari per poter comunicare con l'API di Twitter.  
Per andare direttamente alla pagina di richiesta segui questo [link](https://developer.twitter.com/en/apply-for-access).  
Nel mio caso l'accesso è stato ottenuto in meno di 15 minuti, ma Twitter specifica che il processo potrebbe richiedere anche diverse ore.  
Dopo aver ottenuto l'accesso, compiliamo il modulo di creazione app all'interno della dashboard e generiamo i token e le chiavi.  

# 2) Creare un nuovo progetto ed installare Tweetsharp
Creiamo un progetto console (.NET Framework o .NET Core) da [Visual Studio](https://visualstudio.microsoft.com/it/downloads/) e diamogli il nome che preferiamo.  
Fortunatamente, alcuni programmatori prima di noi si sono presi la briga di creare interfacce tra l'API di Twitter e il nostro programma, per semplificare l'utilizzo dell'API stessa.  
Una di queste è [TweetSharp](https://github.com/shugonta/tweetsharp).
Installiamola cliccando nel menù Progetto->Gestisci Pacchetti Nuget, cerchiamo "TweetSharp" e clicchiamo su installa.  
Il pacchetto nuget scaricato installerà tutte le referenze necessarie per utilizzare Tweetsharp all'interno del nostro progetto.  
Ora possiamo aggiungere la direttiva in cima alla nostra classe Program.cs.  
{% highlight csharp %}
using TweetSharp;
{% endhighlight %}

# 3) Inserire i token e le chiavi di accesso
Torniamo nella nostra dashboard di Twitter e copiamo le chiavi e i token, o generiamole se non sono ancora state create.  
Dichiariamole all'interno del nostro programma.
{% highlight csharp %}
private static string customer_key = ConfigurationManager.AppSettings["customer_key"];
private static string customer_key_secret = ConfigurationManager.AppSettings["customer_key_secret"];
private static string access_token = ConfigurationManager.AppSettings["access_token"];
private static string access_token_secret = ConfigurationManager.AppSettings["access_token_secret"];
{% endhighlight %}  
Il mio consiglio è quello di inserire le chiavi all'interno dell'App.config, in modo da poterle nascondere dal codice e soprattutto modificarle senza il bisogno di ricompilare la nostra applicazione.  
Ora creiamo un TwitterService passandogli tutte le nostre chiavi:  
{% highlight csharp %}
private static TwitterService service = new TwitterService(customer_key, customer_key_secret, access_token, access_token_secret);
{% endhighlight %}  

# 4) Creare il metodo di invio tweet
Inseriamo il metodo SendTweet all'interno del nostro programma, passando come parametro una stringa, che rappresenta lo stato che vogliamo twittare.  
  {% highlight csharp %}
  private static void SendTweet(string _status)
        {
            service.SendTweet(new SendTweetOptions{ Status = _status} , (tweet, response) =>
            {
                if(response.StatusCode == System.Net.HttpStatusCode.OK){
                    Console.WriteLine($"<{DateTime.Now}> - Tweet Sent!");
                    Environment.Exit(0);
                }
            else
                    Console.WriteLine($"<ERROR> " + response.Error.Message);
        });
        }
{% endhighlight %}  
Il metodo controllerà l'effettiva trasmissione del tweet all'API di twitter.  
In caso di successo stamperà l'orario di invio e chiuderà l'applicazione.   
In caso di errore invece, stamperà l'errore e lascerà aperta l'applicazione.  

# 5) Chiamare il metodo all'interno della nostra applicazione
All'interno del nostro Main chiamiamo il metodo SendTweet e passiamogli la stringa di testo che vogliamo twittare.  
  {% highlight csharp %}
  static void Main(string[] args)
        {
            Console.WriteLine($"<{DateTime.Now}> - Bot Started");
            SendTweet("Hello World!");
            Console.Read();
        }
  {% endhighlight %}  
Ricordiamoci che twitter possiede delle strette regole antispam, quindi non ci sarà possibile inviare due tweet identici di fila (nemmeno dopo un giorno intero).  
Nel mio caso ho aggiunto un simpatico numero da 1 a 10000 alla fine della stringa, e Twitter sembra accettare (ad oggi!) il tweet giornaliero.  
Per concludere, avviate il progetto e il tweet sarà postato immediatamente.  
Provare per credere!  
Potete trovare l'intero progetto su [Github](https://github.com/Sgridev/KrTwitterBot/blob/master/Program.cs).  
Alla prossima!  

