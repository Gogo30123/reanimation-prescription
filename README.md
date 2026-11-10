# Simulateur de réanimation

Logiciel de formation par simulation en santé : surveillance et prescription en réanimation, sur des **patients fictifs**. Non destiné à un usage clinique.

- **Formateur** : ouvre `formateur.html`, obtient un code de séance, crée des patients et programme des scénarios (hypotension, désaturation, effets de médicaments).
- **Apprenants** : ouvrent la page d'accueil sur leur propre écran et saisissent le code.
- Les patients et scénarios sont enregistrés en fichiers `.json` sur le poste du formateur (dossier « logiciel de simulation en santé »), réutilisables et échangeables.

## Fonctionnement

Le site est statique (GitHub Pages). La liaison entre le formateur et les apprenants passe par une base **Firebase Realtime Database**, interrogée en HTTPS toutes les secondes. La base ne contient que l'état des séances en cours, avec des patients fictifs.

## Mise en place (une fois)

1. **Firebase** : sur https://console.firebase.google.com, créer un projet, puis *Créer > Realtime Database* (emplacement Europe, mode verrouillé). Dans l'onglet *Règles*, coller le contenu de `firebase-regles.json` et publier. Copier l'adresse de la base (onglet *Données*), du type `https://mon-projet-default-rtdb.europe-west1.firebasedatabase.app`.
2. **Configuration** : coller cette adresse dans `config.js`.
3. **GitHub Pages** : *Settings > Pages*, source *Deploy from a branch*, branche `main`, dossier `/ (root)`.

## Limites à connaître

- Toute personne qui connaît un code de séance peut la voir et y écrire : n'utilisez que des patients fictifs.
- Offre gratuite de Firebase : 100 connexions simultanées et 10 Go téléchargés par mois, soit environ 170 séances de 2 h avec 6 apprenants.
- Les séances restent dans la base ; « Nouvelle séance » supprime la précédente. Pour faire le ménage, supprimez le nœud `seances` dans la console Firebase.
