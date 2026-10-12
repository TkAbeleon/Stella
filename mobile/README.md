# Application Android mobile — Java

Ce dossier contient maintenant un projet Android Gradle compilable, initialisé à partir de l'application Java existante avant la réorganisation. L'ancienne copie reste préservée sous `Archive/avant-reorganisation/Interface/`.

## Compiler localement

Sur un poste ayant un JDK 21 et le SDK Android installé :

~~~bash
chmod +x ./gradlew
./gradlew --no-daemon testDebugUnitTest assembleDebug
~~~

L'APK de debug est produit sous `app/build/outputs/apk/debug/app-debug.apk`.

## Build automatique

Le workflow [Android Build](../.github/workflows/android-build.yml) s'exécute à chaque push sur `main` touchant `mobile/**), lors d'une pull request ciblant `main`, ou manuellement depuis l'onglet GitHub Actions. Il compile et teste les sources puis publie l'APK comme artefact téléchargeable du run.

## État d'intégration

Le code Java actif est une base existante conservée pour obtenir un build reproductible. Son client API historique communique encore avec les anciennes routes Java/Spring. Il faudra ensuite adapter `ApiClient` au contrat cible de `../Doc/API_FASTAPI_MOBILE.md`. Le fait que l'APK compile ne signifie donc pas que l'application est déjà intégrée au nouveau backend FastAPI.

La conception fonctionnelle des écrans et la palette cible sont décrites dans [DESIGN_MOBILE.md](../Doc/DESIGN_MOBILE.md). L'intégration de ces changements visuels et fonctionnels reste à réaliser.
