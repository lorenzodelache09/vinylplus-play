<div align="center">
  <img src="assets/header.png" alt="VinylPlus Play" width="720">
  <p><strong>Le lecteur musical local de l'écosystème VinylPlus.</strong></p>
  <p>
    <img src="https://img.shields.io/badge/Windows-10%2F11-22D3EE?style=flat-square" alt="Windows 10/11">
    <img src="https://img.shields.io/badge/Electron-45-A855F7?style=flat-square" alt="Electron 45">
    <img src="https://img.shields.io/badge/React-19-8B5CF6?style=flat-square" alt="React 19">
    <img src="https://img.shields.io/badge/TypeScript-strict-3B2558?style=flat-square" alt="TypeScript strict">
    <img src="https://img.shields.io/badge/Licence-MIT-F4F0FA?style=flat-square" alt="Licence MIT">
  </p>
</div>

---

## À propos

**VinylPlus Play** est un lecteur musical **desktop, local et hors ligne** pour Windows. Il lit vos propres fichiers audio sans les déplacer, sans les réencoder et sans envoyer de données sur Internet.

Il reprend le langage visuel VinylPlus : palette violette, accents cyan, disque vinyle animé et interface sombre par défaut. Le thème clair utilise une variante blanche du même en-tête.

> Les captures ci-dessous proviennent d'une exécution réelle de l'application avec un dossier de démonstration temporaire de 5 fichiers WAV générés localement. Aucune donnée factice n'est incluse dans le logiciel : la bibliothèque, l'historique et les statistiques affichés sont bien ceux du profil utilisateur.

## Sommaire

