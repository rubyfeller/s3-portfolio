# Onderzoek security
### Op welke plek kun je in een gedistribueerde webapplicatie het veiligst JWT-tokens opslaan?

#### Waarom dit onderzoek?
Ik doe dit onderzoek om de veiligheid van mijn applicatie te waarborgen, en dit aan te kunnen tonen.

#### Onderzoeksmethode
Voor dit onderzoek maak ik gebruik van het DOT-framework. Dit is een gestandaardiseerd research-framework, wat voor kwalitatief onderzoek zorgt.
Onderstaande strategieën binnen het DOT-framework zullen worden toegepast:

**Library**

Literature study

Best good and bad practices

![img.png](images/Library.png)

Ik kies voor de library-methode in combinatie met de strategie 'Literature study' om onderzoek te doen naar al bestaande richtlijnen en theorieën.
Dit gezien er een grote hoeveelheid informatie beschikbaar is over het onderzoeksonderwerp. Ook gebruik ik de strategie 'Best good and bad practices', zodat onderzocht kan worden wat goede en minder goede implementaties zijn.

**Lab** 

Security test

![img.png](images/Lab.png)

Omdat de security van de applicatie van groot belang is, is het belangrijk om de risico's van verschillende oplossingen voor de onderzoeksvraag in kaart te brengen. Om dit te bereiken gebruik ik de methode 'Lab' met de strategie 'Security test'. 

# Deelvragen

### Wat is een JWT?

Een JSON Web Token (JWT) is een token die versleutelde JSON-data bevat. Het zorgt voor een manier om JSON-data op een veilige manier te versturen.
Ze worden gebruikt voor authenticatie en authorisatie van gebruikers. (auth0.com, z.d.)

Een JWT bestaat uit:

- Header

Hierin word het type key omschreven (JWT) en het hashing algoritme, zoals RSA. (auth0.com, z.d.)

- Payload

Hierin staan waardes zoals permissies en rollen omschreven. De namen van de claims mogen maximaal 3 karakters bevatten om de JWT compact te houden. (auth0.com, z.d.)

- Signature

De JWT word ondertekend om te bevestigen dat de persoon is wie hij zegt dat hij is, en om te bevestigen of de inhoud niet aangepast is. (auth0.com, z.d.)

In onderstaande afbeelding is een JWT uit mijn applicatie zichtbaar. De rode kleur bevat de header, de paarse kleur de payload en de blauwe kleur de signature. (auth0.com, z.d.)

![img.png](../images/JWT-Token.png)

### Wat zijn de mogelijke aanvalsmogelijkheden?
**Access token wordt gestolen**

Wanneer de gebruiker zijn JWT aan iemand anders doorgeeft, kan diegene verzoeken doen namens de daadwerkelijke persoon.

**CSRF-aanvallen**

Een CSRF aanval is een aanval waarbij een ingelogde gebruiker, zonder dat deze het weet, ongewenste requests uitvoert.
Een voorbeeld hiervan is het verwijderen van een post: op het moment dat er via bijvoorbeeld social engineering een link gestuurd zou worden welke deze request uitvoert, word de post verwijderd zonder dat de gebruiker het weet. (Cross Site Request Forgery (CSRF) | OWASP Foundation, z.d.)

**XSS-aanvallen**

XSS (cross-site-scripting) attacks vinden plaats wanneer er onjuiste data verzonden word, en deze alsnog uitgevoerd word. (Cross Site Scripting (XSS) | OWASP Foundation, z.d.)

Deze data kan verzonden worden via bijvoorbeeld een formulier:

