# Cloud Infrastructure 2018 - 

### Auteur: Ruben Bruggeman

## Mogelijkheden voor cloud datastoring


### Pure LAMP stacks

* Per applicatie dient dan in feite een LAMP stack opgebouwd te worden. D.w.z. dat er dus ook een database aan elke LAMP stack dient gekoppeld te worden. Is in ieder geval minder flexibel en minder robuust dan containers en een Kubernetes cluster. 
* **Nadelen**:
    * Huidige situatie: Digital Ocean servers -> hogere kostprijs bij high availability etc. ?
    * Wat als een stack down gaat ? Hoe wordt er gemonitord ? Moet de applicatie weer manueel gestart worden ?
    * Het uppen en scalen van applicaties verloopt hierdoor niet zo vlot -> weinig performantie.
    * De upsnelheid van een gewone stand-alone VM is **veel langer** dan de upsnelheid van een container in een COC bv. (Container Orchestration Cluster) .
    * Elke proces/applicatie draait op Guest OS -> Voor elke VM een apart OS-image -> neemt veel geheugen in beslag , opnieuw weinig performantie en weinig portabiliteit.
   

![container-vs-vms](https://user-images.githubusercontent.com/36444318/41443637-6cf82eb0-703e-11e8-8711-f3610097dfd1.jpg)

## Container Orchestration Tools

* **Swarm** - Nogal zwak en basic, goede omgeving om testapplicaties te draaien maar vaak te simpel en onbetrouwbaar om te gebruiken in een productieomgeving. Ondersteuning wordt evenens afgebouwd.

* **Amazon’s ECS** - enorm geëvolueerd sinds de initiele release, maar kan net zoals Swarm niet mee met grotere spelers als het op de productie omgeving aankomt. Eveneens niet cloud agnostic.

* **Nomad** - Onbetrouwdbaar en een te jong project voor de productieomgeving.

* **Kubernetes** - container orchestration met Kubernetes verloopt tot 10x sneller als met Mesos -> veel handiger in middelmatige tot grote productie omgevingen met veel containers / applicaties. Zeer toegankelijk voor samenwerking met o.a. Azure.

## Vervolg: mogelijkheden voor cloud datastoring

### Heroku

* Een cloud 'platform as a service' (PaaS) 
* Ondersteunt projecten in verschillende programmeertalen (Python, Ruby, Java, PHP, Go, ...)
* Handig om te linken aan GitHub repo -> bij een verandering wordt de huidige Heroku-image verwijderd en wordt een nieuwe aangemaakt met de laatste updates.
* **Nadeel:** Het is mogelijk om containers (zgn. dyno's) te [scalen](https://www.heroku.com/dynos/scaling) via het Heroku dashboard of de Heroku CLI, maar laat dus NIET toe om een 'eigen' COC te implementeren (Container Orchestration Cluster).
   

### Microsoft Azure + cluster

* Hoogstwaarschijnlijk de meest optimale keuze
* Gebruikmakend van een Kubernetes cluster:
    * **De cluster bestaat in feite uit Docker containers** -> Container platform 
      * Containers -> allemaal afzonderlijke processen -> **robuust, performant, isolatie & exporteerbaar** 
    * Microservices platform
    * Portable cloud platform
    * Deployment, scaling, load balancing, logging & monitoring
* Azure ondersteunt [API management](https://docs.microsoft.com/en-us/azure/api-management/)


* **Benodigdheden:**
    * (Voor custom deployments) **ACS-Engine** [(Azure Container Service Engine)](https://github.com/Azure/acs-engine) -> Provision en deploy container orchestrators op Azure 
    * **AKS** [(Azure Kubernetes Service)](https://azure.microsoft.com/en-us/services/kubernetes-service/) -> ondersteuning van de cluster 
        * 100-percent open-source Kubernetes
        * Continous Integration
        * Hoge security van Kubernetes cluster
        * ...
        * Zie [walktrough & alle gedetailleerde voordelen](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes)



## Mogelijkheden voor datapersistentie

* Uiteraard GEEN database per applicatie (Te duur? Neem te veel tijd in beslag? ...)
* Er dient gebruik gemaakt te worden van de voordelen van clustering.

### Eventueel een alternatieve oplossing (lokale datapersistentie in de cluster)

* Een vrij optimale oplossing zou zijn dat er maximaal 2 databases in een Kubernetes cluster opgenomen zouden worden -> 'specialisatie' m.b.t. de ontwikkeling van softwareprojecten tegengaan & 'generalisatie' aanmoedigen ( ~ zoveel mogelijk gebruik maken van dezelfde programmeertalen -> consistentie)    
    * **MongoDB** : Het standaard persistentietype om documenten op te slaan (bijvoorbeeld JSON-files)
    * **MySQL** : Opensource & gemakkelijkere ondersteuning voor allerlei programmeertalen + objectgeoriënteerd.

### Meest essentiële oplossing (online datapersistentie) 

* In zekere zin is dit performanter en veiliger.
* Gebruikmakend van volgende databases (eenvoudig om te koppelen aan het Azure platform) :
   * **DocumentDB / Cosmos DB** : online persistentie om documenten op te slaan (bijvoorbeeld JSON-files)
   * **SQL Database** : Entity Framework (automatische linking tussen mappers en code) -> zeer flexibel t.o.v. verschillende programmeertalen.



![kubernetescluster](https://user-images.githubusercontent.com/36444318/41456561-1f9c9ae6-7081-11e8-92a8-6063998b4146.png)





