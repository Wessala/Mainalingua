# Mainalingua — Interactive Spanish Vocabulary Games

## 📌 Overview

This repository contains all the files for the interactive Spanish vocabulary games of the **Mainalingua** online language school. The site is hosted on **GitHub Pages** and embedded in Wix via an HTML component in "Website address" mode.

### Global Architecture

```
Wix (page "Activités")
    └── HtmlComponent "Website address"
            └── https://wessala.github.io/Mainalingua/themes.html
                    └── (click on a theme)
                            └── index.html?theme=ThemeName
                                    └── fetch data.json
                                            └── images in image/ThemeName/
```

### Main Files

| File | Role |
|---|---|
| `themes.html` | Home page — lists all available themes automatically from `data.json` |
| `index.html` | Game engine — dynamically loads data for the selected theme |
| `data.json` | Central database — contains all words and image paths per theme |
| `image/` | Folder containing all images organized in theme subfolders |
| `.github/workflows/generate_data_json.yml` | Automatic workflow — updates `data.json` on every image upload |

---

## ⚠️ Rule #1 — Always work in the `edit` branch

**Never make changes directly on the `main` branch.** The `main` branch is the stable, public version of the site.

**Procedure before any modification:**

1. At the top left of the repository, click on the branch dropdown menu
2. Select **`edit`**
3. Make all your changes in `edit`
4. Test that everything works correctly
5. Open a **Pull Request** from `edit` to `main` and validate it (Merge)

---

## ⚠️ Rule #2 — Strict naming conventions

**The site will not work if these conventions are not followed.**

The system automatically matches three elements:

1. **The theme name** in `data.json`
2. **The folder name** in `image/`
3. **The `?theme=` parameter** in the URL

These three elements must be **identical character by character**, including uppercase letters and underscores.

### Conventions for theme names and folder names

| ✅ Correct | ❌ Incorrect |
|---|---|
| `Animales_de_compañía` | `animales de compañia` |
| `El_mar` | `El mar` |
| `Frutas` | `frutas` |
| `Descripciones_físicas` | `Descripciones fisicas` |

- **Spaces** are replaced by **underscores** `_`
- The **first letter** is always **uppercase**
- **Accents** are preserved in folder names and theme names

### Conventions for image file names

| ✅ Correct | ❌ Incorrect |
|---|---|
| `La_manzana.png` | `la_manzana.png` |
| `El_plátano.png` | `El_platano.PNG` |
| `Frío.png` | `frio.png` |
| `El_trabajador_de_la_construcción.png` | `El trabajador.png` |

- First letter **uppercase**
- Spaces replaced by **underscores** `_`
- **Accents preserved**
- Extension always in **lowercase** `.png`
- The article (El/La/Los/Las) is part of the file name when it exists
- **No suffix** `_Maina` or `_Paco` in the file name

---

## 🤖 Automatic Workflow — Generating `data.json`

A GitHub Actions workflow automatically generates `data.json` every time images are added to the `image/` folder.

**What the workflow does:**
1. It scans all subfolders in `image/`
2. For each folder (= one theme), it lists all `.png` files
3. It generates a JSON entry with the word (file name without `.png`, underscores replaced by spaces) and the image path
4. It commits and pushes `data.json` automatically

**What the workflow preserves:**
- Themes whose images are hosted on Wix (URLs containing `wixstatic.com`) — like Frutas — are not overwritten

**The workflow triggers automatically when:**
- You push files to the `image/` folder

**To run it manually:**
1. Go to the **Actions** tab of the repository
2. Click on **"Générer data.json automatiquement"**
3. Click **"Run workflow"**

---

## ➕ How to add a new theme

1. **Prepare your images** with the correct file names (see conventions above)
2. **On GitHub**, create a subfolder in `image/` with the exact theme name:
   - Create a new file with the path `image/ThemeName/.gitkeep` to initialize the folder
3. **Upload all images** for the theme into that subfolder
4. **The workflow triggers automatically** and updates `data.json`
5. **Verify** that the theme appears correctly on `themes.html`

