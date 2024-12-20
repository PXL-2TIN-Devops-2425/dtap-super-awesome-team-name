# a) Testserver

## 1. Docker Installeren op de Testserver
Docker is geïnstalleerd op de Testserver, waar Jenkins draait. Dit zorgt ervoor dat de server Docker-containers kan bouwen en draaien. De installatie werd uitgevoerd via de standaard Docker-installatiemethoden voor Ubuntu.
- `sudo apt-get install docker.io`

## 2. Toegang voor de Jenkins-gebruiker zonder sudo
Om ervoor te zorgen dat de **jenkins** gebruiker Docker-commando's kan uitvoeren zonder `sudo`, is de **jenkins** gebruiker toegevoegd aan de Docker-groep met het volgende commando:
- `sudo usermod -aG docker jenkins`
- `sudo usermod -aG docker "eigen gebruiker"`

Ook is de **ubuntu** gebruiker toegevoegd aan de Docker-groep zodat deze gebruiker Docker-commando's kan uitvoeren zonder `sudo`.  
Na het toevoegen van de gebruikers aan de Docker-groep is de Testserver herstart om de wijzigingen effectief te maken.

## 3. Rechten geven aan Jenkins voor specifieke mappen
De juiste rechten zijn toegewezen aan de **Jenkins-gebruiker** voor bepaalde mappen. Hiervoor zijn de commando's `chgrp` en `chmod` gebruikt om de benodigde toegang in te stellen:
- `chgrp`: Wijzigt de groepseigenaar van een bestand.
- `chmod`: Wijzigt de bestandspermissies zodat Jenkins de vereiste toegang heeft.

## 4. Node.js Configureren via Global Tool Configuration in Jenkins
In Jenkins is een nieuwe **Node.js-installatie** toegevoegd via de **Global Tool Configuration**. De versie van Node.js is ingesteld als **testenvnode**. Deze configuratie wordt gebruikt in de pipeline voor de **Install Dependencies** stage, waarin `npm install` wordt uitgevoerd om de benodigde dependencies van de applicatie te installeren.

## 5. Opstellen van de `test.jenkinsfile` Pipeline
De **`test.jenkinsfile`** bevat verschillende stages, waaronder:
- **Cleanup Stage**: Verwijdert alle bestanden in de werkruimte om te zorgen voor een schone start.
- **Clone Repository**: Haalt de laatste versie van de applicatiecode op van GitHub.
- **Install Dependencies**: Installeert de benodigde npm-pakketten via `npm install`.
- **Build Artifact**: Bouwt de Docker-image voor de applicatie.
- **Push Artifact**: Push de Docker-image naar DockerHub.
- **Deploy on Testserver**: Start de Docker-container op poort 3000 op de testserver, waarbij eventuele oude containers worden gestopt en verwijderd.

## 7. Testen van de Applicatie
Na de deployment kan de applicatie worden getest door te navigeren naar [http://localhost:3000](http://localhost:3000) op de **Testserver**, waar de applicatie beschikbaar is.

![testServer1](https://github.com/user-attachments/assets/962a9e73-d8a4-499a-9866-1d7b70e3f2b7)
![testServer2](https://github.com/user-attachments/assets/c25aef63-232d-4604-919b-de27f1ec596f)

# B) Productionserver
## ?. SSH-sleutels instellen voor Jenkins
Voor toegang tot de productieomgeving is een **SSH-sleutel** gegenereerd en toegevoegd aan de **Jenkins-gebruiker**. Dit stelt Jenkins in staat om via SSH in te loggen op de **Productie-server** zonder het gebruik van een wachtwoord, wat nodig is voor de productie deployment pipeline.
<img width="984" alt="ec2-user" src="https://github.com/user-attachments/assets/fb8e85e2-71f2-4d6e-90e0-f421b43f6955">
![productionServer](https://github.com/user-attachments/assets/c6177d26-c8a8-40e4-b7b9-31dcc38b194c)

De volgende comandos hebben we gebruikt om docker te instaleren op de productie server

sudo dnf install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
newgrp docker

