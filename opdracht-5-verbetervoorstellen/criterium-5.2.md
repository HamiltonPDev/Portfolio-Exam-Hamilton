# Criterium 5.2: Verbetervoorstellen op basis van oplevering

In dit onderdeel worden verbetervoorstellen gedaan op basis van de oplevering van het product. Hierbij wordt gekeken naar de functionaliteit, het gebruik en de feedback van gebruikers.

---

## 1. Betere feedback bij login- en authenticatiefouten

**Oplevering/Feedback:**
Tijdens de oplevering bleek dat foutmeldingen bij inloggen of toegang tot admin soms te algemeen of technisch zijn (bijvoorbeeld alleen "Unauthorized").

### Waarom moet dit verbeterd worden?
Duidelijke, gebruikersvriendelijke foutmeldingen helpen gebruikers sneller begrijpen wat er misgaat (bijvoorbeeld: "Verkeerd wachtwoord" of "Geen toegang tot deze pagina").

### Stappen
1. Inventariseer alle foutmeldingen bij login en admin-toegang.
2. Schrijf duidelijke, Nederlandstalige meldingen voor elk scenario.
3. Test met gebruikers of de meldingen duidelijk zijn en pas aan waar nodig.

---

## 2. Verbeteren van gebruikersbeheer (admin)

**Oplevering/Feedback:**
Tijdens de oplevering bleek dat het beheer van gebruikers (rollen toekennen, gebruikers blokkeren) beperkt of handmatig is.

### Waarom moet dit verbeterd worden?
Een gebruiksvriendelijk admin-paneel voor gebruikersbeheer maakt het systeem veiliger en makkelijker te onderhouden.

### Stappen
1. Ontwerp een eenvoudige UI voor het beheren van gebruikers en rollen.
2. Implementeer functies zoals "gebruiker blokkeren" of "rol wijzigen".
3. Voeg tests toe voor deze functionaliteit.

---

## 3. Logging en monitoring van loginpogingen

**Oplevering/Feedback:**
Er is nu geen inzicht in mislukte of verdachte loginpogingen.

### Waarom moet dit verbeterd worden?
Door loginpogingen te loggen en te monitoren, kunnen beveiligingsproblemen sneller worden opgespoord en aangepakt.

### Stappen
1. Implementeer logging van alle (mislukte) loginpogingen.
2. Maak een dashboard of rapportage voor admins.
3. Stel alerts in bij verdachte activiteiten (bijvoorbeeld brute-force aanvallen).

---

## 4. Toegankelijkheid (a11y) van het login/admin-proces verbeteren

**Oplevering/Feedback:**
De login- en adminpagina's zijn mogelijk niet goed bruikbaar voor mensen met een beperking (bijvoorbeeld slechtzienden of mensen die alleen een toetsenbord gebruiken).

### Waarom moet dit verbeterd worden?
Toegankelijke software zorgt ervoor dat iedereen, ook mensen met een beperking, de applicatie kan gebruiken.

### Stappen
1. Test de login- en adminpagina's met toetsenbord en screenreader.
2. Verbeter labels, contrast en navigatie waar nodig.
3. Vraag feedback van gebruikers met verschillende behoeften.