**Example:** to add the theme `Animales_del_mar`:
- Create `image/Animales_del_mar/.gitkeep`
- Upload `El_pez.png`, `La_tortuga.png`, etc. into `image/Animales_del_mar/`
- The workflow automatically generates the entry in `data.json`

---

## ✏️ How to edit an existing word

The word displayed in the game corresponds to the **image file name** (without `.png`, underscores → spaces).

To change a word:
1. Rename the image file with the correct new name
2. The old file can be deleted
3. The workflow updates `data.json` automatically on the next push

---

## 🖼️ How to replace an image

**Option A — Same file name (recommended):**
1. Upload the new image with **exactly the same file name**
2. No changes to `data.json` needed

**Option B — New file name:**
1. Upload the new image with the new name
2. Delete the old image
3. The workflow updates `data.json` automatically

---

## 🗑️ How to delete a word or a theme

**Delete a word:**
1. Delete the corresponding image file in its theme folder
2. The workflow updates `data.json` automatically

**Delete an entire theme:**
1. Delete the theme folder in `image/`
2. The workflow removes the theme from `data.json` automatically
3. The theme disappears automatically from `themes.html`

---

## 🎨 Images — Generation Rules (OpenAI)

Images are generated using the OpenAI `gpt-image-1` API with Google Colab.

### Gender rules
| Article | Character |
|---|---|
| La / Las | **Maina** (female character) |
| El / Los | **Paco** (male character) |

### Available poses
- **Maina** : `Maina1.png`, `Maina2.png`, `Maina4.png` (alternate randomly)
- **Paco** : `Paco1.png`, `Paco2.png`, `Paco4.png` (alternate randomly)
- ⚠️ `Maina3.png` and `Paco3.png` do not exist

### Themes with characters (Maina/Paco appear in the image)
Adjetivos, Emociones, Sentimientos, Oficios, Profesiones, Descripciones físicas, La familia, Rutinas, Saludos, Modales, Me gusta no me gusta

### Themes without characters (Maina/Paco style used as visual reference only)
All other themes (objects, animals, concepts, food, etc.)

### Plural rule
- A word ending in `-s` must show **multiple elements** in the image
- Example: `Las_fresas.png` → multiple strawberries, not just one

---

## 🔗 Important URLs

| Page | URL |
|---|---|
| Themes page | `https://wessala.github.io/Mainalingua/themes.html` |
| Games — Frutas | `https://wessala.github.io/Mainalingua/index.html?theme=Frutas` |
| Games — Other theme | `https://wessala.github.io/Mainalingua/index.html?theme=ThemeName` |
| JSON data | `https://wessala.github.io/Mainalingua/data.json` |

### Wix Integration
The HTML component in Wix is configured in **"Website address"** mode with the URL:
```
https://wessala.github.io/Mainalingua/themes.html
```
No changes in Wix are needed to add new themes — everything is managed from GitHub.

---

## ✅ Checklist before each commit

- [ ] I am in the **`edit`** branch, not `main`
- [ ] The folder name in `image/` follows the naming conventions (uppercase, underscores, accents)
- [ ] Image file names follow the naming conventions (uppercase, underscores, `.png`)
- [ ] The GitHub Actions workflow ran successfully (green ✅ icon in the Actions tab)
- [ ] The theme displays correctly on `themes.html`
- [ ] Images display correctly in the games
- [ ] Once validated, the Pull Request from `edit` to `main` has been merged

---

## 🎮 Available Games

Each theme automatically offers 7 activities:

| Game | Description |
|---|---|
| **Vocabulario** | Hover over images to discover the words |
| **Tarjetas didácticas** | Flashcards with "I knew it / Review" system |
| **Memorama** | Memory game — find matching pairs of identical images |
| **Relaciona la imagen** | Match each image to the correct word (4 pairs at a time) |
| **Completa la palabra** | Fill in the missing letters of the word |
| **Sopa de letras** | Word search in a 12×12 grid |
| **Escribe la palabra** | Write the word matching the image |