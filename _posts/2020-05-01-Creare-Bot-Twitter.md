---
layout: post
title: "Come creare un bot di Twitter in C#"
date: 2020-05-01
excerpt: "Utilizzare le API Twitter per creare un bot"
tags: [Twitter, Twitter Bot, Bot, Andrea Grisafi, .NET, C#]
feature: https://media.wired.com/photos/5a55b72db1cfb87f3206aa5b/master/w_582,c_limit/Twitter-Hole-featured.jpg
comments: false
---
Ogni giorno, tutti noi ripetiamo le stesse azioni quasi in modo automatico: si pensi ad esempio quando ci si lava i denti, la faccia o si mangia.
Ciò che ci sfugge è tutto il tempo perso nel farlo.  
Lavandoci i denti per 5 minuti al giorno, alla fine dell'anno avremmo perso più di 30 ore del nostro tempo.  
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

