# Kit de vérification — EMI

Outil pédagogique d'éducation aux médias et à l'information (EMI), en une seule page HTML autonome (`index.html`), sans dépendance serveur.

## Modules

- **Site** — analyse une adresse (URL) collée par l'utilisateur : détection de TLD suspects, usurpation de noms de domaines officiels/médias, IP à la place d'un nom de domaine, caractères trompeurs (`@`, `xn--`), raccourcisseurs de liens, etc. Fournit ensuite des outils de vérification manuelle (WHOIS, recherche d'avis) et des liens de signalement officiels (Cybermalveillance.gouv.fr, Pharos, Phishing Initiative, Signal Arnaques).
- **E-mail** — analyse un texte de mail collé (objet + corps) et une adresse d'expéditeur optionnelle : formulations d'urgence, demandes d'informations sensibles, salutations génériques, incohérence entre marque citée et domaine réel de l'expéditeur. Tout le traitement se fait dans le navigateur, rien n'est envoyé sur un serveur.
- **Photo** — lecture des métadonnées EXIF d'une image choisie localement (date, appareil, GPS, logiciel) via [exif-js](https://cdnjs.cloudflare.com/ajax/libs/exif-js/2.3.0/exif.min.js), avec liens vers des outils de recherche d'image inversée (Google Images, TinEye, Yandex Images, Google Lens) à utiliser manuellement. L'image n'est jamais transmise à un serveur.

Chaque module affiche un verdict (score + signaux détaillés) plutôt qu'un simple oui/non, pour montrer le raisonnement derrière l'analyse.

## Fonctionnalités pour l'animation d'atelier

- **Exemples pré-chargés** — boutons "Exemple" sur les modules Site et E-mail pour lancer une analyse sur un cas préparé sans taper en live devant un groupe.
- **Mode atelier** — case à cocher dans l'en-tête : le verdict et les signaux sont floutés jusqu'au clic sur « Révéler l'analyse », pour laisser les participants argumenter avant la correction.
- **Fiche imprimable** — bouton « Imprimer cette fiche » sur les résultats Site et E-mail (formulaires et liens externes masqués à l'impression).
- **Réinitialiser** — bouton dédié sur chaque module pour enchaîner rapidement les cas.
- **Fonctionnement 100% hors-ligne** — `exif-js` est vendorisé dans `vendor/exif.js` (plus de dépendance à un CDN), utile en salle sans wifi fiable.

## Utilisation

Ouvrir `index.html` directement dans un navigateur — aucune installation ni build nécessaire. Le dossier `vendor/` doit rester à côté de `index.html` (bibliothèque EXIF embarquée).

## Avertissement

Ces modules donnent des indices, pas des certitudes. En cas de doute sérieux — surtout si des données bancaires ou personnelles ont été transmises — contacter l'organisme concerné par un canal connu et signaler le contenu aux plateformes officielles.
