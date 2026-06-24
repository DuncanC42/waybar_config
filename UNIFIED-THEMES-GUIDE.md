# 🎨 Système de Thèmes Unifié - Guide Complet

Ce système synchronise automatiquement les thèmes de **Hyprland**, **Waybar** et **les wallpapers** !

## 📦 Architecture

```
~/.config/hypr/
├── theme.conf                    # FICHIER À MODIFIER pour changer de thème
├── theme-loader.sh               # Script qui applique tout
├── theme-loader.conf             # Généré automatiquement
│
├── themes/                       # Thèmes Hyprland
│   ├── default.conf              # Bleu/Cyan
│   ├── rouge.conf                # Rouge/Orange
│   └── creme.conf                # Beige/Doré
│
├── waybar/                       # Config Waybar centralisée
│   ├── config                    # Configuration Waybar
│   ├── modules.json              # Modules Waybar
│   ├── style.css                 # Lien symbolique vers le thème actif
│   └── themes/                   # Thèmes CSS Waybar
│       ├── default.css
│       ├── rouge.css
│       └── creme.css
│
└── hyprpaper.conf                # Généré automatiquement par thème

~/.config/waybar/                 # Lien symbolique → ~/.config/hypr/waybar/

~/wallpaper/                      # Wallpapers organisés
├── Celestial-Samurai.jpg         # Default
├── rouge-theme.jpg               # Rouge
└── creme-theme.jpg               # Crème
```

## 🚀 Installation

### Étape 1 : Déplacer Waybar (IMPORTANT)

```bash
# Rendre le script exécutable
chmod +x ~/.config/hypr/install-waybar-centralized.sh

# Exécuter le script
~/.config/hypr/install-waybar-centralized.sh
```

Ce script va :
1. ✅ Sauvegarder votre config Waybar actuelle
2. ✅ Déplacer Waybar dans `~/.config/hypr/waybar/`
3. ✅ Créer un lien symbolique `~/.config/waybar → ~/.config/hypr/waybar`
4. ✅ Préserver votre configuration existante

### Étape 2 : Préparer les wallpapers

```bash
# Créer le répertoire wallpaper
mkdir -p ~/wallpaper

# Copier vos wallpapers
# Pour le thème default (déjà configuré)
# Celestial-Samurai.jpg est déjà mentionné

# Pour le thème rouge
cp /chemin/vers/votre/wallpaper/rouge.jpg ~/wallpaper/rouge-theme.jpg

# Pour le thème crème
cp /chemin/vers/votre/wallpaper/creme.jpg ~/wallpaper/creme-theme.jpg
```

**💡 Astuce :** Si vous n'avez pas de wallpapers spécifiques, vous pouvez utiliser le même wallpaper pour tous les thèmes en modifiant les fichiers de thème.

### Étape 3 : Tester

```bash
# Recharger Hyprland
Super + Shift + R

# Ou manuellement
hyprctl reload
```

## 🔄 Changer de thème

### Méthode simple (recommandée)

1. **Ouvrir le fichier de configuration** :
   ```bash
   nano ~/.config/hypr/theme.conf
   ```

2. **Modifier la ligne THEME** :
   ```bash
   THEME=rouge      # ou creme, ou default
   ```

3. **Appliquer** :
   ```bash
   Super + Shift + T
   ```

### Méthode ultra-rapide (avec alias)

Ajoutez dans votre `~/.bashrc` ou `~/.zshrc` :

```bash
# Alias pour changer de thème rapidement
alias th-default='echo "THEME=default" > ~/.config/hypr/theme.conf && ~/.config/hypr/theme-loader.sh && hyprctl reload'
alias th-rouge='echo "THEME=rouge" > ~/.config/hypr/theme.conf && ~/.config/hypr/theme-loader.sh && hyprctl reload'
alias th-creme='echo "THEME=creme" > ~/.config/hypr/theme.conf && ~/.config/hypr/theme-loader.sh && hyprctl reload'
```

Puis :
```bash
source ~/.bashrc  # ou ~/.zshrc

# Maintenant changez de thème en une commande !
th-rouge
th-creme
th-default
```

## 🎨 Description des thèmes

### 1. Default (Bleu/Cyan) 🔵
- **Hyprland** : Bordures cyan → vert aqua
- **Waybar** : Fond sombre avec accents cyan
- **Wallpaper** : Celestial-Samurai.jpg
- **Style** : Tech, moderne, dynamique

### 2. Rouge (Rouge/Orange) 🔴
- **Hyprland** : Bordures rouge feu → orange vif
- **Waybar** : Fond sombre rouge avec accents orange
- **Wallpaper** : rouge-theme.jpg
- **Style** : Énergique, intense, passion
- **Particularités** : Ombres plus prononcées

