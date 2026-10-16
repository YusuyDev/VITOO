# Vitoo

Plateforme de réservation de trajets interurbains : les passagers réservent et paient leurs billets, les compagnies gèrent trajets, véhicules et chauffeurs, les chauffeurs suivent leurs départs, et un espace admin supervise l'ensemble.

## Structure

- `/` — frontend React + Vite + Tailwind (TypeScript), empaquetable en application mobile avec Capacitor
- `backend/` — API Express + Prisma (SQLite), projet npm séparé (voir [backend/README.md](backend/README.md))

## Démarrage en local

```bash
# API (terminal 1)
cd backend && cp .env.example .env && npm install && npx prisma db push && npm run dev

# Frontend (terminal 2, à la racine)
npm install
npm run dev   # http://localhost:5173
```

Variables du frontend (fichier `.env.local` à la racine) : `VITE_API_URL`, `VITE_GOOGLE_CLIENT_ID`, `VITE_MAPBOX_PUBLIC_TOKEN`, `VITE_MAPBOX_STYLE`.

En dev, la page d'accueil affiche un sélecteur d'espaces (`/dev`) ; en production, `/` redirige vers l'espace passager.

## Déploiement

Voir [README.DEPLOYEMENT.md](README.DEPLOYEMENT.md) (Render, Vercel, Docker, CinetPay).
