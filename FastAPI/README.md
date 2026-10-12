# Backend FastAPI

Cible : Python + FastAPI + PostgreSQL, SQLAlchemy et Alembic. Le but est de livrer vite une API lisible et testable. Ne pas ajouter de microservices, broker ou infrastructure temps réel sans nécessité.

## Organisation prévue

~~~text
FastAPI/
├── app/
│   ├── main.py
│   ├── api/v1/router.py
│   ├── api/v1/routes/
│   │   ├── auth.py
│   │   ├── devices.py
│   │   ├── commands.py
│   │   ├── events.py
│   │   ├── alerts.py
│   │   ├── users.py
│   │   └── simulator.py
│   ├── core/config.py
│   ├── core/security.py
│   ├── db/session.py
│   ├── db/models.py
│   ├── schemas/
│   ├── services/
│   └── repositories/
├── alembic/
├── tests/
├── .env.example
├── requirements.txt
└── README.md
~~~

## Choix de simplicité

- Routes REST JSON, toutes sous le préfixe /api/v1.
- SQLAlchemy 2.x avec le pilote psycopg ; migrations Alembic.
- Routes HTTP courtes, validation Pydantic, règles métier dans des services simples.
- Le backend enregistre une commande ; le contrôleur la récupère et décide localement si elle est sûre à exécuter.
- Tests sur authentification, droits, transitions de commande, données invalides et doublons.
- Simulateur activé uniquement en développement et désactivé en production.

## Démarrage prévu

1. Créer un environnement virtuel et installer requirements.txt.
2. Copier .env.example vers .env et définir les paramètres localement.
3. Créer une base PostgreSQL dédiée et exécuter les migrations Alembic.
4. Lancer avec uvicorn app.main:app --reload.
5. Vérifier /docs, /openapi.json et /health.

Ces commandes décrivent le démarrage cible ; tant que les fichiers d'application ne sont pas ajoutés, le backend n'est pas exécutable.
