# Mon Projet - Monorepo NestJS + React + Vite

Un monorepo contenant une application web complète avec backend NestJS et frontend React (Vite), entièrement containerisée avec Docker.

## 🏗️ Structure du projet

```
mon-projet/
├── apps/
│   ├── backend/          # API NestJS + TypeORM + PostgreSQL
│   └── frontend/         # React + Vite + TypeScript
├── docker-compose.yml    # Configuration production
├── docker-compose.dev.yml # Configuration développement
└── package.json          # Scripts globaux
```

## 🚀 Démarrage rapide

### Prérequis
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Développement
```bash
# Cloner le repo
git clone https://github.com/votre-username/mon-projet.git
cd mon-projet

# Lancer en mode développement (avec hot-reload)
npm run dev

# Accéder aux applications
# Frontend: http://localhost:5173
# Backend: http://localhost:3000
# Database: localhost:5432
```

### Production
```bash
# Lancer en mode production
npm run prod

# Accéder aux applications
# Frontend: http://localhost:80
# Backend: http://localhost:3000
```

## 🛠️ Scripts disponibles

| Script | Description |
|--------|-------------|
| `npm run dev` | Lance l'environnement de développement |
| `npm run dev:down` | Arrête l'environnement de développement |
| `npm run prod` | Lance l'environnement de production |
| `npm run prod:down` | Arrête l'environnement de production |
| `npm run clean` | Nettoie les images et volumes Docker |

## 🔧 Configuration

### Variables d'environnement
Les variables sont définies dans les fichiers docker-compose :
- `DATABASE_HOST`, `DATABASE_PORT`, `DATABASE_NAME`
- `DATABASE_USER`, `DATABASE_PASSWORD`
- `NODE_ENV`

### Base de données
- **Type** : PostgreSQL 15
- **Port** : 5432
- **Nom** : myapp
- **Utilisateur** : myuser
- **Mot de passe** : mypassword

## 🏃‍♂️ Développement

### Backend (NestJS)
```bash
# Accéder au conteneur backend
docker-compose -f docker-compose.dev.yml exec backend sh

# Générer une migration
npm run migration:generate -- -n NomDeLaMigration

# Exécuter les migrations
npm run migration:run
```

### Frontend (React + Vite)
```bash
# Accéder au conteneur frontend
docker-compose -f docker-compose.dev.yml exec frontend sh

# Installer une nouvelle dépendance
npm install nouvelle-dependance
```

## 🚢 Déploiement

### Avec Docker Compose
```bash
# Production
docker-compose up -d --build

# Vérifier les logs
docker-compose logs -f
```

### Avec Docker Hub
```bash
# Tag et push des images
docker tag mon-projet_backend:latest votre-username/mon-projet-backend:latest
docker tag mon-projet_frontend:latest votre-username/mon-projet-frontend:latest

docker push votre-username/mon-projet-backend:latest
docker push votre-username/mon-projet-frontend:latest
```

## 🔍 Troubleshooting

### Problèmes courants

**Base de données non accessible** :
```bash
docker-compose down
docker volume rm mon-projet_postgres_data
docker-compose up --build
```

**Ports occupés** :
```bash
# Vérifier les ports utilisés
netstat -tulpn | grep :3000
netstat -tulpn | grep :5173
```

**Conteneurs qui ne démarrent pas** :
```bash
# Voir les logs détaillés
docker-compose logs service-name

# Reconstruire sans cache
docker-compose build --no-cache
```

## 🤝 Contribution

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add AmazingFeature'`)
4. Push sur la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## 📝 License

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 🆘 Support

Pour toute question ou problème :
- Ouvrir une [issue](https://github.com/votre-username/mon-projet/issues)
- Consulter la [documentation](https://github.com/votre-username/mon-projet/wiki)