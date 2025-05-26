# Project Introductie

**Naam opdrachtgever:** 4U Solutions 
**Projectmanager:** Ties Noordhuis
**Teamleden Development:** Hamilton Posada Serna
**Projectnaam:** Ontwikkeling van een nieuwe website en maatwerk CMS voor 4U Solutions BV

---

## Introductie
4U Solutions is een Nederlands bedrijf gespecialiseerd in kantoor- en industriële ergonomie. Hun missie is het bevorderen van fysieke en mentale fitheid op de werkplek.
Voor dit project hebben wij als developmentteam de opdracht gekregen om een nieuwe website te bouwen voor 4U Solutions en op maat gemaakte CMS te bouwen. De website moet de twee hoofdproducten **EasyFWD** en **EasyFlux** op een moderne en duidelijke manier presenteren aan bedrijven en consumenten en het beheer van de website volledig in eigen hand te houden.

---

## Doel van het project
Het doel van di project is het realiseren van:

* Een moderne, responsive website voor 4U Solutions BV
* Een gebruiksvriendelijk, veilig en flexibel maatwerk CMS voor het beheer van de website
* Eenvoudig beheer van pagina's, secties en afbeeldingen door de opdrachtgever
* Integratie met de bestaande backend van 4U Solutions
* Een gebruiksvriendelijke admin-interface voor het beheer van de website

---

## Doelgroep
- **Bedrijven** die ergonomische oplossingen zoeken om productiviteit te verhogen voor hun medewerkers.
- **Consumenten** die zich zorgen maken over hun fysieke en mentale welzijn en hun werkplek willen verbeteren.

---

## Wat zit er wel/niet in het project? 
### Must Have (moet erin zitten)
* Productpagina's voor EasyFlux en EasyFWD
* Maatwerk CMS voor contentbeheer (eigen ontwikkeling)
* Reserveringssysteem voor demo's
* Logym system voor inloggen en beheren van de website
* Volledig responsive design

### Should Have (Liefst wel)
* SEO-optimalisatie
* Intuïtieve interface (tailored admin UI)
* Veilige login met NextAuth.js en JWT
* Een backend die gebruikt kan worden voor de website en het CMS

### Could Have (Misschien, als er tijd is)
* Meertalige ondersteuning (Nederlands & Engels)
* Geavanceerde data-analyse

### Will Not Have (Bewust niet)
* Social media-integratie
* Geavanceerde data-analyse

---

## Gebruikte technologieën
### Frontend:
- **Next.js** (App Router, React & TypeScript)
- **SCSS** voor gestructureerde styling
- **Framer Motion** voor vloeiende UI-animaties
- **React Hook Form** voor efficiënte formulieren en validatie

### Backend:
- **Next.js API Routes** en **tRPC** voor type-safe communicatie tussen frontend en backend
- **MongoDB** (Mongoose) voor opslag van pagina's, secties en gebruikers
- **NextAuth.js** met **CredentialsProvider** en **JWT** voor veilige inlog- en sessiebeheer
- **Cloudinary** voor afbeelding-hosting en optimalisatie

### Tools & Versiebeheer
- **Notion** voor projectmanagement
- **GitHub** voor versiebeheer
- **Mongo Atlas** voor database-hosting
- **Cloudinary** voor afbeelding-hosting

---

## Koppeling met User Stories
De sisen en wensen van de opdrachtgever zijn vertaald naar User Stories, zoals: 

- **US-18 (MongoDB Connection & User Model):**  
  We bouwen een eigen database-architectuur zodat we volledige controle hebben over content-structuur, rollen en schaalbaarheid.

- **US-19 (Admin Dashboard voor Contentbeheer):**  
  Met een op maat gemaakte admin-interface kunnen beheerders precies díe velden, secties en media beheren die relevant zijn voor 4U Solutions, zonder overbodige functies.

- **US-20 (Beveiligde Admin Login):**  
  Door NextAuth.js en JWT in te zetten, garanderen we dat alleen bevoegde gebruikers toegang hebben tot de inhoudsbewerking. 

- **US-21 t/m US-27 (CMS-functionaliteiten):** verdere uitwerking van de CMS-functionaliteiten.

> De volledige user stories zijn uitgewerkt in het bestand [User Stories.md](../opdracht-1-werkzaamheden/criterium-1.2-user-stories.md) onder de criterium 1.2.

---

