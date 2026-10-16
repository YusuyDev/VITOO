# Vitoo Backend

API Express + Prisma (SQLite) de Vitoo : authentification (passagers, compagnies, chauffeurs, admin), trajets, réservations, billets, paiements CinetPay et notifications SMS/e-mail.

## Démarrage

```bash
cd backend
cp .env.example .env   # puis remplir les valeurs
npm install
npx prisma db push     # crée/synchronise la base SQLite (pas de migrations)
npm run seed           # optionnel : crée un compte admin de dev
npm run dev
```

Le serveur écoute sur `http://localhost:4000`. Les données sont persistées dans la base SQLite indiquée par `DATABASE_URL`.

## Routes (préfixes)

| Préfixe | Rôle |
|---|---|
| `GET /api/health` | Santé du service |
| `/api/auth` | Auth passager (mot de passe, Google, téléphone) |
| `/api/company/auth`, `/api/company` | Auth et espace compagnie (chauffeurs, véhicules, trajets, billets, messages, stats) |
| `/api/driver/auth`, `/api/driver` | Auth et espace chauffeur |
| `/api/trips`, `/api/payments` | Trajets et paiements côté passager |
| `/api/admin` | Administration — JWT avec le rôle `admin` requis |
| `GET /api/dev/reset?token=…` | Vide la base ; actif seulement si `RESET_TOKEN` est défini |

## Compte administrateur

- En dev : `npm run seed` crée un admin de test.
- En prod : définir `ADMIN_BOOTSTRAP_PHONE` et `ADMIN_BOOTSTRAP_PASSWORD` ; l'admin est créé au démarrage s'il n'en existe aucun.

## Scripts de débogage

`scripts/dev/` contient des scripts jetables qui appellent l'API locale (`http://localhost:4000`) avec des comptes de test. Ce ne sont pas des tests automatisés et ils ne sont pas inclus dans l'image Docker.
