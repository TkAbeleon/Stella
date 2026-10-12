# Checklist fonctionnelle

Cocher uniquement après implémentation et test, pas lorsque la fonction est simplement documentée.

> Application Java : code écrit sur la branche `feature/mobile-android` mais non compilé ni testé sur appareil — les cases restent donc décochées. Détails : [MOBILE_IMPLEMENTATION.md](MOBILE_IMPLEMENTATION.md).

## P0 — Minimum démontrable

### Backend et stockage
- [ ] FastAPI démarre avec configuration locale.
- [ ] PostgreSQL est la base active.
- [ ] Migrations Alembic créent et mettent à jour les tables.
- [ ] Aucun secret réel n'est commité.
- [ ] /health ne divulgue aucune donnée sensible.
- [ ] Format d'erreur API cohérent.

### Connexion et droits
- [ ] Connexion identifiant/mot de passe.
- [ ] Mots de passe stockés sous forme de hash.
- [ ] Token expirant et gestion de session expirée dans le mobile.
- [ ] Rôles ADMIN, OPERATEUR, LECTURE validés dans le backend.
- [ ] Un utilisateur sans droits ne peut pas contourner les contrôles via l'API.

### État et événements
- [ ] Heartbeat du contrôleur.
- [ ] Détection d'appareil hors ligne.
- [ ] Données inconnues distinctes de false.
- [ ] Timestamp et fraîcheur visibles.
- [ ] Historique d'événements enregistré dans PostgreSQL.

### Commandes
- [ ] Création d'une commande avec identifiant et request_id.
- [ ] 202 Accepted signifie demande enregistrée, pas résultat physique.
- [ ] Expiration des commandes.
- [ ] ESP32 simulé récupère les commandes par polling.
- [ ] Contrôleur accepte ou refuse avec une raison.
- [ ] Résultat provenant du contrôleur/simulateur après vérification.
- [ ] Une requête répétée ne provoque pas une commande dupliquée.
- [ ] Mode manuel et arrêt d'urgence restent prioritaires.

### Application Java 
- [ ] Connexion et gestion de session expirée.  *(implémenté, non testé)*
- [ ] Tableau de bord et état alimentation.  *(implémenté, non testé)*
- [ ] Statut JIRAMA, UPS, GE, ATS avec heure et fraîcheur.  *(implémenté, non testé)*
- [ ] Confirmation des commandes.  *(implémenté, non testé)*
- [ ] Progression des commandes visible.  *(implémenté, non testé)*
- [ ] Historique et alertes consultables.  *(implémenté, non testé)*
- [ ] Chargement, erreur réseau, état vide et hors ligne traités.  *(implémenté, non testé)*
- [ ] Accès administrateur conditionné par le rôle.  *(squelette seulement ; implémenté, non testé)*
- [ ] Palette JIRAMA et contrastes vérifiés. *(palette appliquée, contrastes calculés ; non testé sur appareil)*

### Simulateur et tests
- [ ] Perte JIRAMA et temporisation.
- [ ] Rappel opérateur et batterie faible.
- [ ] Démarrage GE réussi et GE instable.
- [ ] Trois tentatives de démarrage échouées.
- [ ] Détection puis stabilité GE avant transfert.
- [ ] Retour ATS absent ou contradictoire.
- [ ] Retour JIRAMA stable, refroidissement puis arrêt.
- [ ] Mode manuel, arrêt d'urgence, défaut GE.
- [ ] Perte réseau et reconnexion.
- [ ] Tests automatisés des API et transitions critiques.

## P1 — Si le temps le permet
- [ ] Gestion d'utilisateurs par ADMIN.
- [ ] Configuration des temporisations autorisées.
- [ ] Acquittement des alertes.
- [ ] Résumé des coupures et durées.
- [ ] Export CSV.
- [ ] Journal d'audit.
- [ ] Notifications Android.
- [ ] Thème sombre.

## P2 — Pas avant P0
- [ ] Graphiques avancés.
- [ ] MQTT ou WebSocket.
- [ ] Services distribués.
- [ ] Fonctions automatiques supplémentaires non demandées.
- [ ] Communication directe mobile → ESP32.

## Critère de démonstration

L'opérateur peut se connecter, observer un scénario simulé, soumettre une commande, suivre son résultat, consulter l'historique et constater un refus de sécurité sans matériel réel. Cela ne valide ni le câblage ni la sécurité du système physique installé.
