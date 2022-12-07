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

De applicatie die ik gemaakt heb, is een platform / marktplaats voor mensen om klussen op te plaatsen.
Een ondernemer kan deze klus vervolgens inzien en ook oppakken om uit te voeren. Hierbij kan de ondernemer een prijs en datum aanbieden.
De gebruiker die een ondernemer zoekt om de klus uit te voeren, kan in zijn account zijn aangemaakte klussen inzien.

To do: **meerdere actors toevoegen, componentdiagram, code diagram en stukje over UI, front-end testen, API-documentatie aan de hand van Postman of Swagger.**

#### C4: context diagram
![img.png](images/C4ModelSystemContextDiagram2.png)

Uit feedback bleek dat de API (grijs blok), niet gezien kan worden als extern systeem omdat het bij de applicatie hoort. Dit maakt de contextdiagram minder relevant. Ik heb hem toch laten staan omdat ik er wel wat van geleerd heb. 

#### C4: container diagram
![img.png](images/C4ModelContainerDiagram2.png)

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

In onderstaande afbeelding is een van de code smells te zien:

![img.png](images/SonarCodeSmell.png)

Ook staat er een toelichting bij over waarom dit een probleem is: "When verifying that code raises a runtime exception, a good practice is to avoid having multiple method calls inside the tested code, to be explicit about which method call is expected to raise the exception.

It increases the clarity of the test, and avoid incorrect testing when another method is actually raising the exception."

Hierom heb ik de code aangepast zodat er maar 1 exception op 1 method call mogelijk is.

Ook hadden veel code smells te maken met code die in minder regels geschreven kon worden, ook dit heb ik toegepast. Daarnaast hadden de meeste code smells betrekking op code die uitgecomment is.
Aangezien ik gebruik maak van versiebeheer heb ik besloten om geen stukken code gecomment in mijn code te laten staan.

Tot slot waren er ook enkele code smells waar ik niets mee gedaan heb. Zo gebruik ik af en toe dezelfde tekst in een exception test. Aangezien het hier om tests gaat, waar alle tests in principe los van elkaar moeten staan, heb ik besloten hier niets mee te doen.

****Security notices****

Gedurende het ontwikkelen van de applicatie zijn ook security notices naar boven gekomen:

![img.png](images/SonarCloudSecurityNotice.png)

Zoals in de afbeelding is te zien, word op dit moment ieder soort HTTP-request naar de applicatie toegestaan. Dit is niet veilig en dient aangepast te worden wanneer de applicatie naar productie gaat. SonarCloud zorgt er voor dat je dit niet vergeet.


To do: **stukje toevoegen over onderzoek naar veiligheid JWT-tokens**

