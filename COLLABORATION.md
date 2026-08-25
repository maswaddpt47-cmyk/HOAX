# Collaboration avec Claude — projet HOAX

Contexte : `index.html` est un outil pédagogique EMI en page unique (HTML/CSS/JS vanilla + `exif-js` via CDN), sans backend, sans build, sans pipeline de déploiement. `README.md` documente les trois modules. Le repo est petit et mono-fichier applicatif : la plupart des changements sont visuels (CSS/layout) ou logiques (règles de scoring des modules Site/E-mail, lecture EXIF).

## Côté Claude

**Patterns récurrents — priorité haute**

1. Ne jamais présenter une explication technique plausible comme un fait : marquer explicitement "hypothèse non vérifiée" dans le code, les commits et les messages, tant qu'aucune preuve (test dans un navigateur, capture, valeur EXIF réelle) ne la confirme.
2. Ne jamais déclarer "c'est réparé" ou "ça marche" sans vérification réelle (ouverture du HTML dans un navigateur, interaction avec l'onglet concerné) — pas une lecture de code qui "devrait marcher". Comme il n'y a ni build ni déploiement ici, "vérifié" veut dire : testé dans le navigateur, pas juste relu.
3. Sur toute demande d'audit ou de correction d'un bug de scoring (règles de détection Site/E-mail) ou de lecture de métadonnées (module Photo), livrer un audit systématique de toutes les règles concernées avant la première correction, pas des trouvailles ponctuelles au fil des questions.
4. Signaler explicitement toute déviation d'une consigne fournie ou toute décision de design prise seul (nom de fichier, structure du README, contenu ajouté), au moment où elle est prise — jamais en note après coup.
5. Poser une question de clarification dès qu'une demande est réellement ambiguë ou sous-spécifiée (fichier cible, "adapte" vs "applique tel quel", contenu de commit/branche non précisé) plutôt que de trancher en silence ou produire un placeholder.
6. Avant toute lecture/modification de fichier en début de session : faire `git pull origin <branche>` (ou `git fetch` + vérifier l'écart avec la branche distante) même si le repo local semble à jour — l'oubli est une cause récurrente d'écrasement de travail. Vérifier `git status`/`git log` et la cohérence entre les instructions de session (branche désignée) et toute autre consigne, et signaler tout conflit avant d'agir, pas après.
7. Après toute reprise de session ou résumé de contexte, relire l'état réel du fichier concerné (`index.html`, `README.md`, etc.) avant de le modifier ou de le renvoyer — ne jamais présumer qu'un correctif précédent est encore en place.
8. Avant de pousser un changement visuel (CSS/layout), vérifier mentalement les interactions connues à risque sur la page — bascule d'onglets (`.section.active`), verdicts colorés, grille responsive à 520px, prévisualisation image — pour ne pas casser un état qui marchait.
9. Utiliser des dates explicites (JJ/MM ou JJ/MM/AAAA) plutôt que des termes relatifs ("hier", "aujourd'hui", "la semaine dernière") dans les messages — la perception du temps de Claude vient du contexte injecté en début de session, pas d'une horloge live.
10. Ne pas systématiser les tests navigateur sur des changements simples et directement vérifiables par lecture du code (libellés, couleurs, texte du README) — ça consomme du temps pour rien. Réserver la vérification en navigateur aux cas où la logique change réellement (règles de scoring, parsing EXIF, comportement des onglets).

**Règle de branche / push**

11. **Pull systématique en début de session** : avant toute lecture ou modification, faire `git pull` (ou `git fetch` + comparaison) sur la branche de travail.
12. **Push vers `main`** : si l'utilisateur ou les instructions de session demandent explicitement de pousser sur `main`, le faire. Par défaut, ce repo fonctionne avec des branches dédiées par session (`claude/...`) fournies par les instructions de session — dans ce cas, ces instructions priment et le push se fait sur la branche désignée, pas sur `main`, sauf demande explicite contraire au moment considéré. Dans tous les cas, informer clairement de la branche réellement utilisée pour chaque push.

**Bonnes pratiques à maintenir**

13. Continuer à demander l'avis avant toute action à fort impact (push sur `main`, réécriture de `README.md`/`index.html` en profondeur) et exécuter vite dès validation reçue.
14. Continuer à privilégier la preuve concrète (rendu navigateur réel, contenu de fichier relu) sur la déduction théorique pour tout diagnostic.

## Côté utilisateur

**Patterns récurrents — priorité haute**

1. Donner le contexte et les tentatives déjà faites dès le premier message ("ça affichait ça hier", "j'ai déjà testé X") plutôt qu'après coup.
2. Pour un bug visuel ou de scoring "bizarre", ajouter une description précise du symptôme (quel onglet, quelle entrée testée, quel résultat obtenu vs attendu) plutôt qu'une formule vague.
3. Signaler explicitement en début de message tout changement fait hors session (renommage de branche, edit direct sur GitHub, fichier renommé/déplacé).
4. Pour les demandes ouvertes ("plus clair", "améliore le module email"), préciser le critère de succès attendu.
5. Donner un retour de validation réelle après test ("testé dans Chrome, ça marche" / "l'onglet Photo ne s'affiche pas") — sans ce signal, Claude ne peut pas recouper ses inférences sur un projet sans CI/déploiement.
6. Utiliser des dates explicites (JJ/MM) plutôt que des termes relatifs en retour.

**Bonnes pratiques à maintenir**

7. Continuer à valider court et vite sur le travail bien cadré ("ok", "pousse-le") — ça marche bien tant que la portée est claire.
8. Continuer à recadrer immédiatement dès qu'une mauvaise direction est repérée.
