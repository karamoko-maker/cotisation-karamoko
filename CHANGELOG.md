# CHANGELOG — Cotisation Famille Karamoko

## v.2026-10-09-creation — 9 octobre 2026

Première version, créée à partir du fichier `COTISATION_FAMILLE.ods` et sur le modèle de La Roue.

**Principe** : application de l'administrateur seul. Les cotisations se font par événement (mariage, funérailles, baptême, soutien, autre), l'admin fixe la part de chaque membre et la date limite.

- Écran de verrouillage par code administrateur à 4 chiffres (haché SHA-256)
- 19 membres repris du fichier (nom corrigé : VAKARAMOKO KARAMOKO RACHID), avec téléphone, département, part habituelle, statut actif/désactivé
- Appels de cotisation : type, intitulé, date de l'événement, date limite, personne concernée, message, part fixée par membre (même montant pour tous, montants habituels, ajustement individuel, dispense)
- Roue de l'appel : un segment par membre, coloré selon payé / partiel / à payer / en retard
- Paiements reçus enregistrés par l'admin, liés à un appel ou répartis automatiquement sur les appels les plus anciens (excédent en crédit)
- Passage automatique « en retard » après la date limite
- Caisse : solde, entrées, sorties (remises, dépenses) liées ou non à un appel ; journal horodaté de toutes les actions
- WhatsApp en un geste : annonce au groupe, message privé avec la part de chacun, point de la collecte, relances, remerciements ; les numéros Mobile Money de l'admin sont ajoutés aux messages
- Export Excel (Récapitulatif, Parts fixées, Paiements, Caisse), sauvegarde/restauration JSON, import de la liste des membres depuis un fichier .ods/.xlsx
- Sauvegarde en ligne facultative via Firebase Firestore (REST), avec file d'attente hors ligne et contrôle de version pour éviter tout écrasement silencieux
- Thème clair/sombre, identité La Roue (or, indigo, terre cuite, vert, motif wax)
- PWA : manifest.json, sw.js, icônes ; guide d'installation GitHub Pages + APK via PWABuilder