#### Onderzoek 1
Tot slot heb ik onderzoek gedaan naar hoe de kwaliteit in een gedistribueerde webapplicatie gewaarborgd kan worden middels testen. Hiervoor heb ik gebruik gemaakt van het [DOT-framework](https://ictresearchmethods.nl/The_DOT_Framework).

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

Het Agile Manifesto is een reeks van principes voor het ontwikkelen van software. Het manifest is opgesteld door een groep softwareontwikkelaars. Het manifest kent 4 kernwaarden:
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


**Azure DevOps (Scrum)board:**

![img.png](images/AzureDevOpsBoard.png)

In Azure Devops hebben we de sprints gepland, user stories en taken toegevoegd. Daarnaast gebruiken we op advisering van de product owners de geïntegreerde Git functionaliteit voor onze repo's. Ook gebruiken we de DevOps Pipelines voor onze CI/CD. 

Bij de eerste sprints van het project kwamen we er achter dat de taken te algemeen beschreven werden. Ook werkte er meerdere mensen aan 1 taak. Uiteindelijk hebben we dit veranderd door kleinere taken te maken, zodat ieder lid een taak kan oppakken.
Ook hebben we de taken beter geformuleerd en op advies van de productowners een Definition of Done toegevoegd, zodat er geen discussie kan ontstaan over wanneer een taak af is:

![img.png](images/DevOpsTaskDoD.png)

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

### Wat is cultuur?
Cultuur omschrijft de gewoontes, normen en waarden van een samenleving. Het kan verschillende groepen mensen van elkaar onderscheiden, en word overgedragen van generatie op generatie.

Ik heb gekeken naar mijn interculturele competenties door een assessment van IDI (Intercultural Development Inventory) te maken.
Ook heb ik gekeken naar de uitkomsten hiervan middels een debriefing en quiz. 

Uit het assessment kwam naar voren dat ik mijn vaardigheden met betrekking tot het aanpassen en begrijpen van culturele verschillen erg heb overschat.

In onderstaande afbeelding is de score te zien waarop ik mezelf had ingeschat (perceived):

![img.png](images/IDIPerceivedScore.png)

Deze score valt binnen het oriëntatieprofiel 'minimization': dit weerspiegelt een tendens om de nadruk te leggen op overeenkomsten tussen culturen, maar waarbij belangrijke verschillen in waarden, waarneming en gedrag over het hoofd gezien kunnen worden.

In onderstaande afbeelding is mijn werkelijke score (developmental) te zien: 

![img.png](images/IDIDevelopmentalScore.png)

Deze score geeft aan dat ik te kritisch ben op mijn eigen cultuur (Reversal), en ik minder kritisch ben op andere culturen.
Hier kan ik mijzelf in herkennen, aangezien ik mijn eigen cultuur uiteraard het best ken en hier dus ook de nadelen van zie. Deze blijk ik echter teveel uit te vergroten.

In onderstaande afbeelding zijn de positieve kanten van het profiel polarisatie te zien, en de kansen die er nog liggen:

![img.png](images/IDIPolarization.png)

Ik ben van plan om meer te kijken naar overeenkomsten tussen mijn eigen cultuur en andere culturen, en om niet te kritisch te zijn op mijn eigen cultuur.
Ook hoop ik hiermee in te gaan zien dat iedere cultuur een mix van positieve en negatieve kanten heeft.

### In kaart brengen van culturele verschillen
Om culturele verschillen tussen landen in kaart te brengen, heb ik gekeken naar het cultuurmodel van Geert Hofstede.
Dit cultuurmodel laat de verschillen tussen landen en culturen zien aan de hand van 6 dimensies. Dit maakt het mogelijk om de culturen te vergelijken.

Onderstaand de belangrijkste dimensies:
- Machtsafstand

Geeft aan in hoeverre hiërarchie een belangrijke rol speelt in een land. Nederland scoort erg laag op deze dimensie. Dit betekend dat leidinggevenden bijvoorbeeld toeganlijk zijn en informeel aangesproken kunnen worden. De communicatie is direct.
In andere landen zoals Maleisië is de werkcultuur veel hiërarchischer: mensen verwachten dat hen verteld word wat ze moeten doen, en het doel is om een baan te krijgen waarin ze zelf kunnen bepalen wat anderen moeten doen.

- Individualisme

Geeft aan hoe individualistisch of hoe collectivistisch een land is. Nederland scoort hier erg hoog: men zorgt vooral voor zichzelf en directe familie. Daarnaast worden bijvoorbeeld promoties alleen gegeven op basis van resultaten.
Aziatische culturen zijn collectivistischer: de communicatie is indirect en men vermijdt conflicten. De prioriteit in (zakelijke)relaties ligt niet op taken maar op moraliteit.

- Masculiniteit

Deze dimensie geeft aan in hoeverre er waarde gehecht word aan mannelijke en vrouwelijke kwaliteiten. Landen als Nederland worden als feminiem bestempeld omdat de rolverdeling tussen man en vrouw overlapt. 
In landen als Japan is een duidelijke rolverdeling tussen de man en vrouw.

- Onzekerheidsvermijding

Geeft aan hoe een samenleving omgaat met onzekerheid. Sommige culturen willen zoveel mogelijk onzekerheid vermijden, door bijvoorbeeld het gebruik van rituelen. Ook is geloof er sterker.
Nederland scoort gemiddeld. Mensen hebben wel een lichte voorkeur voor het vermijden van onzekerheid. Dit houdt in dat men zich graag aan regels houd en punctualiteit belangrijk is. Ook is veiligheid erg belangrijk.

Bronnen:

Hofstede Insights: https://www.hofstede-insights.com/country-comparison/the-netherlands/

Wikipedia: https://nl.wikipedia.org/wiki/Geert_Hofstede

Clearly Cultural: https://clearlycultural.com/geert-hofstede-cultural-dimensions/

To do: **analyse / omschrijving over ethiek van de applicatie**

### Ethiek


## Requirements and design
Voor het opstellen van requirements heb ik gebruik gemaakt van user stories in combinatie met acceptatiecriteria / definition of done.
Deze zijn per sprint bijgehouden in Jira:

![img.png](images/Jira%20board%202.png)

In het individuele project is geen gebruik gemaakt van Scrum, aangezien ik niet werkte in een team en ook geen productowners had.
Voor het groepsproject is wel gebruik gemaakt van Scrum: zie [Agile](https://github.com/rubyfeller/s3-portfolio/blob/main/portfolio/portfolio.md#agile).

Zie voor de architectuur van het IP [Webapplicatie](https://github.com/rubyfeller/s3-portfolio/blob/main/portfolio/portfolio.md#c4-context-diagram), en zie voor een architectuurtekening van het GP [CI/CD](https://github.com/rubyfeller/s3-portfolio/blob/main/portfolio/portfolio.md#cicd).

## Business processes

## Professional

To do: **Insert FeedPulse screenshot / export**

In het groepsproject hebben we elkaar aan het einde van de sprint peer feedback gegeven:

![img.png](images/Peer%20feedback.png)

Ook heb ik onderzoeken geschreven met gebruik van het DOT-framework, zie [Software Quality](https://github.com/rubyfeller/s3-portfolio/blob/main/portfolio/portfolio.md#software-quality).

To do: **reflecteren op proces en verschillen tussen GP en IP (scrum etc).**

## Reflectie
To do: **reflectie op dit semester.**