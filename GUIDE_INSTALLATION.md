# Cotisation Famille Karamoko — Guide d'installation

Version : **v.2026-10-09-creation**

C'est **ton application d'administrateur**. Les membres n'ont pas de compte : tu lances un appel quand un événement l'exige (mariage, funérailles, baptême, soutien…), tu fixes la part de chacun, tu enregistres les paiements reçus et tu informes la famille par WhatsApp.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète (un seul fichier) |
| `manifest.json` | Permet l'installation sur le téléphone (PWA) |
| `sw.js` | Ouverture même sans réseau |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Icônes de l'application |

## 1. Mettre en ligne sur GitHub Pages (gratuit)

1. Sur github.com, crée un dépôt, par exemple `cotisation-karamoko`.
2. Dépose tous les fichiers du dossier (bouton **Add file › Upload files**).
3. Va dans **Settings › Pages**, choisis la branche `main` et le dossier `/ (root)`, puis **Save**.
4. Après une à deux minutes, l'adresse s'affiche : `https://<ton-compte>.github.io/cotisation-karamoko/`.

## 2. Installer sur ton téléphone Android

- **Le plus simple** : ouvre l'adresse dans Chrome, menu ⋮ › **Ajouter à l'écran d'accueil**.
- **En APK** : sur pwabuilder.com, colle l'adresse, puis **Package for stores › Android** et télécharge l'APK.

## 3. Premier lancement

1. Crée ton code administrateur à 4 chiffres (il protège l'application si quelqu'un prend ton téléphone).
2. **Réglages › Vos numéros de réception** : saisis tes numéros Orange Money, MTN, Moov, Wave. Ils sont ajoutés automatiquement aux messages WhatsApp.
3. **Membres** : les 19 membres de ton fichier sont déjà là. Complète téléphone, département et part habituelle (fiche de chaque membre), ou importe ton fichier `.ods` complété depuis **Réglages › Liste des membres**.

## 4. Quand un événement survient

1. **Lancer un appel de cotisation** : type, intitulé, date de l'événement, date limite de paiement.
2. Fixe la part de chacun : même montant pour tous, montants habituels, ou ajustement membre par membre (0 = dispensé, décoché = non concerné).
3. **Annoncer au groupe** : WhatsApp s'ouvre avec le message prêt (parts de chacun + tes numéros) ; choisis le groupe familial.
4. Dans l'appel, le bouton vert à côté de chaque nom envoie à la personne **sa part** en message privé.
5. À chaque argent reçu : **Paiement reçu** (ou touche le nom dans l'appel). Un bouton te propose ensuite de remercier la personne.
6. **Point de la collecte** envoie au groupe qui a payé et qui reste.
7. Quand l'argent est remis : **Remise / dépense**, puis **Clôturer**.

Après la date limite, les membres qui n'ont pas tout payé passent **en retard** ; l'accueil les liste avec un bouton **Relancer**.

## 5. Sauvegarde

Les données sont enregistrées **dans le téléphone**. Pour ne rien perdre :

- **Réglages › Télécharger une sauvegarde** régulièrement (fichier `.json`), et **Restaurer** sur un nouvel appareil.
- **Exporter en Excel** produit un tableau proche de ton fichier d'origine (une colonne par appel), plus les feuilles Parts fixées, Paiements et Caisse.

### Sauvegarde en ligne (facultatif, Firebase gratuit)

Pour retrouver les mêmes données sur plusieurs appareils :

1. console.firebase.google.com › **Ajouter un projet** (forfait Spark gratuit).
2. **Firestore Database › Créer une base de données**.
3. **Paramètres du projet** : note le `projectId` et la `apiKey` (clé API Web).
4. Dans Firestore › **Règles**, autorise le document de l'application :

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /familles/karamoko {
      allow read, write: if true;
    }
  }
}
```

5. Dans l'application : **Réglages › Sauvegarde en ligne**, saisis `projectId` et `apiKey`, puis **Connecter**. Ou inscris-les une fois pour toutes dans `index.html` (constante `FIREBASE`, en haut du script) avant de déposer le fichier sur GitHub.

Ces règles laissent le document ouvert à quiconque connaît l'adresse du projet : suffisant pour un usage familial, mais garde le `projectId` pour toi.
