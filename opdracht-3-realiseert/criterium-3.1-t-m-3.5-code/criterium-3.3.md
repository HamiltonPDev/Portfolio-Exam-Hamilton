# Criterium 3.3 – Codekwaliteit

## Projectstructuur & Best Practices

Hieronder volgt een overzicht van de projectstructuur van easyFWD, met toelichting en best practices per onderdeel:

```
easyfwd-website/
│
├── src/
│   ├── app/                # Next.js app directory (routes, pages, API)
│   ├── components/         # Herbruikbare React componenten (front-end)
│   ├── models/             # Mongoose datamodellen (User, Page)
│   ├── utils/              # Hulpfuncties (bijv. trpc, navdata)
│   ├── server/             # Server-side logica en routers
│   ├── lib/                # Database-connectie (mongodb.ts)
│   ├── config/             # Configuratiebestanden
│   ├── scss/               # Styling (Sass)
│   └── middleware.ts       # Centrale beveiligingsmiddleware
│
├── public/                 # Publieke assets (afbeeldingen, icons)
├── tests/                  # Testbestanden
├── docker-compose.yml      # Docker configuratie voor development
├── package.json            # Projectafhankelijkheden en scripts
├── README.md               # Projectdocumentatie
└── ... (overige config- en lockbestanden)
```

**Opmerkingen per map/bestand:**
- `/src/app/`: Volgt de nieuwe Next.js app directory structuur. API-routes, pagina's en layouts zijn logisch gescheiden per functionaliteit.
- `/src/components/`: Componenten zijn netjes per domein gegroepeerd en herbruikbaar opgezet (bijv. LoginForm).
- `/src/models/`: Bevat Mongoose-modellen met OOP-methoden, zorgt voor duidelijke scheiding van data en logica (MVC).
- `/src/utils/`: Helpers voor logica die op meerdere plekken nodig is.
- `/src/server/`: Server-side API-routers, houdt API-logica gescheiden van de front-end.
- `/src/lib/`: Centrale plek voor database-connectie.
- `/src/middleware.ts`: Centrale beveiligingsmiddleware, beschermt admin-routes efficiënt en schaalbaar.
- `public/`, `tests/`, `docker-compose.yml`, `README.md`: Assets, testen, development setup en documentatie zijn aanwezig.

**Best practices:**
- Modulaire opzet en duidelijke scheiding van verantwoordelijkheden.
- Herbruikbare componenten en helpers.
- Centrale beveiliging en validatie.
- Goede documentatie en schaalbare structuur.

---

## Structuur & Leesbaarheid
Het usersysteem is modulair en overzichtelijk opgezet:
- **Back-end:** Authenticatie-logica in `/src/app/api/auth/[...nextauth]/route.ts`, het user model in `/src/models/User.ts`, en beveiligingsmiddleware in `/src/middleware.ts`.
- **Front-end:** Herbruikbare componenten zoals `LoginForm.tsx` in `/src/components/login/`.
- Namen van functies, variabelen en componenten zijn beschrijvend en consistent gekozen.

[GitHub link "User model"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/models/User.ts)
```js
/* User model schema (vereenvoudigd) */
const userSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  passwordHash: { type: String, required: true },
  role: { type: String, enum: ['admin', 'editor'], default: 'editor' }
}, { timestamps: true });
```

## Efficiëntie & Herbruikbaarheid
- **Instance-methodes:** Veelgebruikte logica zoals wachtwoordvergelijking is als methode aan het user model toegevoegd, zodat deze overal in de code hergebruikt kan worden.
- **Middleware:** De beveiligingsmiddleware is generiek opgezet en beschermt alle admin-routes op één centrale plek.
- **Componenten:** Het LoginForm is een herbruikbaar React component, losgekoppeld van de rest van de UI.
- **Validatie:** Inputvalidatie gebeurt centraal in het model en in de authorize-functie.

[GitHub link "Compare password"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/models/User.ts)
```js
// src/models/User.ts

/* This interface describes instance methods available on the User model itself. */
export interface IUser extends Document {
  ...
comparePassword(candidatePassword: string): Promise<boolean>;
}

/* instance method to compare password */
userSchema.methods.comparePassword = async function (
  this: IUser,
  candidatePassword: string
): Promise<boolean> {
  return bcrypt.compare(candidatePassword, this.passwordHash);
};
```

[GitHub link "Middleware"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/middleware.ts)
```js
// src/middleware.ts
import { withAuth } from 'next-auth/middleware';
import { NextResponse } from 'next/server';

export default withAuth(
  function middleware(req) {
    return NextResponse.next();
  },
  {
    callbacks: {
      authorized: ({ token }) => {
        return token?.role === 'admin' || token?.role === 'editor';
      },
    },
  }
);
export const config = { matcher: ['/admin/:path*'] };
```
>*Deze middleware zorgt ervoor dat alleen gebruikers met de juiste rol toegang krijgen tot admin-routes. Dit is efficiënt, want hoeft niet in elke route apart te controleren op rechten.*

## Security & Validatie
- Wachtwoorden worden gehasht met bcrypt in het User model, zodat ze nooit als platte tekst in de database staan.
- Authenticatie gebeurt via NextAuth.js met een custom credentials provider.
- JWT-tokens worden opgeslagen in cookies met HttpOnly-attribuut, zodat ze niet kunnen worden gelezen door JavaScript in de browser.
- Gevoelige data (zoals database-URL) staan in `.env`-bestanden, die niet in de repository staan.
- Input wordt gevalideerd met Zod of handmatige checks.

