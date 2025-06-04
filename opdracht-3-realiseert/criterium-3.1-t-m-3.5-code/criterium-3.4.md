# Criterium 3.4 – Code conventions & structuur

## Code conventions
- Ik gebruik camelCase voor variabelen en functies (bijv. `userEmail`, `handleSubmit`).
- Componenten en modellen zijn in PascalCase (bijv. `LoginForm`, `UserModel`).
- Bestandsnamen zijn duidelijk en beschrijvend (bijv. `LoginForm.tsx`, `User.ts`).
- Consistente inspringing (2 spaties) en witregels voor leesbaarheid.
- Korte, duidelijke comments waar nodig.

## Structuur
- De mappenstructuur is logisch: front-end, back-end, modellen, utils, middleware, enz.
- Elke map bevat alleen relevante bestanden (bijv. alle modellen in `/models`, alle componenten in `/components`).
- API-routes en pagina's zijn gescheiden in de Next.js app directory.

## Voorbeelden uit de code
[GitHub link "User model"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/models/User.ts)

```js
/* Define the schema for the User collection in MongoDB. */
const userSchema = new mongoose.Schema<IUser, IUserModel>(
  {
    /* Email field: required, unique, trimmed, lowercased, and must match email regex */
    email: {
      type: String,
      required: [true, 'Email is required'],
      unique: true,
      trim: true,
      lowercase: true,
      match: [/^\S+@\S+\.\S+$/, 'Please use a valid email address'],
    },
    /* Password hash field: required */
    passwordHash: {
      type: String,
      required: [true, 'Password is required'],
    },
    /* Role field: can be 'admin' or 'editor', defaults to 'editor' */
    role: {
      type: String,
      enum: ['admin', 'editor'],
      default: 'editor',
    },
  },
  {
    timestamps: true, // Automatically adds createdAt and updatedAt fields
  }
);
```

[GitHub link "LoginForm"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/components/login/LoginForm.tsx)

```tsx
// src/components/login/LoginForm.tsx
export const LoginForm = () => {
  const router = useRouter();
  const [error, setError] = useState<string | null>(null);
  const [loading, setLoading] = useState(false);
  // ...
};
```

[GitHub link "Middleware"](https://github.com/HamiltonPDev/easyFWD/blob/main/src/middleware.ts)

```js
// src/middleware.ts
import { withAuth } from 'next-auth/middleware';
import { NextResponse } from 'next/server';

/* Protect /admin routes: only allow users with 'admin' or 'editor' role */
export default withAuth(
  () => NextResponse.next(),
  {
    callbacks: {
      authorized: ({ token }) => token?.role === 'admin' || token?.role === 'editor',
    },
  }
);

/* Apply middleware only to /admin routes */
export const config = {
  matcher: ['/admin/:path*'],
};
```

## Conclusie
Mijn code voldoet aan de geldende code conventions en is overal gestructureerd, leesbaar en professioneel opgezet. De structuur en conventies maken het project makkelijk te onderhouden en uit te breiden.