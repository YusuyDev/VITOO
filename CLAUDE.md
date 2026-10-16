# Vitoo

- Deux projets npm indépendants : le frontend à la racine, l'API dans `backend/`. Installer, builder et lancer chacun depuis son propre dossier.
- L'API écoute sur le port 4000 et lit `backend/.env` (`tsx --env-file`) ; le frontend la joint via `VITE_API_URL`.
- Prisma utilise SQLite **sans migrations** : on modifie `backend/prisma/schema.prisma` puis `npx prisma db push`. Le conteneur fait aussi un `db push` au démarrage.
- En production, un seul conteneur sert l'API et le SPA buildé (voir `Dockerfile`) ; toute route `/api` inconnue doit rester une 404 JSON.
- `src/dev/` (routes `/dev`, `/maptest`) est réservé au développement ; en prod `/` redirige vers `/passenger`.
- `backend/scripts/dev/` contient des scripts de débogage jetables, pas des tests. Il n'existe pas encore de suite de tests : valider avec `npm run build` (et `npm run lint` à la racine).
- Services externes : paiements CinetPay, SMS Africa's Talking / Twilio, e-mails Resend, connexion Google, cartes Mapbox/Leaflet.
- Textes de l'interface et messages d'API en français.

## Interdits

- Ne jamais committer de fichier `.env` ni de vraie clé (CinetPay, Twilio, JWT…). Seuls les `*.example` sont versionnés.
- Ne jamais appeler `/api/dev/reset` ailleurs qu'en local : il vide toute la base.
