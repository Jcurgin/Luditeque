# Mettre Luditèque en ligne sur Google Play

Tout est prêt : l'appli, sa construction automatique, la clé de signature, les visuels, les textes et la politique de confidentialité. **Tu n'as besoin ni d'Android Studio ni de Node.js** : GitHub fabrique le fichier `.aab` pour toi, gratuitement, dans le cloud.

## Ce que tu as reçu

- **`luditeque-android.zip`** : le projet complet.
  - `www/` : l'appli (fonctionne sans internet).
  - `android/` : le projet Android.
  - `.github/workflows/` : la recette de construction automatique.
  - `docs/index.html` : la politique de confidentialité.
  - `play-store/` : icône, image de présentation, captures d'écran et `fiche-play-store.md` (tous les textes et réponses aux formulaires).
- **`luditeque-upload.jks`** et **`secrets-github.txt`** : ta clé de signature et ses mots de passe. ⚠️ Range-les en lieu sûr, à deux endroits, et ne les mets **jamais** dans le dépôt GitHub.

## Étape 1 : préparer GitHub (10 minutes, une seule fois)

1. Crée un compte gratuit sur **github.com**.
2. Installe **GitHub Desktop** (desktop.github.com) et connecte-toi avec ce compte.
3. Décompresse `luditeque-android.zip` dans tes Documents.

## Étape 2 : compléter la politique de confidentialité

Ouvre `docs/index.html` avec le Bloc-notes et remplace `[TON NOM]` et `[TON ADRESSE E-MAIL]` (deux endroits). Enregistre.

## Étape 3 : envoyer le projet sur GitHub

1. Dans GitHub Desktop : **File → Add local repository**, choisis le dossier `luditeque-android`.
2. Il propose de « create a repository » : accepte, puis **Create repository**.
3. Clique sur **Publish repository**. **Décoche « Keep this code private »** : la page de confidentialité ne peut être hébergée gratuitement que sur un dépôt public. Le code de l'appli sera visible, mais il ne contient aucune donnée personnelle ni la clé de signature.

## Étape 4 : ajouter les 4 secrets

Sur github.com, ouvre ton dépôt `luditeque-android` → **Settings → Secrets and variables → Actions → New repository secret**.

Crée les 4 secrets indiqués dans `secrets-github.txt` (`KEY_ALIAS`, `KEYSTORE_PASSWORD`, `KEY_PASSWORD`, `KEYSTORE_BASE64`), en copiant chaque valeur exactement. Le dernier est une très longue ligne : copie-la en entier.

## Étape 5 : mettre la politique de confidentialité en ligne

Dans le dépôt : **Settings → Pages** → Source « Deploy from a branch » → branche **main**, dossier **/docs** → **Save**.

Une ou deux minutes plus tard, elle est en ligne à l'adresse `https://TON-PSEUDO.github.io/luditeque-android/`. C'est l'adresse à donner à la Play Console.

## Étape 6 : fabriquer le fichier .aab

1. Dans le dépôt, onglet **Actions**. Si GitHub le demande, clique sur le bouton vert pour activer les workflows.
2. Choisis **Construire l'appli Android** à gauche → **Run workflow** → laisse « 1.0 » → **Run workflow**.
3. Patiente 5 à 10 minutes, jusqu'à la coche verte ✅.
4. Clique sur la construction terminée. En bas, dans **Artifacts**, télécharge `luditeque-aab-…` : c'est un zip qui contient **`app-release.aab`**.

Si la construction échoue (croix rouge ❌) : clique dessus, ouvre l'étape en rouge et copie-moi le message d'erreur.

## Étape 7 : premier envoi sur Google Play (test interne)

1. Dans la Play Console, sur l'écran « Créer une release pour tests internes », importe `app-release.aab`.
2. Google propose de gérer la signature de l'appli (« Signature d'application Play ») : **accepte**. La clé que tu as reçue sert alors seulement à *envoyer* les versions. Si elle était perdue un jour, l'assistance Google peut la remplacer.
3. Notes de version : `Première version de test de Luditèque.`, puis **Suivant** → **Enregistrer et publier**.
4. Dans « Testeurs », ajoute ton adresse Gmail et celle de la tablette de ton fils, puis ouvre le lien d'inscription depuis la tablette pour installer l'appli.

C'est aussi le moyen le plus simple de vérifier que tout marche : la 3D, le bouton 🔊, le bouton retour d'Android, la progression conservée. Si la voix ne parle pas : Paramètres Android → Synthèse vocale → installe la voix française.

## Étape 8 : la fiche et les formulaires

Suis `play-store/fiche-play-store.md` : textes, visuels, classification du contenu, public cible, sécurité des données, publicité. Tout y est.

## Étape 9 : le test fermé (12 testeurs pendant 14 jours)

1. **Tester et publier → Tests → Test fermé** → crée un canal, ajoute une version avec le même `app-release.aab` (bouton « Ajouter à partir de la bibliothèque »).
2. Ajoute 12 à 15 testeurs (adresses Gmail), pays : France.
3. Envoie-leur le lien d'inscription : chacun clique sur « Devenir testeur » puis installe l'appli.
4. Il faut **au moins 12 testeurs inscrits 14 jours d'affilée**. Quelqu'un qui se désinscrit avant la fin ne compte pas.

## Étape 10 : la mise en production

Après les 14 jours : **Demander l'accès à la production** sur le tableau de bord, réponds au questionnaire sur le test, puis **Production → nouvelle version** avec le `.aab` → **Envoyer pour examen**. L'examen prend de quelques jours à deux semaines.

## Publier une mise à jour plus tard

1. Remplace `www/index.html` par la nouvelle version (je peux te la fournir).
2. Dans GitHub Desktop : écris un résumé (ex. « Ajout du Dojo des tables ») → **Commit to main** → **Push origin**.
3. Onglet Actions → **Run workflow** avec un nouveau nom de version (« 1.1 »…). Le numéro de version interne augmente tout seul.
4. Envoie le nouveau `.aab` dans la Play Console.
