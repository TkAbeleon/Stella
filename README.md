# Stella — supervision et commande de l'alimentation

## Objectif

Construire rapidement une solution simple à tester de bout en bout pour superviser l'alimentation JIRAMA / UPS / groupe électrogène (GE).

Cible : **FastAPI + Python**, **PostgreSQL**, **Android en Java**, et un **simulateur logiciel** pour les essais sans matériel. La responsable électronique adaptera ensuite son firmware et l'interface physique au contrat documenté ici.

Le backend FastAPI et le nouveau firmware ne sont pas présentés comme déjà implémentés : ce dépôt définit la cible d'organisation et les contrats.

## Dossiers

| Dossier | Rôle |
|---|---|
| [FastAPI](FastAPI/README.md) | Organisation du backend Python |
| [mobile](mobile/README.md) | Application Android Java |
| [Doc](Doc/README.md) | Architecture, contrats API, conception, checklist et données |
| [Electronique](Electronique/README.md) | Contrat logiciel et sketch de référence inchangé |
| [Archive](Archive/README.md) | Copies des sources avant réorganisation |

## À lire en premier

1. [Architecture cible](Doc/ARCHITECTURE.md)
2. [Contrat mobile ↔ FastAPI](Doc/API_FASTAPI_MOBILE.md)
3. [Contrat ESP32 ↔ FastAPI](Doc/API_FASTAPI_ELECTRONIQUE.md)
4. [Conception mobile](Doc/DESIGN_MOBILE.md)
5. [Checklist fonctionnelle](Doc/CHECKLIST_FONCTIONNELLE.md)
6. [Modèle PostgreSQL](Doc/MODELE_POSTGRESQL.md)
7. [Décisions et limites](Doc/DECISIONS_ET_LIMITES.md)

## Principe d'intégration

Le mobile ne communique qu'avec FastAPI. L'ESP32 initie aussi ses requêtes HTTP vers FastAPI : heartbeat, événements, récupération des commandes et accusés de réception. Le backend n'a donc pas besoin de pouvoir joindre directement l'ESP32.

Le contrôleur conserve les automatismes et sécurités locales. Une commande enregistrée ne prouve pas que le GE a démarré ou que l'ATS a changé de position.

## État

- [ ] Implémenter FastAPI et PostgreSQL.
- [ ] Implémenter le simulateur logiciel.
- [ ] Construire l'application Android Java selon la conception.
- [ ] Adapter et tester le firmware selon le contrat.
- [ ] Tester l'intégration ; faire valider les essais physiques par la personne compétente.
