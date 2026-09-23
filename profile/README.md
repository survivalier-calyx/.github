<div align="center">

# 🌿 Calyx

**Langage de script simple et modulaire — un seul fichier, aucune dépendance.**

![visitors](https://survivalier.fast-page.org/badge.svg)
![Version](https://img.shields.io/badge/version-1.0.3-brightgreen)
![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20macOS%20%7C%20Windows-lightgrey)
![License](https://img.shields.io/badge/license-MIT-yellow)

</div>

---

## ✨ Présentation

**Calyx** est un langage de script léger interprété par **`calyx.py`**, un unique fichier Python
sans aucune dépendance externe (Python 3.8+ suffit). Il tourne partout : Linux, macOS, Windows.

- 🧩 **Modulaire** : système d'imports simple (`use`) avec modules internes prêts à l'emploi.
- 📦 **Zéro dépendance** : tout tient dans `calyx.py`.
- 🖥️ **Installateur graphique** inclus (`installer.py`), avec version texte (`--cli`).
- 🌍 **Multiplateforme** : Linux, macOS, Windows — et des exécutables autonomes disponibles.

## 🚀 Installation

### Depuis les sources (recommandé pour développer)

```bash
python3 installer.py        # installateur graphique (double-clic sous Windows)
python3 installer.py --cli  # installation en mode texte
```

L'installateur affiche : **Accueil** (bannière, *Installer maintenant* selon l'OS détecté,
*Installation personnalisée*, *Licence*) → **Progression** → **Résultat**.

Structure attendue à côté de `installer.py` :

```
calyx.py  installer.py  LICENSE  assets/  examples/
```

### Exécutable autonome (sans Python requis)

Des scripts de build sont fournis pour générer un exécutable qui embarque son propre
interpréteur Python (via [PyInstaller](https://pyinstaller.org/)) :

| Script | Résultat |
|---|---|
| `build_windows.bat` (à lancer **sur Windows**) | `Calyx-Installer.exe` |
| `build_unix.sh` (Linux / macOS) | `Calyx-Installer` (binaire / `.app`) |
| `build_appimage.sh` (Linux) | `Calyx-Installer-<arch>.AppImage`, portable |
| `build_windows_wine.sh` (Linux, via Wine) | `Calyx-Installer.exe` sans machine Windows |

Voir [`BUILD.md`](./BUILD.md) pour le détail de chaque méthode.

## 🛠️ Utilisation

```bash
calyx programme.cx          # exécuter un script
calyx                       # console interactive
calyx modules                # lister les modules disponibles
calyx install monmodule.cx   # installer un module dans le dossier universel
```

## 📦 Modules

| Instruction | Effet |
|---|---|
| `use test;` | cherche `test.cx` : dossier du script → `./modules/` → dossier universel |
| `use libs/outils;` | sous-dossier (`/` fonctionne aussi sous Windows) |
| `use test as t;` | alias |
| `use #int/sys;` | module interne : `sys.os`, `sys.time()`, `sys.date()`, `sys.env()`, `sys.exit()`... |
| `use #int/color;` | `color.red("x")`, `bold`, `rgb`, `ok/error/warn/info`... |
| `use #int/webserver;` | `webserver.create()`, `app.get/post/static/start` |
| `use #int/math`, `random`, `fs`, `json` | modules bonus |

Dossier universel des modules : `~/.calyx/modules` (Linux/macOS) ·
`%APPDATA%\Calyx\modules` (Windows) — surchargeable via la variable
d'environnement `CALYX_MODULES`. Les noms commençant par `_` dans un module ne
sont pas exportés.

## 📖 Aperçu du langage

```js
let x = 5;  const PI = 3.14;
fn add(a, b = 1) { return a + b; }

if x > 3 { ... } else if x == 3 { ... } else { ... }
while cond { ... }
for item in liste { ... }
for i in range(10) { ... }

let l = [1, 2];
let m = { nom: "Ada" };
m.age = 36;

"Bonjour ${nom}"   // interpolation (guillemets doubles)
'texte brut'       // sans interpolation

class A {
    fn init(n) { self.n = n; }
}
class B extends A {
    fn init(n) { super.init(n); }
}

try {
    throw "oups";
} catch e {
    print(e);
}

// commentaire
/* bloc */
```

Exemple complet dans [`examples/hello.cx`](./examples/hello.cx) :

```js
use #int/color;
use #int/sys;

let nom = "Monde";
print(color.bold(color.green("Bonjour ${nom} !")));
print("Système : ${sys.os} | date : ${sys.date()} | heure : ${sys.time()}");
```

D'autres exemples sont disponibles dans [`examples/`](./examples) (`demo.cx`,
`test.cx`, `web.cx`).

## 🎨 Personnaliser l'installateur

Remplacez `assets/windows.png`, `assets/linux.png`, `assets/macos.png` et
`assets/header.png` par vos propres images (mêmes noms de fichiers). La
licence affichée est le fichier `LICENSE` (MIT par défaut, éditable).

## 🤝 Contribuer

Les contributions sont les bienvenues : ouvrez une *issue* pour signaler un
bug ou proposer une idée, ou une *pull request* directement.

## 📄 Licence

Distribué sous licence [MIT](./LICENSE).
