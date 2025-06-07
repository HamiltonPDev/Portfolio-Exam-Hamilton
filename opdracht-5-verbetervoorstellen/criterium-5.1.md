# Criterium 5.1: Verbetervoorstellen op basis van testen

In dit onderdeel worden verbetervoorstellen gedaan op basis van de resultaten uit de uitgevoerde tests (zie [opdracht 4](../opdracht-4-testen/TESTREPORT.md)). Ook als alle tests geslaagd zijn, zijn er altijd scenario's of uitbreidingen te bedenken die de kwaliteit van de applicatie verder kunnen verhogen.

---

## 1. Edge cases en security: brute-force & rate limiting

**Testscenario:**
De huidige tests dekken standaard login-scenario's, maar niet wat er gebeurt bij brute-force aanvallen of te veel inlogpogingen.

### Waarom moet dit verbeterd worden?
Hoewel de applicatie correct reageert op geldige en ongeldige logins, is het systeem kwetsbaar voor geautomatiseerde aanvallen. Zonder rate limiting of lockout-mechanismen kan een kwaadwillende onbeperkt wachtwoorden proberen.

### Stappen
1. Implementeer rate limiting op de login endpoint (bijvoorbeeld max. 5 pogingen per minuut per IP).
2. Voeg tests toe die meerdere foutieve pogingen simuleren en controleer of verdere pogingen tijdelijk worden geblokkeerd.
3. Voeg logging toe voor verdachte activiteiten.

---

## 2. Databasefouten: rollback en dataconsistentie

**Testscenario:**
De Jest-test controleert of er een foutmelding komt bij een databasefout, maar niet of de database in een consistente staat blijft.

### Waarom moet dit verbeterd worden?
Bij een databasefout kan het zijn dat data gedeeltelijk wordt opgeslagen. Dit kan leiden tot inconsistentie of corrupte gebruikersdata.

### Stappen
1. Implementeer transacties of rollback-mechanismen bij kritieke database-operaties.
2. Voeg tests toe die een geforceerde databasefout simuleren en controleer of er geen (deels) nieuwe data wordt opgeslagen.
3. Controleer na een fout of de database nog in de verwachte staat is.

---

## 3. Multi-user en concurrency scenario's

**Testscenario:**
De huidige tests zijn gericht op één gebruiker per keer. Er is niet getest wat er gebeurt als meerdere gebruikers tegelijk inloggen of acties uitvoeren.

### Waarom moet dit verbeterd worden?
In een productieomgeving kunnen race conditions of concurrency-problemen optreden, bijvoorbeeld dubbele sessies of onverwachte foutmeldingen.

### Stappen
1. Schrijf tests die meerdere gelijktijdige login-acties uitvoeren (bijvoorbeeld met Cypress of een load testing tool).
2. Controleer of alle gebruikers correct worden ingelogd en geen sessies van elkaar overnemen.
3. Implementeer locks of andere concurrency-oplossingen indien nodig.

---

## 4. Mobiele browsers en responsiviteit

**Testscenario:**
De Cypress-tests zijn alleen uitgevoerd in een desktop-browser.

### Waarom moet dit verbeterd worden?
Veel gebruikers loggen in via mobiele apparaten. Zonder testen op mobiel kunnen er bugs of usability-problemen ontstaan die op desktop niet zichtbaar zijn.

### Stappen
1. Voeg Cypress-tests toe voor verschillende mobiele resoluties (bijvoorbeeld iPhone, Android).
2. Controleer of alle functionaliteit (login, foutmeldingen, redirects) ook op mobiel werkt.
3. Optimaliseer de UI/UX waar nodig voor touch en kleine schermen.

---

*Deze lijst kan worden aangevuld naarmate er meer tests worden uitgevoerd of nieuwe scenario's zich voordoen.* 