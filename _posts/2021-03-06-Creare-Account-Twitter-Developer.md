---
layout: post
title: "Come creare un bot di Twitter in C#"
date: 2020-03-06
excerpt: "Come utilizzare le API Twitter per creare un bot"
tags: [Twitter, Twitter Developer, Account Developer Twitter, Andrea Grisafi]
feature: https://media.wired.com/photos/5a55b72db1cfb87f3206aa5b/master/w_582,c_limit/Twitter-Hole-featured.jpg
comments: false
---

Spesso, sostituire le nostre azioni manuali con dei bot automatizzati può risultarci molto utile per risparmiare tempo e fatica.   
Ad esempio, una mattinata estiva del 2019, decisi di voler trovare un modo per ricordare ogni giorno alla mia ragazza quanto fosse bella.  
E quale miglior idea se non un [bot di Twitter](https://twitter.com/sarabellxmbot)? /s  
Quindi, buttiamoci subito all'azione!

# 1) Ottenere un account Twitter developer
![_config.yml]({{ site.baseurl }}/assets/img/twitterpost/twitter1.png)  
Per prima cosa dobbiamo richiedere ed ottenere un account Twitter Developer per poter comunicare con l'[API](https://en.wikipedia.org/wiki/Application_programming_interface) di Twitter.  
Per andare direttamente alla pagina di richiesta segui questo [link](https://developer.twitter.com/en/apply-for-access).  
Dopo aver completato l'applicazione ed aver ottenuto l'accesso, ci ritroveremo davanti questa [dashboard](https://developer.twitter.com/en/apps):
![_config.yml]({{ site.baseurl }}/assets/img/twitterpost/twitter2.png)
Completiamo i campi richiesti nel seguente modo  
  