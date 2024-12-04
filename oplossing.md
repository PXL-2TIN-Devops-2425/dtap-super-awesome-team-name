Vul onderstaande aan met de antwoorden op de vragen uit de readme.md file. Wil je de oplossingen file van opmaak voorzien? Gebruik dan [deze link](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) om informatie te krijgen over
opmaak met Markdown.

a)
1. Toevoegen van gebruikers aan de Docker-groep
We zorgen ervoor dat de gebruikers jenkins en Ubuntu Docker commando's kunnen uitvoeren zonder sudo.
Commando's: usermod -aG docker jenkins, usermod -aG docker "eigen gebruiker"
Na het toevoegen van de gebruikers aan de groep is er een herstart van de vm nodig.
2. Rechten geven aan Jenkins voor specifieke mappen
Onze rechten hebben we aangepast met de commando's: chgrp en chomd
3. SSh-sleutels instellen voor Jenkins
Voor toegang tot de productieomgeving hebben we een SSH-sleutel gegenereerd en toegevoegd aan de Jenkins-gebruiker.
4. Node.js configuratie via Global Tool Configuration
In Jenkins hebben we een nieuwe Node.js-installatie toegevoegd.
Ook gebruiken we in onze pipeline bij de install dependencies de configuratie.

b)
