# Criterium 3.5 – Verzorging, leesbaarheid & commentaar

## Verzorging & leesbaarheid
- De code is netjes opgemaakt met consistente inspringing en witregels.
- Variabelen, functies en componenten hebben duidelijke, beschrijvende namen.
- De code bevat geen overbodige of dode code.

## Structuur
- De mappenstructuur is logisch en consistent.
- Bestanden zijn niet te groot en bevatten één duidelijke verantwoordelijkheid.

## Commentaar
- Bij belangrijke functies en complexe logica staat een korte uitleg.
- Commentaar is beknopt, relevant en helpt bij het begrijpen van de code.

## Voorbeelden uit de code
```js
// src/models/User.ts
// Instance method: compares a candidate password to the stored hash
userSchema.methods.comparePassword = async function (
  this: IUser,
  candidatePassword: string
): Promise<boolean> {
  // bcrypt.compare returns true if the password matches the hash
  return bcrypt.compare(candidatePassword, this.passwordHash);
};
```

```tsx
// src/components/shared/button/Button.tsx
// Button component for consistent UI buttons throughout the app
export const Button: React.FC<ButtonProps> = ({ text, onClick, color }) => (
  <button className={color} onClick={onClick}>{text}</button>
);
```

```js
// src/server/api/routers/page.ts
/* tRPC-procedure met duidelijke inputvalidatie en foutafhandeling voor de pagina's */
export const pageRouter = t.router({

  /* Get all pages */
  getAll: t.procedure.query(async () => {
    return PageModel.find().sort({ createdAt: -1 });
  }),

  /* Get a page by slug (with sections) */
  getBySlug: t.procedure
    .input(z.object({ slug: z.string() }))
    .query(async ({ input }) => {
      const page = await PageModel.findBySlug(input.slug);
      if (!page) throw new TRPCError({ code: 'NOT_FOUND', message: 'Page not found' });
      return page;
    }),

  // ...
});
```

## Conclusie
Mijn code is overal verzorgd, goed leesbaar, logisch gestructureerd en voorzien van zinvol commentaar. Dit maakt het project makkelijk te begrijpen en te onderhouden. 