[GitHub link "Hash password"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/models/User.ts)
```js
// src/models/User.ts
userSchema.pre('save', async function (this: IUser, next) {
  if (!this.isModified('passwordHash')) return next();
  const salt = await bcrypt.genSalt(10);
  this.passwordHash = await bcrypt.hash(this.passwordHash, salt);
  next();
});
```

[GitHub link "Authorize function"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/app/api/auth/[...nextauth]/route.ts)
```js
// src/app/api/auth/[...nextauth]/route.ts
if (!user) {
  throw new Error('No user found');
}
```

## Foutafhandeling & Terugkoppeling
- Fouten bij inloggen of registreren worden netjes afgehandeld. De gebruiker krijgt duidelijke feedback, bijvoorbeeld bij een fout wachtwoord of een bestaand e-mailadres.
- In de authorize-functie worden errors gegooid, die door NextAuth worden afgehandeld en als melding aan de gebruiker getoond.
- In de front-end wordt de foutmelding getoond in het LoginForm component.

[GitHub link "LoginForm.tsx"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/components/login/LoginForm.tsx)
```tsx
export const LoginForm = () => {
  const [error, setError] = useState<string | null>(null);
  // ...
  async function handleSubmit(e: React.FormEvent<HTMLFormElement>) {
    // ...
    if (result?.error) {
      setError(result.error);
    }
  }
  return (
    <form className={styles.form} onSubmit={handleSubmit}>
      {error && <div className={styles.error}>{error}</div>}
      {/* ... */}
    </form>
  );
};
```

---

## OOP & MVC in dit project

### OOP in de praktijk van dit project

In dit project heb ik OOP toegepast in het User model. Hierin zijn data (zoals email, passwordHash, rol) en logica (zoals wachtwoordvergelijking) samengebracht in één object. Dit zorgt voor structuur, herbruikbaarheid en veiligheid.

**Voorbeeld uit het project:**
```ts
// src/models/User.ts
import mongoose, { Document, Model, Types } from 'mongoose';
import bcrypt from 'bcryptjs';

export interface IUser extends Document {
  _id: Types.ObjectId;
  email: string;
  passwordHash: string;
  role: 'admin' | 'editor';
  comparePassword(candidatePassword: string): Promise<boolean>;
}

const userSchema = new mongoose.Schema<IUser>(
  {
    email: { type: String, required: true, unique: true },
    passwordHash: { type: String, required: true },
    role: { type: String, enum: ['admin', 'editor'], default: 'editor' },
  },
  { timestamps: true }
);

// Encapsulatie: logica en data samen
userSchema.methods.comparePassword = async function (
  this: IUser,
  candidatePassword: string
): Promise<boolean> {
  return bcrypt.compare(candidatePassword, this.passwordHash);
};

// Abstractie: gebruikt comparePassword zonder te weten hoe bcrypt werkt

// Overerving: IUser extends Document (Mongoose)

const UserModel = mongoose.models.User || mongoose.model<IUser>('User', userSchema);
export default UserModel;
```
Hiermee maak ik gebruik van:
- **Encapsulatie:** Data en logica (zoals wachtwoordcontrole) zitten samen in het model.
- **Abstractie:** De methode `comparePassword` verbergt de complexiteit van bcrypt.
- **Overerving:** Het model erft standaardmethoden van Mongoose via `Document`.

Dit User model is een concreet voorbeeld van OOP in de backend van mijn project.

### MVC in dit project

- **Model:**
  - User model (`/src/models/User.ts`): gebruikersdata, validatie, methoden.
  - Page model (`/src/models/Page.ts`): paginadata, sections, methoden.
- **View:**
  - React componenten zoals LoginForm en Button bepalen de UI.
- **Controller:**
  - API-routes (zoals `/src/app/api/auth/[...nextauth]/route.ts`) en tRPC-routers regelen de communicatie tussen front-end en modellen.
  - **tRPC** fungeert als type-veilige API-controller tussen front-end en back-end. Procedures zoals `getBySlug` of `create` voeren businesslogica uit en valideren input.

*Voorbeeld tRPC-procedure:*
```js
// src/server/api/routers/page.ts
getBySlug: t.procedure
  .input(z.object({ slug: z.string() }))
  .query(async ({ input }) => {
    const page = await PageModel.findBySlug(input.slug);
    if (!page) throw new TRPCError({ code: 'NOT_FOUND', message: 'Page not found' });
    return page;
  }),
```

**Samengevat:**
- In de back-end zijn data en logica netjes gescheiden in modellen en API-routes.
- In de front-end zijn componenten herbruikbaar, goed gestructureerd en maken ze gebruik van props en state (OOP in React).
- Het project volgt zowel OOP- als MVC-principes, wat zorgt voor onderhoudbaarheid, uitbreidbaarheid en duidelijke structuur.

## Conclusie
Het usersysteem is opgezet volgens best practices: de code is modulair, veilig, goed leesbaar en efficiënt. Validatie, foutafhandeling en security zijn op meerdere plekken in de code geborgd. De MVC-structuur en OOP-principes zijn zowel in de back-end als front-end duidelijk terug te zien. Hiermee voldoet het systeem aan de eisen van codekwaliteit.