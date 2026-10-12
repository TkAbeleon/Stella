# Backend FastAPI

Backend Stella en Python/FastAPI, SQLAlchemy et PostgreSQL. Le dépôt contient les routes REST, la couche métier, les modèles de données, l'authentification par jeton et un simulateur logiciel du contrôleur ESP32.

## Docker

Le `Dockerfile` utilise Python 3.12 slim, installe les dépendances, exécute Uvicorn sans mode `--reload` et lance l'application avec un utilisateur non privilégié. Le simulateur et les données de démonstration sont désactivés par défaut dans l'image.

Depuis la racine du dépôt :

```bash
docker build -t stella-api:local ./FastAPI
```

Démarrage (remplacer l'adresse de base de données par une adresse joignable depuis le conteneur) :

```bash
docker run --rm --name stella-api \
  -p 8000:8000 \
  -e APP_ENV=production \
  -e DATABASE_URL='postgresql+psycopg://stella_app:mot-de-passe@hote-postgres:5432/stella' \
  -e JWT_SECRET_KEY='<secret-aleatoire-long-de-32-caracteres-minimum>' \
  -e SIMULATOR_ENABLED=false \
  -e SEED_DEV_DATA=false \
  stella-api:local
```

Ne pas placer de vrais secrets dans le dépôt, le Dockerfile ou l'historique du terminal partagé. Injecter les valeurs depuis l'environnement de déploiement ou un gestionnaire de secrets. Depuis un conteneur, `localhost` désigne le conteneur lui-même, pas l'hôte PostgreSQL.

- API : `http://localhost:8000`
- Documentation interactive : `http://localhost:8000/docs`
- Contrôle de santé HTTP : `http://localhost:8000/health`

Le contrôle Docker `HEALTHCHECK` vérifie que l'endpoint HTTP répond ; il ne prouve pas que PostgreSQL accepte les connexions.

## Limites actuelles avant un déploiement réel

- Le dépôt ne contient pas encore de migration Alembic/configuration de migration. Le schéma PostgreSQL doit donc être préparé séparément ; le conteneur n'exécute pas de création automatique des tables en production.
- La validation de démarrage exige un `JWT_SECRET_KEY` valide en production, avec au moins 32 caractères.
- En production, garder `SIMULATOR_ENABLED=false` et `SEED_DEV_DATA=false`.
- Le simulateur et les comptes de démonstration sont réservés au développement/test.
- Une compilation Docker ne remplace ni les tests FastAPI, ni les tests d'intégration à PostgreSQL, ni la validation de sécurité.

## Développement local sans Docker

1. Créer un environnement virtuel et installer `requirements.txt`.
2. Copier `.env.example` vers `.env` et configurer l'environnement local.
3. Préparer une base de données adaptée à l'environnement.
4. Lancer `uvicorn app.main:app --reload` depuis ce dossier.
5. Lancer les tests avec `pytest`.

Voir aussi les contrats dans `../Doc/API_FASTAPI_MOBILE.md` et `../Doc/API_FASTAPI_ELECTRONIQUE.md`.
