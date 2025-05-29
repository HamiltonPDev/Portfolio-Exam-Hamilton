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
persoonsgegevens worden beschermd door alleen noodzakelijke data op te slaan. Wachtwoorden worden gehasht met bcrypt en sessies worden veilig beheerd via HttpOnly cookies in NextAuth.js. Geboeige gegevens zijn versleuteld opgeslagen in MongoDB. Alleen geautoriseerde gebruikers met de juiste rol krijgen toegang tot privacygevoelige informatie. Omgevingsvariabelen staan veilig in een .env-bestand buiten versiebeheer.

---

## Security
Authenticatie en autorisatie verlopen via NextAuth.js, waarbij wachtwoorden nooit in plain text worden opgeslagen. Rol-gebaseerde toegang en middleware zorgen ervoor dat alleen bevoegde gebruikers het CMS kunnen heberen. Alle communicatie veloopt via HTTPS. tRPC-endpoints zijn beveiligd met authorisatiechecks en gebruikersinput wordt gevalideerd om misbruik te voorkomen.

---

## Reflectie en verbeterpunten
Het ontwerp van EasyFWD is veilig, privacyvriendelijk en ethisch verantwoord. Een sterk punt is de duidelijke scheiding van verantwoordelijkheden en de type-safe communicatie via tRPC. In de toekomst zou ik nog meer willen investeren in automatische accessibility-tests, het verder beperken van dataretentie en het uitbreiden van de rechtenstructuur voor verschillende gebruikersrollen.