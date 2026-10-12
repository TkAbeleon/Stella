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

## Construire et lancer

1. Ouvrir le dossier `mobile/` dans Android Studio (JDK 21, SDK Android 36) et synchroniser Gradle.
2. Démarrer FastAPI sur le PC (port 8000). Dans l'émulateur, `10.0.2.2` désigne le PC : l'URL par défaut du build `debug` est `http://10.0.2.2:8000/api/v1` (modifiable sur l'écran de connexion). Sur un téléphone réel, saisir `http://<IP-du-PC>:8000/api/v1`.
3. Lancer `app` ; tests unitaires : `./gradlew test`.
4. Build `release` : définir l'URL HTTPS dans `app/build.gradle` (`DEFAULT_BASE_URL`).

Statut, hypothèses sur l'API et travail restant : voir [Doc/MOBILE_IMPLEMENTATION.md](../Doc/MOBILE_IMPLEMENTATION.md).

## Structure réellement implémentée

~~~text
app/src/main/java/mg/stella/mobile/
├── api/        ApiClient, ApiException
├── auth/       SessionManager
├── model/      DeviceStatus, EventItem, CommandInfo
├── ui/         MainActivity, BaseFragment, ErrorMessages
│   ├── login/ dashboard/ commands/ events/ settings/
└── util/       Json, Dates, Labels
~~~
(Les écrans « users » sont reportés en P1.)
