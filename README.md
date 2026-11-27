<p align="center"><img src="logo.jpg" width="320" alt="MKW Remote Together"></p>

<h1 align="center">MKW-remote-together-v0.7</h1>

<p align="center">
  <b>Mario Kart World sur PC avec Steam Remote Play Together, pour jouer en écran partagé avec des amis à distance.</b><br>
  <b>Mario Kart World on PC with Steam Remote Play Together, for split-screen with friends who are not in the room.</b>
</p>

<p align="center">
  <a href="https://github.com/sinedgiveaways/mkw-recomp/releases/download/v0.1.15-rpt1/mkw-recomp-0.1.15-rpt1-windows-x64.zip"><b>⬇ Télécharger / Download : MKW-remote-together-v0.7 (Windows x64, zip)</b></a>
</p>

---

## Source du build / Build source

Ce build vient de **https://github.com/adriadam10/mkw-recomp** (recompilation statique de Mario Kart World pour
Linux et Windows). Il est basé sur sa version **0.1.15**, avec en plus le support de Steam Remote Play Together
(branche `steam-rpt` du fork [sinedgiveaways/mkw-recomp](https://github.com/sinedgiveaways/mkw-recomp)).
Tout le mérite de la recompilation revient à son auteur et à ses contributeurs.

This build comes from **https://github.com/adriadam10/mkw-recomp** (a static recompilation of Mario Kart World for
Linux and Windows). It is based on its **0.1.15** release, plus Steam Remote Play Together support (the `steam-rpt`
branch of the [sinedgiveaways/mkw-recomp](https://github.com/sinedgiveaways/mkw-recomp) fork).

> **Rien du jeu n'est inclus.** Il faut votre propre copie de Mario Kart World, extraite de votre propre console
> (`exefs/` et `romfs/`, ou un fichier `.nup` / `.nx`). Version 1.0.0 ou 1.8.0.
> *Nothing of the game is included. You need your own dump of the game.*

## Contenu du zip / What is in the zip

Le zip (`mkw-recomp-0.1.15-rpt1-windows-x64.zip`, 217 Mo) contient le dossier `mkw-recomp/` avec les éléments
ci-dessous. Les quatre DLL sont aussi dans le dossier [`dll/`](dll/) de ce dépôt : si l'une manque à côté de
`mkw.exe`, copiez-la depuis ce dossier.

| Fichier | Rôle |
|---|---|
| `mkw.exe` | le lanceur et le jeu |
| `steam_api64.dll` | la bibliothèque de Steam (Steamworks SDK 1.65), **indispensable à Remote Play Together** |
| `SDL3.dll`, `libopus-0.dll`, `libusb-1.0.dll` | bibliothèques d'entrée, d'audio et USB |
| `setup/` | les outils qui préparent le jeu sur votre machine |

SHA-256 de `steam_api64.dll` : `e6d9bafb9a41e42fba7b21553db49f8719027af3f0deb23ff86cfc44d60e776d`
(c'est le fichier officiel de Valve, vérifiable avec `certutil -hashfile steam_api64.dll SHA256`).

## Comment ça marche / How it works

Remote Play Together est la fonction de Steam qui diffuse la fenêtre et le son du jeu à vos amis. Leurs manettes
(ou claviers) deviennent les joueurs 2, 3, 4… du jeu en écran partagé, jusqu'à 8 joueurs selon le mode. Ils n'ont
besoin que de Steam, de l'application Steam Link, ou d'un navigateur avec un lien invité : **pas du jeu**.

Le jeu se déclare à Steam sous l'identité d'un jeu de votre bibliothèque qui supporte Remote Play Together
(par défaut RetroArch, App ID `1118310`, gratuit). Vos amis voient donc le nom de ce jeu dans Steam.

### Ce qu'il faut / Requirements

- Windows 10 ou 11 x64, processeur x86-64 avec AVX2, GPU Vulkan 1.3, environ 30 Go libres, 16 Go de RAM conseillés.
- Steam installé, lancé et connecté sur le PC qui fait tourner le jeu (l'hôte).
- Le jeu RetroArch (ou un autre jeu de votre bibliothèque avec Remote Play Together) installé dans Steam.
- Votre dump de Mario Kart World.

### Installation

1. Téléchargez le zip depuis ce [lien de téléchargement](https://github.com/sinedgiveaways/mkw-recomp/releases/download/v0.1.15-rpt1/mkw-recomp-0.1.15-rpt1-windows-x64.zip) et dézippez-le dans un dossier.
2. Lancez `mkw.exe`, ouvrez **Game files**, choisissez votre dump puis appuyez sur **Set up**.
   La première préparation est longue (le jeu est compilé sur votre machine). Ensuite, **Play**.

### Activer Remote Play Together

`steam_api64.dll` est déjà à côté de `mkw.exe` : il n'y a rien à télécharger.

1. **L'App ID.** Dans `mkw.ini` (à côté de `mkw.exe`) :

   ```ini
   [steam]
   steam_appid = 1118310
   ```

   Le même réglage existe dans le menu : `F1` > General > Steam Remote Play Together > Steam App ID
   (pris en compte au démarrage suivant).

2. **Lancer depuis Steam** (nécessaire pour que les manettes de vos amis arrivent dans le jeu) :
   - installez RetroArch dans Steam ;
   - clic droit > Propriétés > Général > Options de lancement, puis saisissez le chemin de `mkw.exe` entre
     guillemets suivi de `%command%`, par exemple :

     ```
     "C:\Users\vous\Downloads\mkw-recomp\mkw.exe" %command%
     ```

   - appuyez sur Jouer dans Steam. Pour revenir au vrai RetroArch, videz les options de lancement.

   Lancé directement depuis son dossier, le jeu accepte les invitations, mais Steam ne lui donne pas les manettes
   des invités. Un raccourci « jeu non-Steam » ne fonctionne pas non plus.

3. **Inviter.** Dans le jeu, menu `F1` > General > **Steam Remote Play Together** :
   - **Invite friends** ouvre la liste d'invitation de Steam ;
   - **Copy guest link** copie un lien à envoyer à n'importe qui (navigateur ou Steam Link, sans compte ami).

   En choisissant le multijoueur local (2 à 4 joueurs) avec moins de manettes que de joueurs, le jeu propose
   d'ouvrir la liste d'invitation. Quand les invités ont rejoint et appuyé sur un bouton de leur manette,
   choisissez de nouveau le mode.

Dans `logs/mkw.log`, la ligne `steam: running as App ID ...; Remote Play Together ready` confirme que tout est prêt.

### Bon à savoir

- Les invités ne peuvent pas ouvrir le menu (`Esc`, `F1`, `F10`, `F11` restent à l'hôte).
- Un invité sans manette obtient un joueur à la première touche pressée (WASD, Espace, Maj…).
- Les réglages Steam Input du jeu choisi comme App ID changent le résultat. RetroArch (`1118310`) et
  Streets of Rage 4 (`985890`) ont fonctionné pour les manettes de l'hôte et des invités.
- Le jeu lit l'App ID au démarrage : un changement demande un redémarrage.
- Sous Linux Wayland, si les invités voient « Steam not launched with -pipewire », lancez Steam avec
  `steam -pipewire`. (Ce build ne fournit que le zip Windows.)
- **Mises à jour :** l'écran d'accueil propose les nouvelles versions de `adriadam10/mkw-recomp`, qui n'ont
  **pas** Remote Play Together. Désactivez la vérification dans **Settings > Menu > Check for updates**, sinon
  l'installation d'une de ces versions remplacerait ce build.

### État des tests

Le support de Remote Play Together a été testé contre la bibliothèque Steam 1.65 et une simulation de Steam
(démarrage, invités qui arrivent et partent, manette d'invité en joueur 2, clavier d'invité en joueur 3, lien
invité, erreurs). La documentation du projet indique qu'une vraie session avec des amis via Steam n'avait pas
encore été faite au moment de son écriture.

### Vérifier le build

Le zip est celui de la release `v0.1.15-rpt1` du fork `sinedgiveaways/mkw-recomp`, republié tel quel sous
le nom MKW-remote-together-v0.7. Documentation détaillée : `docs/guides/remote-play.md` dans la branche `steam-rpt-main` du fork.

---

## English summary

1. Download the zip from the [download link](https://github.com/sinedgiveaways/mkw-recomp/releases/download/v0.1.15-rpt1/mkw-recomp-0.1.15-rpt1-windows-x64.zip), unpack it, run `mkw.exe`, point **Game files** at your own
   dump and press **Set up**.
2. `steam_api64.dll` is already next to `mkw.exe`. Set `steam_appid = 1118310` (RetroArch) under `[steam]` in `mkw.ini`.
3. In Steam, install RetroArch and set its launch options to `"<path>\mkw.exe" %command%`, then press Play in Steam.
4. In the game press `F1` > General > Steam Remote Play Together > **Invite friends** (or **Copy guest link**).
   Friends join with Steam, Steam Link or a browser. Their controllers become players 2, 3, 4.
5. Turn off **Settings > Menu > Check for updates**: upstream releases do not include Remote Play Together.

Source of the build: https://github.com/adriadam10/mkw-recomp (based on 0.1.15).
