# Mainalingua — Jeux interactifs de vocabulaire espagnol

## 📌 Introduction

Tout ce qui concerne les jeux interactifs (Vocabulario, Tarjetas didácticas, Memorama, Relaciona la imagen, Escribe la palabra, Sopa de letras, Completa la palabra) est géré ici, sur GitHub — pas directement dans Wix. Wix se contente d'afficher ce contenu via un lien (le composant HTML pointe vers l'URL de ce site).

Concrètement, ce dépôt contient trois éléments :

| Élément | Rôle |
|---|---|
| `vocabulario.html` | Le moteur du jeu — le code qui génère l'affichage. **Ne jamais modifier sauf en cas de besoin technique avancé.** |
| `data.json` | La liste de tous les thèmes, tous les mots, et le chemin de leur image. **C'est le fichier que vous modifierez le plus souvent.** |
| `images/` | Le dossier contenant toutes les images, organisées dans un sous-dossier par thème. |

Pour ajouter ou corriger un mot, une image, ou un thème entier, **il ne faut jamais toucher au code** (`vocabulario.html`). Seuls `data.json` et le dossier `images/` doivent être modifiés.

## ⚠️ Règle n°1 — Toujours travailler dans la branche `edit`

La branche `main` doit toujours rester une version stable et fonctionnelle du site. **Ne faites jamais de modification directement sur `main`.**

La branche `edit` a déjà été créée à cet effet. Avant toute modification :

1. En haut à gauche de la page du dépôt, cliquez sur le menu déroulant qui affiche le nom de la branche actuelle
2. Sélectionnez **`edit`**
3. Faites vos modifications uniquement à l'intérieur de cette branche
4. Une fois certain·e que tout fonctionne (testez l'URL du jeu après modification), ouvrez une **Pull Request** de `edit` vers `main`, puis validez-la (« Merge »)

Cela permet de toujours pouvoir revenir à une version stable de `main` en cas d'erreur dans `edit`.

## ⚠️ Règle n°2 — Respecter exactement l'orthographe et la syntaxe

**Ceci est essentiel : le site ne fonctionnera pas si cette règle n'est pas respectée.**

Le jeu fonctionne en faisant correspondre trois éléments **caractère pour caractère** :
1. Le nom du thème écrit dans l'URL (`?theme=NomDuTheme`)
2. La clé du thème dans `data.json`
3. Le nom du fichier image dans le dossier `images/`

Si l'un de ces trois éléments contient une faute de frappe, un espace en trop, une majuscule différente, ou un accent manquant, **le site ne trouvera pas l'image ou le thème, et rien ne s'affichera** (l'utilisateur verra une erreur ou une page vide).

**Règles précises à respecter :**

- Le nom du thème dans `data.json` doit être identique à celui utilisé dans l'URL, y compris les majuscules (ex : `"Frutas"`, pas `"frutas"`)
- Le nom de fichier d'une image doit toujours suivre ce format : le mot espagnol, première lettre en majuscule, espaces remplacés par des underscores `_`, sans accents si possible, suivi de `.png` (ex : `El_bombero.png`)
- Le chemin de l'image dans `data.json` doit correspondre **exactement** à l'emplacement réel du fichier dans `images/` (ex : `images/Oficios/El_bombero.png`)
- Ne jamais laisser d'espace au début ou à la fin d'un mot ou d'un nom de fichier
- Toujours vérifier qu'il n'y a pas de virgule manquante ou de guillemet mal fermé dans `data.json` après une modification (un fichier JSON mal formé empêche TOUT le site de fonctionner, pas seulement le thème concerné)

**Avant de valider (commit), relisez toujours votre modification une seconde fois.**

## ➕ Comment ajouter un nouveau thème

1. Allez dans le dossier `images/`
2. Créez un nouveau sous-dossier au nom exact du thème (ex : `images/Oficios/`). Pour cela, créez un nouveau fichier avec le chemin complet, par exemple `images/Oficios/.gitkeep` — GitHub créera automatiquement le dossier
3. Uploadez toutes les images de ce thème dans ce sous-dossier, en respectant le format de nom de fichier (voir Règle n°2 ci-dessus)
4. Ouvrez `data.json`, ajoutez une nouvelle entrée avec le nom exact du thème et la liste de ses mots :
```json
"Oficios": [
  {"word": "El bombero", "image": "images/Oficios/El_bombero.png"},
  {"word": "El doctor", "image": "images/Oficios/El_doctor.png"}
]
```
5. Vérifiez que la virgule entre chaque thème dans `data.json` est bien présente (sauf après le tout dernier thème du fichier)
6. Commit vos changements dans la branche `edit` (voir Règle n°1)

## ➕ Comment ajouter un mot à un thème existant

1. Uploadez l'image dans le sous-dossier correspondant de `images/` (ex : `images/Frutas/`), en respectant le format de nom de fichier
2. Ouvrez `data.json`, trouvez le thème concerné, ajoutez une ligne à l'intérieur de ses crochets `[ ]` :
```json
{"word": "El mango", "image": "images/Frutas/El_mango.png"}
```
3. Vérifiez la virgule entre cette ligne et la ligne précédente
4. Commit vos changements

## ✏️ Comment modifier l'image d'un mot existant

**Option A — Garder le même nom de fichier (recommandé, le plus simple) :**
1. Allez dans le sous-dossier du thème concerné dans `images/`
2. Cliquez sur l'image à remplacer, puis uploadez une nouvelle image avec exactement le même nom de fichier
3. Aucune modification de `data.json` n'est nécessaire

**Option B — Utiliser un nouveau nom de fichier :**
1. Uploadez la nouvelle image avec un nouveau nom
2. Supprimez l'ancienne image (icône poubelle sur la page du fichier)
3. Mettez à jour le champ `"image"` correspondant dans `data.json` avec le nouveau chemin

## ✏️ Comment corriger l'orthographe d'un mot

1. Ouvrez `data.json`
2. Trouvez le mot concerné dans le thème correspondant
3. Modifiez uniquement le champ `"word"` (ne touchez pas au champ `"image"` sauf si le nom de fichier doit changer aussi)
4. Commit vos changements

## 🔗 Format de l'URL pour afficher un thème

```
https://[votre-pseudo].github.io/[nom-du-depot]/vocabulario.html?theme=NomDuTheme
```

Exemple pour Frutas :
```
https://wessala.github.io/Mainalingua/vocabulario.html?theme=Frutas
```

⚠️ Le texte après `?theme=` doit correspondre **exactement**, majuscules incluses, à la clé utilisée dans `data.json`.

## 🧩 Intégration dans Wix

Dans Wix, le composant HTML (HtmlComponent) de la page concernée est configuré en mode **« Website address »** (et non « Code »), avec l'URL ci-dessus collée directement. Pour changer le thème affiché sur une page Wix, il suffit de modifier le paramètre `?theme=` dans cette URL — aucune modification de code n'est nécessaire dans Wix.

## ✅ Checklist avant chaque commit

- [ ] Le nom du thème est identique partout (URL, `data.json`, dossier `images/`)
- [ ] Le nom de chaque fichier image suit le format exact (majuscule initiale, underscores, `.png`)
- [ ] Le chemin `"image"` dans `data.json` correspond exactement à l'emplacement réel du fichier
- [ ] Toutes les virgules et guillemets de `data.json` sont corrects
- [ ] Le travail a été fait dans la branche `edit`, pas dans `main`
- [ ] L'URL du jeu a été testée après modification pour confirmer que tout s'affiche correctement
