# Criterium 5.3: Verbetervoorstellen op basis van reflectie

In dit onderdeel worden verbetervoorstellen gedaan op basis van reflectie op het ontwikkelproces en de eigen bijdrage. Door kritisch terug te kijken op het proces kunnen zowel het project als de persoonlijke ontwikkeling worden verbeterd.

---

## 1. Eerder en breder testen van edge cases

**Reflectie/Ervaring:**
Tijdens het testen lag de focus vooral op standaard scenario's (geldige/ongeldige login, admin/user toegang). Edge cases zoals brute-force aanvallen, sessie-verloop of gelijktijdige logins zijn niet meegenomen.

### Waarom moet dit verbeterd worden?
Door vanaf het begin ook edge cases te testen, worden potentiële beveiligings- en stabiliteitsproblemen eerder ontdekt.

### Stappen
1. Brainstorm in een vroege sprint over mogelijke edge cases en security scenario's.
2. Voeg deze scenario's toe aan het testplan en implementeer ze in Jest/Cypress.
3. Evalueer regelmatig of er nieuwe edge cases zijn bijgekomen.

---

## 2. Testautomatisering en CI/CD direct opzetten

**Reflectie/Ervaring:**
De testautomatisering en CI/CD zijn pas later in het project opgezet, waardoor fouten soms pas laat werden ontdekt.

### Waarom moet dit verbeterd worden?
Door direct te automatiseren en CI/CD te gebruiken, worden fouten sneller zichtbaar en blijft de codebase stabiel.

### Stappen
1. Zet direct bij projectstart een basis CI/CD-pipeline op (bijvoorbeeld GitHub Actions).
2. Automatiseer het draaien van alle tests bij elke commit/push.
3. Monitor de pipeline en verbeter waar nodig.

---

## 3. Meer samenwerking en kennisdeling rond testen

**Reflectie/Ervaring:**
Het testproces is grotendeels individueel uitgevoerd. Er was weinig overleg of review van testscenario's door teamleden.

### Waarom moet dit verbeterd worden?
Door samen te testen en elkaars scenario's te reviewen, worden blinde vlekken voorkomen en leren teamleden van elkaar.

### Stappen
1. Plan gezamenlijke testreview-sessies in (bijvoorbeeld na elke sprint).
2. Laat teamleden elkaars testcode en scenario's reviewen.
3. Documenteer en deel best practices binnen het team.

---

## 4. Vroeger gebruikersfeedback ophalen over login/admin

**Reflectie/Ervaring:**
Feedback van gebruikers over het loginproces en admin-functionaliteit is pas laat in het traject verzameld.

### Waarom moet dit verbeterd worden?
Vroegtijdige feedback zorgt ervoor dat de functionaliteit beter aansluit bij de wensen en verwachtingen van gebruikers.

### Stappen
1. Plan feedbackmomenten in na elke grote oplevering of sprint.
2. Gebruik demo's of prototypes om gebruikers te laten testen.
3. Verwerk feedback direct in de backlog en testscenario's.