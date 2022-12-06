# Portfolio S3
In dit portfolio licht ik mijn werk per leerdoel toe. Het gaat hierbij om zowel de IP-leerdoelen als GP-leerdoelen.


## Webapplicatie

**Front-end**

Voor de front-end word gebruik gemaakt van React. Aangezien React het meest gebruikte Javascript framework is en er veel ondersteuning en informatie over is te vinden.
Ik had voor dit semester nog geen kennis van React, maar wel van VueJS. Aangezien er veel gelijkenissen zijn, ben ik in React begonnen aan de hand van de [uitgebreide documentatie](https://reactjs.org/docs/getting-started.html).

**Back-end**

De back-end word geschreven in Java i.c.m. het Spring Boot framework om een REST-API te ontwikkelen. Dit omdat ik al ervaring heb met C# en graag een nieuwe taal wil leren.
Er is gekozen voor Spring Boot omdat het er voor zorgt dat je geen server nodig hebt, maar de applicatie lokaal kan draaien. Ook kan je de applicatie snel configureren. Daarnaast biedt het verschillende ORMs voor databases.

Om Java onder de knie te krijgen heb ik eerst een [cursus](https://www.codecademy.com/learn/learn-java) op CodeCademy gevolgd. Dit hielp om de verschillen tussen C# en Java te leren.

De applicatie die ik gemaakt heb is een platform / marktplaats voor mensen om klussen op te plaatsen.
Een ondernemer kan deze klus vervolgens inzien en ook oppakken om uit te voeren. Hierbij kan de ondernemer een prijs en datum aanbieden.
De gebruiker die een ondernemer zoekt om de klus uit te voeren, kan in zijn account zijn aangemaakte klussen inzien.

To do: **componentdiagram, code diagram en stukje over UI, API-documentatie aan de hand van Postman of Swagger.**

#### C4: context diagram
![img.png](images/C4%20Model%20System%20Context%20Diagram.png)

#### C4: container diagram
![img.png](images/C4%20Model%20Container%20Diagram.png)

[Front-end repository
](https://github.com/rubyfeller/s3-ip-frontend)

[Back-end repository
](https://github.com/rubyfeller/s3-ip-restapi)

**Database**

Voor de database is SQL gebruikt in combinatie met MySQL.
Dit omdat de database veel relaties zal gaan bevatten, en van tevoren bekend is welke data er in komt.
Daarnaast word gebruik gemaakt van de ORM Hibernate.

## Software quality
Voor het toepassen van Version Control heb ik gebruik gemaakt van GitHub.
Daarnaast word gebruik gemaakt van verschillende branches: een main/master branch en een development branch.
Zo kan er eerst een pull request gemaakt worden voordat de wijzigingen toegepast worden.

Voor het bewaken van de kwaliteit van de software heb ik gebruik gemaakt van SonarCloud. Deze tool maakt scans van de code, en laat op basis hiervan zien of er verbeteringen mogelijk zijn, of dat er bugs of kwetsbaarheden in de code zitten.

![img.png](images/SonarCloud%20GH%20Action.png)
![img.png](images/SonarCloud%20code%20scan%203.png)

To do: **toevoegen wat gedaan is met de code smells / security notices.**

To do: **stukje toevoegen over onderzoek naar veiligheid JWT-tokens**

Tot slot heb ik onderzoek gedaan naar hoe de kwaliteit in een gedistribueerde webapplicatie gewaarborgd kan worden middels testen.

[Onderzoek testen
](https://github.com/rubyfeller/s3-portfolio/blob/main/portfolio/research/Onderzoek%20testen.docx)

Aan de hand van dit onderzoek heb ik mijn applicatie getest. Aangezien het in een gedistribueerde webapplicatie belangrijk is dat diverse modules/onderdelen met elkaar kunnen communiceren, heb ik gekozen voor integratietests.
Om te valideren dat de applicatie voldoet aan de eisen heb ik tevens gebruik gemaakt van acceptatietests, in de vorm van endpoint-tests.

Deze tests heb ik toegepast met gebruik van Spring Boot Test, JUnit en TestContainers. TestContainers zorg voor een Docker image, met daarop de database.
Hiervoor heb ik gekozen omdat het mocken van de data minder waardevol is, en de daadwerkelijke database gebruiken de database onnodig vult. 
In de TestContainer wordt dezelfde versie van MySQL gedraaid als in de daadwerkelijke applicatie, zodat eventuele fouten met betrekking tot MySQL ook aan het licht komen.
In onderstaande afbeelding is 1 van de integratietests zichtbaar:

![img.png](images/IntegrationTestService.png)

Ik test hier of de assignment wordt toegevoegd, of de velden correct zijn, en of deze correct in de database komt.

In onderstaande afbeelding is een voorbeeld van een acceptatietest te zien. Hierbij word de controller getest, voornamelijk om te controleren of het resultaat en de HTTP statuscode uit het endpoint correct is:

![img.png](images/AcceptanceTestController.png)

## Agile
### Wat houdt Agile in?
Agile is een benadering voor het ontwikkelen van software. De focus ligt op het behalen van resultaten in iteraties van 1 tot 4 weken.
Het doel is om flexibel om te gaan met feedback: iedere iteratie kunnen klanten hun eisen aanpassen. Dit zorgt ervoor dat de feedback van de klant direct wordt meegenomen in de Systems Development Life Cycle (SDLC).

### Agile Manifesto

Het Agile Manifesto is een reeks van principes voor het ontwikkelen van software. Het manifest is opgesteld door een groep softwareontwikkelaars. Het manifest heeft 4 kernwaarden:
- Personen en interacties zijn belangrijker dan processen en tools

Dit principe betekend dat de focus is op de leden van het team in plaats van op tools en documentatie. Dit komt o.a. terug in de retrospective en planning.


- Werkende software is belangrijker dan uitgebreide documentatie

In plaats van een uitgebreide analyse, moet de focus op het product liggen. Er word uiteraard nog steeds documentatie geschreven, echter alleen het minimum dat nodig is voor de ontwikkeling van het product.


- Actieve rol voor de klant is beter dan het uitonderhandelen van een contract

Dit principe is opgesteld omdat klanten er vaak tijdens de ontwikkeling pas achter komen wat ze daadwerkelijk willen.
De flexibiliteit en continue feedback zorgt er voor dat het eindproduct beter is, en niet teleurstellend is op basis van een vooraf opgestelde omschrijving.

- Reageren op verandering is beter dan het volgen van een vooraf bedacht plan.

Dit principe geeft aan dat iets nooit perfect is en het product continue verbeterd word op basis van feedback in de opleveringen.


Bronnen:

Agile Manifesto: https://agilemanifesto.org/

Codeproject: https://www.codeproject.com/Articles/704720/Scrum-explained

In de proftaak is gebruik gemaakt van de agile ontwikkelmethode Scrum. Hier hebben we voor gekozen vanwege de flexibiliteit in de ontwikkeling en betrokkenheid van de klant. We zijn ervan overtuigd dat dit zorgt voor een beter eindproduct, omdat de klant goed op de hoogte is en feedback of nieuwe inzichten kan delen.

Hierbij hebben we als groep daily standups en planningmeetings gehouden, 5 sprint opleveringen gehad en een aantal refinement sessies met de product owners gehad. Hierbij is gebruik gemaakt van Azure DevOps om de voorgang bij te houden en te communiceren.
Ook is er een burndownchart gemaakt.

Voor de retrospective hebben we gebruik gemaakt van de [4ls](https://www.atlassian.com/team-playbook/plays/4-ls-retrospective-technique) methode:

![img.png](images/Retrospective%20GP.png)

Op basis van deze methode konden we direct zien wat er goed ging, wat we hebben geleerd, wat we miste, en wat we de volgende keer beter kunnen doen.

### Andere agile ontwikkelmethodes
Andere agile ontwikkelmethodes zijn onder andere kanban, extreme programming en lean development. Bij kanban ligt de focus op efficiency en op het verminderen van de duur van een project.
Er zijn hierbij geen vastgezette sprints, maar het werk word continu voorgezet. Ook zijn er geen rollen als product owners en scrum masters of vaste meetings (daily standups, refinements etc).

Extreme programming (XP), lijkt meer op SCRUM. Er word hierbij wel gekozen voor kortere iteraties van tussen de 1 en 3 weken.
Er word gekeken wat in de iteratie mogelijk is en iedere ontwikkelaar geeft aan wat hij kan doen. De klant prioriteert de user stories.
Daarnaast gaan de ontwikkelaars pair-programmeren, ook worden er iedere iteratie tests geschreven voordat de code op productie gaat.

Tot slot een vergelijking met lean development. Hier geldt, net zoals bij kanban, dat er geen vaste iteraties/sprints worden afgesproken.
Er word dus continu doorontwikkeld. De lean methode komt voort uit de industriewereld, met als doel om processen binnen een bedrijf efficiënter te maken. Dit is dus anders dan bij Scrum, welke alleen ingezet word in kleine teams.

### Andere ontwikkelmethodes
De meest bekende alternatieve ontwikkelmethode voor agile is waterval.
De watervalmethode is een linear proces waarin van tevoren alle requirements worden opgesteld. Het volgt de Software Development Life Cycle (SDLC).
Vaak is er in deze methode ook sprake van een contract welke van tevoren getekend word en niet meer gewijzigd kan worden.

In onderstaande afbeelding is te zien hoe de SDLC in de waterval-methode eruit ziet:

![img.png](images/Software%20Development%20Life%20Cycle.png)

Iedere stap die is weergegeven: analyse, design, implementatie, testen en evaluatie worden los van elkaar uitgevoerd. De volgende stap kan niet starten voordat de voorgaande afgerond en gereviewd is.
Er word dus bijvoorbeeld niet zoals bij Scrum iedere sprint getest, maar pas als alle voorgaande processen zijn afgerond (analyse tot en met implementatie).

Dit ontwikkelproces word voornamelijk gebruikt als er weinig veranderingen verwacht worden.

Bronnen: 

Coscreen: https://www.coscreen.co/blog/extreme-programming-vs-scrum-difference/

Atlassian: https://www.atlassian.com/agile/kanban/kanban-vs-scrum

Visual Paradigm: https://www.visual-paradigm.com/scrum/scrum-vs-waterfall-vs-agile-vs-lean-vs-kanban/

Azure DevOps (Scrum)board:

![img.png](images/AzureDevOpsBoard.png)

To do: **toelichting DoD, kleine taken etc.**

To do: **Insert screenshot burndown chart**

## CI/CD
Aan de repositories op GitHub heb ik 'Github Actions' toegevoegd: een tool om CI/CD toe te passen.
De CI/CD workflow zorgt er als eerst voor dat er een build van de applicatie gemaakt word. Daarnaast worden alle testen uitgevoerd.
Op basis van het resultaat van de eerste actie, word een Docker image aangemaakt. In de laatste stap word deze image gepushet naar GitHub Packages, welke gekoppeld is aan de correcte repository.

Daarnaast word SonarCloud getriggered om een code scan te maken. Op basis hiervan kan de code verbeterd worden.

[GitHub workflow front-end
](https://github.com/rubyfeller/s3-ip-frontend/blob/main/.github/workflows/node.js.yml)

[GitHub workflow back-end
](https://github.com/rubyfeller/s3-ip-restapi/blob/master/.github/workflows/maven.yml)

[Dockerfile front-end
](https://github.com/rubyfeller/s3-ip-frontend/blob/main/Dockerfile)

[Dockerfile back-end
](https://github.com/rubyfeller/s3-ip-restapi/blob/master/Dockerfile)

[GitHub Package front-end
](https://github.com/rubyfeller/s3-ip-frontend/pkgs/container/s3-ip-frontend)

[GitHub Package back-end
](https://github.com/rubyfeller/s3-ip-restapi)

In het groepsproject heb ik gebruik gemaakt van Azure Pipelines, waar een Docker image gemaakt en gepushet word naar AWS ECR. Vanuit daar word een ECS instance aangemaakt, welke ervoor zorgt dat de applicatie draait op een EC2 server.
In onderstaande afbeelding is de architectuurdiagram van het groepsproject te zien, met daarin het CI/CD proces:

![img.jpg](images/Architectuurdiagram%20GP.jpg)

## Cultural differences and ethics
Ik heb gekeken naar mijn interculturele competentie door een assessment van IDI (Intercultural Development Inventory) te maken.
Ook heb ik gekeken naar de uitkomsten hiervan middels een debriefing en quiz. 

Uit de assessment kwam naar voren dat ik mijn vaardigheden met betrekking tot het aanpassen en begrijpen van culturele verschillen erg heb overschat.

In onderstaande afbeelding is de score te zien, welke ik mezelf gegeven heb (perceived):

![img.png](images/IDIPerceivedScore.png)

Deze score valt binnen het oriëntatieprofiel 'minimization': dit weerspiegelt een tendens om de nadruk te leggen op overeenkomsten tussen culturen, maar belangrijke verschillen in waarden, waarneming en gedrag over het hoofd kan zien.

In onderstaande afbeelding is mijn werkelijke score (developmental) te zien: 

![img.png](images/IDIDevelopmentalScore.png)

Deze score geeft aan dat ik te kritisch ben op mijn eigen cultuur (Reversal), en ik minder kritisch ben op andere culturen.
Hier kan ik mijzelf in herkennen, aangezien ik mijn eigen cultuur uiteraard het best ken en hier dus ook de nadelen van zie. Deze blijk ik echter teveel uit te vergroten.

In onderstaande afbeelding zijn de positieve kanten van het profiel polarisatie te zien, en de kansen die er nog liggen:

![img.png](IDIPolarization.png)

Ik ben van plan om meer te kijken naar overeenkomsten tussen mijn eigen cultuur en andere culturen, en om niet te kritisch te zijn op mijn eigen cultuur.
Ook hoop ik hiermee in te zien dat iedere cultuur een mix van positieve en negatieve kanten heeft.

To do: **analyse / omschrijving over ethiek van de applicatie**

## Requirements and design
Voor het opstellen van requirements heb ik gebruik gemaakt van user stories in combinatie met acceptatiecriteria / definition of done.
Deze zijn per sprint bijgehouden in Jira:

![img.png](images/Jira%20board%202.png)

## Business processes

## Professional

To do: **Insert FeedPulse screenshot / export**

In het groepsproject hebben we elkaar aan het einde van de sprint peer feedback gegeven:

![img.png](images/Peer%20feedback.png)

To do: **reflecteren op proces en verschillen tussen GP en IP (scrum etc).**

## Reflectie
To do: **reflectie op dit semester.**