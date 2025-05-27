# Criterium 2.3 – Onderbouwing

## Inleiding
In deze sectie licht ik mijn ontwerpkeuzes toe en geef ik aan hoe ik rekening heb gehouden met ethiek, privacy en security binnen het EasyFWD-project.

---

## Relatie ontwerp met eisen en wensen
Het ontwerp van EasyFWD is gebaseerd op de user stories die zijn opgesteld in overleg met de opdrachtgever. Zo is er gekozen voor een duidelijke scheiding tussen beheerders en bezoekers, en is het CMS zo ingericht dat alleen bevoegde gebruikers content kunnen aanpassen. De datastructuur (zie class diagram en ERD) en API's (zie tRPC API-overzicht) zijn afgestemd op de behoefte om snel en veilig content te kunnen beheren. Voor elke functionaliteit is gekeken naar de wensen van de eindgebruiker, zoals eenvoudig pagina's kunnen aanmaken, producten beheren en afbeeldingen uploaden.

---

## Ethiek
Bij het ontwerp is rekening gehouden met toegankelijkheid: de website is bruikbaar op verschillende apparaten (responsive design) en voor mensen met een beperking (o.a. door het gebruik van semantische HTML en voldoende contrast). Transparantie is belangrijk: gebruikers kunnen altijd zien welke gegevens over hen worden opgeslagen en waarvoor deze worden gebruikt. Er wordt geen misleidende informatie getoond en alle gebruikers krijgen eerlijke toegang tot de functionaliteiten van het systeem.

---

## Privacy
Privacy is gewaarborgd door alleen noodzakelijke persoonsgegevens op te slaan. Gevoelige data wordt versleuteld opgeslagen in de database. Gebruikers kunnen hun gegevens op verzoek laten verwijderen (recht op vergetelheid). Er wordt geen onnodige tracking of profiling toegepast. Alleen geautoriseerde beheerders hebben toegang tot privacygevoelige informatie in het CMS.

---

## Security
Voor de beveiliging is gekozen voor NextAuth voor authenticatie, zodat wachtwoorden nooit in plain text worden opgeslagen. Alle tRPC-endpoints zijn beveiligd met authorisatiechecks, zodat alleen bevoegde gebruikers data kunnen aanpassen. Input van gebruikers wordt gevalideerd om SQL-injectie en XSS-aanvallen te voorkomen. Regelmatige updates en dependency checks zorgen ervoor dat bekende kwetsbaarheden snel worden verholpen. Daarnaast worden gevoelige API-routes afgeschermd via middleware.

---

## Reflectie en verbeterpunten
Het ontwerp van EasyFWD is veilig, privacyvriendelijk en ethisch verantwoord. Een sterk punt is de duidelijke scheiding van verantwoordelijkheden en de type-safe communicatie via tRPC. In de toekomst zou ik nog meer willen investeren in automatische accessibility-tests, het verder beperken van dataretentie en het uitbreiden van de rechtenstructuur voor verschillende gebruikersrollen. 