- [Galerie fonctionnelle](#galerie-fonctionnelle)
- [Fonctionnalités](#fonctionnalités)
- [Installation](#installation)
- [Démarrage développeur](#démarrage-développeur)
- [Architecture](#architecture)
- [Données et confidentialité](#données-et-confidentialité)
- [Raccourcis clavier](#raccourcis-clavier)
- [Limites et feuille de route](#limites-et-feuille-de-route)
- [Licence](#licence)

---

## Galerie fonctionnelle

### Premier lancement

![Premier lancement](docs/screenshots/01-premier-lancement.png)

Au premier démarrage, l'application guide l'utilisateur : choix d'un dossier musical, analyse locale puis accès à la bibliothèque. L'annulation de la sélection ne marque pas l'assistant comme terminé et affiche un message explicite. Le bouton **Continuer sans importer** reste disponible.

### Accueil

![Accueil](docs/screenshots/02-accueil.png)

La page d'accueil affiche le nombre de morceaux, albums et artistes indexés, quatre cartes de statistiques calculées à partir de l'historique réel, les écoutes récentes, les ajouts récents, les albums récents et les favoris. Le disque vinyle tourne tandis que le logo VPP reste fixe au centre.

### Bibliothèque

![Bibliothèque](docs/screenshots/03-bibliotheque.png)

La bibliothèque liste tous les morceaux avec filtres **Genre**, **Année** et **Format**, des pastilles de synthèse par format et un tableau triable : titre, artiste, album, date d'ajout, nombre d'écoutes, durée, favori et menu d'actions.

### Albums

![Albums](docs/screenshots/04-albums.png)

Vue en grille des albums avec pochette, artiste, année et nombre de titres. Survolar une pochette révèle un bouton de lecture qui lance le premier titre de l'album avec la file d'attente correspondante.

### Artistes

![Artistes](docs/screenshots/05-artistes.png)

Chaque artiste dispose d'une carte avec sa pochette, son nombre d'albums et son nombre de titres. Cliquer sur une carte déclenche une recherche contextuelle et ouvre la vue **Morceaux** filtrée sur cet artiste.

### Morceaux

![Morceaux](docs/screenshots/06-morceaux.png)

Vue dédiée à tous les titres. Elle réutilise le même tableau que la bibliothèque et affiche les résultats filtrés lorsqu'une recherche contextuelle est active.

### Recherche contextuelle

![Recherche depuis une carte artiste](docs/screenshots/21-recherche-artiste.png)

Le titre de la vue devient `Résultats pour « Artiste A »`. VinylPlus Play n'affiche pas de champ de recherche global dans la barre de titre : la recherche est déclenchée depuis les cartes artiste/album et les filtres de la bibliothèque.

### Playlists

![Playlists](docs/screenshots/07-playlists.png)

Création, renommage, duplication, suppression, ajout multicritère, réorganisation par glisser-déposer et export M3U. La colonne de gauche liste les playlists, la zone de droite affiche leur contenu et les actions disponibles.

### Ajout de morceaux à une playlist

![Ajouter des morceaux](docs/screenshots/17-ajouter-morceaux.png)

La fenêtre d'ajout permet de chercher dans la bibliothèque, de cocher plusieurs titres puis de les ajouter à la playlist sélectionnée.

### Favoris

![Favoris](docs/screenshots/08-favoris.png)

Les titres marqués d'un cœur sont regroupés ici. Le bouton favori est disponible dans le tableau des titres et dans la barre de lecture permanente.

### Historique d'écoute

![Historique](docs/screenshots/09-historique.png)

Chaque écoute réelle est enregistrée avec sa date, sa durée écoutée et le titre associé. L'historique alimente directement les statistiques ; aucune donnée n'est inventée.

### Lecture en cours

![Lecture en cours](docs/screenshots/12-lecture-en-cours.png)

La vue **Now Playing** affiche la pochette agrandie, les métadonnées du fichier (album, année, format, débit), la progression, les contrôles, le visualiseur spectrum temps réel, les marqueurs de piste, la file « à suivre » et un encart paroles honnête lorsqu'aucune parole synchronisée n'est disponible. Le fond flou est généré depuis la pochette quand l'option est active.

### Mode vinyle

![Mode vinyle](docs/screenshots/13-mode-vinyle.png)

Le mode vinyle remplace la pochette carrée par un disque animé avec bras de lecture. Le logo VPP reste centré sur le label, y compris pendant la rotation.

### Égaliseur 10 bandes

![Égaliseur](docs/screenshots/14-egaliseur.png)

L'égaliseur applique un traitement temps réel via la Web Audio API : 10 bandes, activation/bypass, presets (Flat, Rap, Trap, Hip-Hop, Rock, Pop, Jazz, Classical, Electronic, Bass Boost) et enregistrement de configurations personnalisées.

### File d'attente

![File d'attente](docs/screenshots/15-file-dattente.png)

Le panneau latéral montre les titres à suivre, le titre actif, le retrait d'un élément et le vidage de la file. Il s'ouvre depuis la barre de lecture et se ferme avec `Échap`.

### Édition des métadonnées

![Modification des métadonnées](docs/screenshots/16-modification-metadonnees.png)

Le formulaire modifie titre, artiste, artiste d'album, album, genre, année, numéros de piste/disque et couverture. Les tags sont réécrits directement dans le fichier via ffmpeg en `-c copy` : **aucun réencodage audio**. La base est resynchronisée après l'écriture.

### Statistiques

![Statistiques](docs/screenshots/10-statistiques.png)

Toutes les cartes et tous les graphiques sont dérivés de la table `history` : temps total d'écoute, morceaux écoutés, morceaux uniques, taille de la bibliothèque, podium artiste/album/titre, genres dominants, activité des 30 derniers jours et titres les plus écoutés.

### Export Wrapped

![Export Wrapped](docs/screenshots/19-wrapped-export.png)

Le bouton **Exporter Wrapped (PNG)** génère une image 1080 × 1350 prête à partager.

![Exemple de Wrapped généré](docs/screenshots/22-wrapped-image.png)

### Paramètres

![Paramètres](docs/screenshots/11-parametres.png)

Cinq sections : bibliothèque musicale (dossiers, analyse, nettoyage des fichiers manquants), apparence (thème, disposition, couleur d'accentuation, animations, fond dynamique), audio (volume, aléatoire, répétition, égaliseur), notifications et démarrage, enfin à propos. Tout est enregistré localement et conservé au redémarrage.

### Thème clair

![Thème clair](docs/screenshots/18-theme-clair.png)

Le thème clair remplace le header `black.png` par `white.png`, conserve la sidebar et adapte les couleurs de texte, de fond et de logo.

### Analyse de la bibliothèque

![Analyse de la bibliothèque](docs/screenshots/20-analyse-bibliotheque.png)

L'analyse récursive affiche la progression, le fichier courant et les erreurs éventuelles par dossier. Un dossier illisible n'invalide pas le reste de la bibliothèque.

---

## Fonctionnalités

- Navigation complète : Accueil, Bibliothèque, Albums, Artistes, Morceaux, Playlists, Favoris, Historique, Statistiques et Paramètres.
- Barre de lecture permanente : pochette, titre/artiste, précédent/play/suivant, progression interactive, lecture aléatoire, répétition (`off` / `all` / `one`), volume, mute réversible, file d'attente et égaliseur.
- Moteur audio réel basé sur `HTMLAudioElement` et la Web Audio API : lecture/pause, file dynamique, historique, gestion d'erreurs, notifications Windows et raccourcis globaux.
- Import de dossiers et analyse récursive avec extraction des pochettes et durées. Les fichiers manquants sont signalés, jamais supprimés automatiquement.
- Filtres par genre, année et format, tris, favoris et recherche contextuelle depuis les cartes album/artiste.
- Édition des tags directement dans les fichiers audio, sans réencodage.
- Assistant de premier lancement et persistance de tous les réglages.

### Fonctionnalités avancées

- **Playlists complètes** : création, renommage, duplication, suppression, ajout multicritère, retrait, réorganisation et export M3U.
- **Égaliseur 10 bandes** temps réel avec presets et configurations personnalisées sauvegardées.
- **Now Playing immersif** : fond dynamique, mode vinyle, visualiseur spectrum, marqueurs et file « à suivre ».
- **Statistiques réelles** et export Wrapped PNG.
- **Thèmes sombre/clair**, 4 dispositions, 7 couleurs d'accentuation, animations et fond dynamique configurables.

---

## Installation

### Version grand public

Téléchargez l'un des exécutables publiés dans la section **Releases** GitHub :

| Fichier | Description |
| --- | --- |
| `VinylPlus-Play-0.1.0-x64-portable.exe` | Version portable, aucune installation requise. |
| `VinylPlus-Play-0.1.0-x64-setup.exe` | Installateur NSIS assisté : dossier d'installation, raccourcis Bureau/menu Démarrage, licence MIT, écran de fin avec lancement immédiat. |

Les exécutables sont **non signés**. Selon la configuration de Windows Defender SmartScreen, cliquez sur **Plus d'informations** puis **Exécuter quand même** lors du premier lancement.

### Depuis les sources

```bash
npm install
npm run dev       # Vite + Electron avec rechargement à chaud
npm run build     # vérification TypeScript + build du renderer dans dist/
npm start         # lance l'application compilée
```

### Compilation Windows

```bash
npm run build:exe        # => release/VinylPlus-Play-0.1.0-x64-portable.exe
npm run build:installer  # => release/VinylPlus-Play-0.1.0-x64-setup.exe
npm run assets:installer # régénère les BMP/ICO de l'installateur
npm run icon             # régénère l'icône applicative
```

Une workflow GitHub Actions (`.github/workflows/release.yml`) reconstruit les deux artifacts sur `windows-latest`. Elle se déclenche manuellement ou lors d'un tag `v*` et publie automatiquement les exécutables dans une release.

---

## Démarrage développeur

```text
electron/               Processus principal : IPC, base SQLite, scan, protocole media://
  main.mjs              Fenêtre, raccourcis globaux, handlers IPC, notifications
  db.mjs                Schéma SQLite, requêtes, statistiques, purges
  library.mjs           Analyse récursive, métadonnées, cache des pochettes
  metadata.mjs          Écriture des tags via ffmpeg (-c copy)
  preload.mjs           API typée exposée sous window.vinyl

src/                    Renderer React
  components/           TitleBar, Sidebar, PlayerBar, TrackTable, EqualizerPanel, ...
  views/                Home, Browse, Playlists, NowPlaying, Statistics, Settings
  store/AppContext.tsx  État global, file de lecture, aléatoire, réglages
  audio/AudioEngine.ts  Web Audio, gain, analyseur, égaliseur
  api.ts                Client IPC typé

assets/                 Icône, logo texte, en-têtes clair/sombre
build/                  Habillage NSIS (BMP, ICO, licence)
docs/screenshots/       Captures de cette documentation
scripts/                Génération des assets d'installation
```

---

## Données et confidentialité

- Base de données locale : `%APPDATA%\VinylPlus Play\vinylplus.db` en mode WAL.
- Pochettes mises en cache dans `%APPDATA%\VinylPlus Play\covers`.
- Protocole `media://` limité aux pistes indexées, au dossier des pochettes et aux couvertures choisies manuellement ; il renvoie les en-têtes CORS et `Accept-Ranges` nécessaires à la lecture et au seek.
- Aucun compte, aucun télémétrie, aucun service distant requis.
- L'intégration avec VinylPlus DJ reste optionnelle et n'est pas une dépendance de fonctionnement.

---

## Raccourcis clavier

| Raccourci | Action |
| --- | --- |
| `Espace` | Lecture / pause hors champ de saisie. |
| `Ctrl + Alt + P` | Lecture / pause globale. |
| `Ctrl + Alt + →` | Morceau suivant. |
| `Ctrl + Alt + ←` | Morceau précédent. |
| `Ctrl + Alt + U` | Ouvrir la lecture en cours. |
| Touches multimédia | Lecture/pause, suivant, précédent. |
| `Échap` | Fermer une modale ou le panneau file d'attente. |

---

## Feuille de route

Non implémenté dans cette version :

- crossfade et gapless ;
- mini-player ;
- import/export M3U complet aller-retour ;
- dossiers intelligents, détection de doublons et ReplayGain ;
- Bass Boost, Reverb, Compressor, Limiter et sélection du périphérique de sortie ;
- MusicBrainz, Vinyl Carousel, Listening Sessions, Album Journal, Smart Shuffle, Mood Playlists ;
- plugins/API et intégration VinylPlus DJ.

---

## Licence

Distribué sous licence [MIT](LICENSE). Le même texte est intégré à la page de licence de l'installateur Windows.
