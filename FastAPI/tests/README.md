# Tests du backend

Les tests doivent démontrer le fonctionnement sans ESP32 physique.

Priorités :
1. authentification et permissions ;
2. création de commande avec réponse 202 et identifiant stable ;
3. dédoublonnage par request_id ;
4. expiration et récupération répétée d'une commande ;
5. refus si l'état ne permet pas l'action ;
6. heartbeat et détection hors ligne ;
7. événements et alertes idempotents ;
8. simulateur : coupure, batterie faible, démarrage, stabilisation GE, transfert ATS, retour JIRAMA, échec et arrêt d'urgence.

Utiliser une base de test séparée. Ne jamais lancer de migration ou de nettoyage contre une base utilisée par le projet réel.