````
<SCRIPT type="text/javascript">
var adr = '../evil.php?cakemonster=' + escape(document.cookie);
</SCRIPT>
`````

Wanneer deze data niet gevalideerd zou worden, zou de cookie van een andere gebruiker gebruikt kunnen worden. (Cross Site Scripting (XSS) | OWASP Foundation, z.d.)

### Is mijn applicatie kwetsbaar voor een van de aanvallen?
- CSRF

De applicatie is niet kwetsbaar voor CSRF-aanvallen. Dit omdat de API middels [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) alleen verzoeken toestaat vanuit betrouwbare bronnen. Op dit moment mag alleen het IP-adres van de front-end request naar de API maken.
Dit betekend dat een andere applicatie geen requests naar de API kan maken. Daarnaast is er geen gebruik gemaakt van cookies voor de API-requests.

- XSS

React heeft enkele features ingebouwd welke XSS kunnen voorkomen. (Cooper Codes, 2022).

- String variabelen worden automatisch ge-escaped. (Cooper Codes, 2022)

```<script>alert("Hack")</script>``` word bijvoorbeeld ```"<script>alert("Hack")</script>"```: het wordt dus een stuk tekst in plaats van code, wat het onuitvoerbaar en dus ongevaarlijk maakt.


- Bij het dynamisch inladen van tekst word de code ook ge-escaped. In het geval dat ```<h1>Kop</h1>``` ingeladen zou worden, zou dit letterlijk zo geprint worden.
Om dit te voorkomen is het in React mogelijk om de prop ```dangerouslySetInnerHTML``` te gebruiken. Zoals de naam al zegt, is deze echter wel kwetsbaar.
De kwetsbaarheid kan gedicht worden door de data te 'sanitizen', hiervoor kunnen packages als DOMPurify gebruikt worden (React XSS Guide: Examples and Prevention, n.d.):
"DOMPurify sanitizes HTML and prevents XSS attacks. You can feed DOMPurify with string full of dirty HTML and it will return a string (unless configured otherwise) with clean HTML. DOMPurify will strip out everything that contains dangerous HTML and thereby prevent XSS attacks and other nastiness. It's also damn bloody fast. We use the technologies the browser provides and turn them into an XSS filter. The faster your browser, the faster DOMPurify will be." (DOMPurify, n.d.)

In de front-end van de applicatie heb ik geen mogelijkheid kunnen vinden voor het uitvoeren van een XSS-aanval, ook gebruik ik geen ```dangerouslySetInnerHTML```.

### Waar kan de JWT het veiligst opgeslagen worden?
De JWT wordt doorgaans opgeslagen in de localstorage, in een cookie of in session storage (Wikipedia contributors, 2022) : allemaal client-side. 
Om de afweging te maken waar de token op te slaan speelt ook de balans tussen user experience en veiligheid een rol. Zo kan de token in de session storage worden opgeslagen, echter dient de gebruiker dan bij ieder bezoek van de applicatie opnieuw in te loggen (Koniaris, 2020).

Zowel bij het opslaan in de localstorage, in-memory of in de cookies is de JWT op te halen gezien deze hoe dan ook op de client-side staat.
Dit is echter niet direct een probleem als de applicatie beveiligd is tegen XSS en CSRF aanvallen. Wanneer de applicatie hier niet tegen beschermd is, ontstaan er wel problemen. Deze problemen beperken zich echter niet alleen tot de JWT, maar betreffen de gehele applicatie.

### Conclusie
Aangezien het op de client-side altijd mogelijk is om bij de JWTs te komen, kies ik ervoor om ze in de localstorage te zetten. Dit is de meest gebruiksvriendelijke manier, en ook op de andere locaties zijn er risico's.
Het blijft wel belangrijk om in de localstorage geen kwetsbare data als wachtwoorden op te slaan. Daarnaast kan er, mocht het mis gaan, slechts voor beperkte tijd misbruik gemaakt worden van de JWT aangezien deze slechts 1 minuut geldig is. Tot slot dient de applicatie in zijn geheel beveiligd te zijn tegen XSS en CSRF aanvallen.

**Bronnen**

(auth0.com, z.d.) https://auth0.com/learn/json-web-tokens

Cross Site Scripting (XSS) | OWASP Foundation. (z.d.). https://owasp.org/www-community/attacks/xss/

Cross Site Request Forgery (CSRF) | OWASP Foundation. (z.d.). https://owasp.org/www-community/attacks/csrf

Cooper Codes. (2022, April 13). Preventing XSS Attacks in React [Video]. YouTube. https://www.youtube.com/watch?v=UMeAP3ySpsE

React XSS Guide: Examples and Prevention. (n.d.). StackHawk. https://www.stackhawk.com/blog/react-xss-guide-examples-and-prevention/

DOMPurify. (n.d.). GitHub. https://github.com/cure53/DOMPurify

Wikipedia contributors. (2022, December 25). JSON Web Token. Wikipedia. https://en.wikipedia.org/wiki/JSON_Web_Token

Koniaris, G. (2020, July 11). How to securely store JWT tokens. DEV Community 👩‍💻👨‍💻. https://dev.to/gkoniaris/how-to-securely-store-jwt-tokens-51cf