### 3. Crème (Beige/Doré) 🟡
- **Hyprland** : Bordures beige → doré
- **Waybar** : Fond brun doux avec accents dorés
- **Wallpaper** : creme-theme.jpg
- **Style** : Élégant, chaleureux, raffiné
- **Particularités** : Arrondis plus prononcés (12px), gaps élargis

## ⚙️ Comment ça marche ?

Le script `theme-loader.sh` est exécuté automatiquement au démarrage de Hyprland et quand vous appuyez sur `Super + Shift + T`. Il :

1. 📖 Lit le thème sélectionné dans `theme.conf`
2. 🎨 Charge le thème Hyprland approprié
3. 🖼️ Crée un lien symbolique vers le CSS Waybar correspondant
4. 🌄 Configure le wallpaper dans `hyprpaper.conf`
5. 🔄 Recharge Waybar et Hyprpaper si nécessaire

## 🛠️ Personnalisation

### Créer votre propre thème

#### 1. Créer le thème Hyprland

```bash
cp ~/.config/hypr/themes/default.conf ~/.config/hypr/themes/montheme.conf
nano ~/.config/hypr/themes/montheme.conf
```

Modifiez les couleurs et ajoutez votre wallpaper :
```bash
$theme_wallpaper = ~/wallpaper/mon-wallpaper.jpg
```

#### 2. Créer le thème Waybar

```bash
cp ~/.config/hypr/waybar/themes/default.css ~/.config/hypr/waybar/themes/montheme.css
nano ~/.config/hypr/waybar/themes/montheme.css
```

Modifiez les variables CSS :
```css
@define-color accent-primary #votre-couleur;
@define-color accent-secondary #votre-autre-couleur;
```

#### 3. Utiliser votre thème

```bash
# Dans theme.conf
THEME=montheme
```

### Modifier un wallpaper de thème existant

Éditez simplement le fichier de thème :

```bash
nano ~/.config/hypr/themes/rouge.conf

# Changez la ligne
$theme_wallpaper = ~/wallpaper/mon-nouveau-wallpaper.jpg
```

## 📝 Raccourcis clavier

| Raccourci | Action |
|-----------|--------|
| `Super + Shift + T` | Recharger le thème (Hyprland + Waybar + Wallpaper) |
| `Super + Shift + R` | Recharger Hyprland complètement |

## 🔍 Dépannage

### Waybar ne change pas de thème

```bash
# Vérifier le lien symbolique
ls -la ~/.config/waybar/style.css

# Recharger Waybar manuellement
killall waybar && waybar &
```

### Le wallpaper ne change pas

```bash
# Vérifier la configuration
cat ~/.config/hypr/hyprpaper.conf

# Recharger hyprpaper
killall hyprpaper && hyprpaper &
```

### Le thème Hyprland ne s'applique pas

```bash
# Vérifier que le thème existe
ls ~/.config/hypr/themes/

# Vérifier le fichier généré
cat ~/.config/hypr/theme-loader.conf

# Recharger complètement
hyprctl reload
```

### Waybar ne démarre plus

```bash
# Vérifier les erreurs
waybar --log-level debug

# Restaurer la sauvegarde
rm -rf ~/.config/waybar
mv ~/.config/waybar.backup.* ~/.config/waybar
```

## 🎯 Avantages du système

✅ **Un seul fichier à modifier** - `theme.conf`
✅ **Synchronisation automatique** - Hyprland, Waybar, Wallpaper
✅ **Changement instantané** - Un raccourci, tout change
✅ **Organisation centralisée** - Tout dans `~/.config/hypr/`
✅ **Sauvegarde automatique** - Votre ancienne config est préservée
✅ **Extensible** - Créez autant de thèmes que vous voulez

## 💡 Conseils Pro

### Adapter le reste du système

Pour une cohérence totale, pensez à :

1. **Terminal (Kitty)** - Créez des thèmes dans `~/.config/kitty/`
   ```bash
   # Dans kitty.conf
   include ./themes/rouge.conf
   ```

2. **GTK Theme** - Utilisez `nwg-look` ou `lxappearance`
   ```bash
   nwg-look
   ```

3. **Curseur** - Changez avec `hyprcursor`

4. **Notifications (Mako)** - Créez des configs par thème
   ```bash
   ~/.config/mako/config.rouge
   ~/.config/mako/config.creme
   ```

### Organisation des wallpapers

```bash
~/wallpaper/
├── themes/
│   ├── default/
│   │   ├── main.jpg
│   │   └── lock.jpg
│   ├── rouge/
│   │   ├── main.jpg
│   │   └── lock.jpg
│   └── creme/
│       ├── main.jpg
│       └── lock.jpg
```

## 📚 Ressources

- **Couleurs** : https://coolors.co/
- **Wallpapers** : https://unsplash.com/, https://wallhaven.cc/
- **Hyprland Wiki** : https://wiki.hyprland.org/
- **Waybar Wiki** : https://github.com/Alexays/Waybar/wiki

---

**Créé avec ❤️ pour une expérience Hyprland harmonieuse**
