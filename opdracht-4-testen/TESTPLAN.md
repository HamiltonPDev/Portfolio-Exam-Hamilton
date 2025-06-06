# Criterium 4.1 & 4.2: Testplan & Testscenario's

## User Stories Covered
- US-22: User login with credentials
- US-23: Role-based access (admin)

## Test Scenarios
| Scenario        | Steps                                 | Test Data                                 | Expected Result         |
|----------------|---------------------------------------|-------------------------------------------|------------------------|
| Valid login    | POST /api/auth with correct credentials| email: admin@easyfwd.com, pass: admin1234 | 200 OK, JWT issued     |
| Invalid login  | POST /api/auth with wrong password     | email: admin@easyfwd.com, pass: wrong     | 401 Unauthorized       |
| Admin access   | GET /admin as admin                    | admin JWT                                 | 200 OK                 |
| User access    | GET /admin as user                     | user JWT                                  | 403 Forbidden          |
| ...            | ...                                   | ...                                       | ...                    |

## Testaanpak
Voor het testen van de applicatie zijn zowel **unit tests** (met Jest) als **end-to-end tests** (met Cypress) gebruikt. Hiermee is de betrouwbaarheid en veiligheid van het authenticatiesysteem en de login-functionaliteit gecontroleerd.

- [Unit tests: `easyfwd-website/tests/auth/auth.test.ts`](https://github.com/HamiltonPDev/easyFWD/blob/main/tests/auth/auth.test.ts)
- [E2E tests: `easyfwd-website/cypress/e2e/auth.cy.ts`](https://github.com/HamiltonPDev/easyFWD/blob/main/cypress/e2e/auth.cy.ts) 

Zie het [testverslag](TESTREPORT.md) voor de volledige resultaten en screenshots.

## How to Run the Tests

### Unit tests (Jest)
Voer eenvoudig de volgende command uit:
```sh
npm test
```

### End-to-end tests (Cypress)
1. Start de Docker-component (MongoDB) en verbind eventueel met MongoDB Compass.
2. Maak een admin-gebruiker aan door deze URL te bezoeken:
   [http://localhost:3000/api/test-user/](http://localhost:3000/api/test-user/)
3. Start de Next.js development server:
```sh
npm run dev
```
4. Start Cypress:
```sh
npm run cypress:open
```
of voor headless run:
```sh
npm run cypress:run
``` 