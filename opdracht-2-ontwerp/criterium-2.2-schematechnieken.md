# Criterium 2.2 – Schematechnieken

## Inleiding

In deze sectie laat ik zien hoe ik verschillende schema's en diagrammen heb gebruikt om het ontwerp van de EasyFWD-website en het CMS te verduidelijken. Deze schema's helpen om de structuur, werking en datastromen van het systeem inzichtelijk te maken voor zowel ontwikkelaars als andere betrokkenen.

---

## Overzicht van gebruikte schema's

- **Use Case Diagram:** Laat zien welke gebruikers (bezoeker, bedrijfsklant, beheerder) welke acties kunnen uitvoeren op de EasyFWD-website en in het CMS.
- **Flowchart voor Authenticatie:** Laat zien het login- en sessieproces binnen Next.js met React-functionaliteiten zoals `useForm`, `cookies()`, `middleware` en redirects.
- **Class Diagram (UML):** Geeft de datastructuur van het systeem weer, met klassen als User, Page, Product en hun onderlinge relaties.
- **Sequence Diagram:** Toont het verloop van een belangrijke interactie, zoals het inloggen van een beheerder of het aanmaken van een nieuwe pagina via het CMS.
- **ERD (Entity Relationship Diagram):** Visualiseert de database-structuur, met entiteiten als User, Page, Product en de relaties daartussen (zoals foreign keys).
- **tRPC API-overzicht:** Schema van de belangrijkste tRPC-endpoints die gebruikt worden voor communicatie tussen frontend en backend, bijvoorbeeld voor authenticatie, pagina-beheer en image uploads.

---

## Use Case Diagram

![Use Case Diagram](./use-case-diagram.png)

**Toelichting:**
Het use case diagram geeft een overzicht van de belangrijkste gebruikers (actoren) en hun interacties met het systeem. Hiermee wordt in één oogopslag duidelijk welke functionaliteiten voor welke gebruikers beschikbaar zijn.

---

## Flowchart voor Authenticatie (aanvullend)

![Flowchart Auth](./uml-diagrammen/login-UML.png)

**Toelichting:**
Dit extra schema toont het login- en sessieproces binnen Next.js met React-functionaliteiten zoals `useForm`, `cookies()`, `middleware` en redirects. Het dient als visuele verduidelijking van de authenticatiestappen.

---

## Class Diagram (UML)

![Class Diagram](./class-diagram.png)

**Toelichting:**
Het class diagram laat de belangrijkste klassen en hun relaties zien, zoals User, Page, Product, etc. Dit geeft inzicht in de datastructuur en de koppelingen tussen verschillende onderdelen van het systeem.

---

## ERD (Entity Relationship Diagram)

![ERD](./erd.png)

**Toelichting:**
Het ERD geeft de structuur van de database weer, met tabellen (entiteiten) en de relaties daartussen. Dit is vooral belangrijk voor het backend- en datamodel.

---

## Sequence Diagram

![Sequence Diagram](./uml-diagrammen/sequence.png)

**Toelichting:**
Het sequence diagram toont het verloop van een belangrijke interactie, bijvoorbeeld het inloggen van een beheerder of het aanmaken van een nieuwe pagina. Hiermee wordt duidelijk hoe de verschillende onderdelen samenwerken tijdens een proces.

---

## API-overzicht of flowchart

![tRPC API Diagram](./uml-diagrammen/tRPC.webp)

**Toelichting:**
Het tRPC API-overzicht toont de belangrijkste backend-endpoints die via tRPC beschikbaar zijn voor de EasyFWD-website en het CMS. tRPC wordt gebruikt voor CRUD-operaties zoals het aanmaken, bewerken, verwijderen en ophalen van pagina's, producten, afbeeldingen én sections (informatieblokken binnen pagina's). Authenticatie (zoals login) verloopt via NextAuth en niet via tRPC. Dit schema maakt inzichtelijk hoe de frontend en backend type-safe communiceren voor content- en sectionbeheer, wat zorgt voor een robuust en onderhoudbaar systeem. 