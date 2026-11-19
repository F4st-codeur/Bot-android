# BlitzBot — bot automatique pour Block Blitz (Android 11+)

Service d'accessibilité qui : capture l'écran → lit la grille 8x8 et les 3 pièces →
calcule le meilleur enchaînement (toutes permutations/positions + heuristique) → fait glisser la pièce.

## Compiler l'APK (sans rien installer) — GitHub Actions
1. Crée un dépôt GitHub (privé) et pousse ce dossier :
   git init && git add . && git commit -m "BlitzBot" && git branch -M main
   git remote add origin https://github.com/<toi>/BlitzBot.git && git push -u origin main
2. Onglet **Actions** → workflow « Build APK » → attends ~3 min.
3. Télécharge l'artefact **BlitzBot-apk** (zip contenant app-debug.apk) et installe-le sur le téléphone.

Alternative : ouvrir le dossier dans Android Studio → Build → Build APK(s).

## Utilisation
1. Ouvre BlitzBot → « Ouvrir les réglages d'accessibilité » → active **BlitzBot**.
   Android 13+ : si l'option est grisée → Paramètres → Applis → BlitzBot → ⋮ → *Autoriser les paramètres restreints*.
2. Lance une partie **Classic** dans Block Blitz.
3. Panneau flottant (en haut à gauche) → **Cadrer** :
   trace un rectangle pile sur la grille 8x8, puis un autre sur toute la zone des 3 pièces.
4. **▶ Jouer**. Les 1ers coups posent une pièce au centre pour mesurer le décalage doigt/pièce
   (« Calage OK ✔ » quand c'est bon), puis le bot joue normalement.

## Si ça ne marche pas
- **Debug** : points verts = cases vues pleines, cadres jaunes = pièces (avec leur taille lignes x colonnes),
  violet = coup prévu. Si les points verts sont faux → ajuste le « seuil de luminosité ».
- Les tailles affichées des pièces sont fausses → règle « Taille des pièces en attente » (ex. 0.5) au lieu de 0 (auto).
- Pièces lâchées trop tôt / pas prises → augmente « Durée du glissé ».
- Le bot lit l'écran avant la fin des animations → augmente la « Pause après chaque coup ».

## Fichiers
- `Solver.java` : moteur (pur Java, testable sur PC)
- `ScreenReader.java` : lecture des couleurs de la capture
- `BotService.java` : boucle du bot, captures, gestes, apprentissage du décalage
- `CalibrationView.java` / `DebugView.java` : calques à l'écran
