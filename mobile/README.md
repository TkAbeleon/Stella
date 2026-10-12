# Application Android mobile — Java

L'application cible est native Android en Java. Les fichiers de l'ancienne application sont conservés sous Archive/avant-reorganisation/Interface/. Le nouveau développement doit respecter Doc/API_FASTAPI_MOBILE.md et Doc/DESIGN_MOBILE.md.

## Organisation recommandée

~~~text
mobile/
├── app/src/main/java/.../
│   ├── api/          # client HTTP, DTO, erreurs
│   ├── auth/         # session et permissions
│   ├── data/         # repositories et cache léger
│   ├── model/        # modèles de présentation
│   ├── ui/
│   │   ├── login/
│   │   ├── dashboard/
│   │   ├── commands/
│   │   ├── events/
│   │   ├── alerts/
│   │   ├── settings/
│   │   └── users/
│   └── util/
├── design/
├── build.gradle
└── README.md
~~~

## Règles d'implémentation

- Utiliser Java et les composants Android/Material compatibles avec le projet.
- Regrouper les requêtes dans un client API unique.
- Ne jamais intégrer une clé d'appareil ou un secret backend dans l'APK.
- Montrer l'état réellement rapporté par l'appareil et l'heure de dernière mise à jour.
- Après une commande, montrer son statut ; ne pas déduire la réussite de la seule réponse HTTP.
- Exiger une confirmation avant les actions physiques et désactiver les actions lorsque les données sont périmées ou inconnues.
- Les permissions sont vérifiées par le backend, même si l'écran est masqué.
- Tester petits écrans, textes agrandis, rotation et pertes réseau.
