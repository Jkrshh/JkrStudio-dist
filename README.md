# Jkr Studio

> **Ce depot est le canal de mise a jour.** Il ne contient que les archives
> pretes a l emploi - pas la source, pas de donnees.
>
> **[-> Telecharger la derniere version](https://github.com/Jkrshh/JkrStudio-dist/releases/latest)**

Produire, monter et programmer des reels en masse, sur autant de comptes qu'on
veut — sans que deux comptes publient jamais la même chose au même moment.

Trois vues, dans l'ordre où l'on s'en sert :

| Vue | Ce qu'elle fait |
|---|---|
| **Repurpose** | prend un reel et en sort une variante par compte, chacune avec son cadrage, ses couleurs, son encodage et ses métadonnées |
| **Edit Studio** | monte les reels : clips, textes, images, musique, transitions |
| **Batching Studio** | répartit les variantes sur les comptes et dans la semaine, puis les envoie à Buffer qui publie |
| **Statistiques** | quel reel performe, sur quel compte, sur la période de ton choix |

L'interface est en **français et en anglais**, et un **guide complet vit dans
l'outil** : bouton `Guide` en haut à droite. Il s'ouvre tout seul au premier
lancement. Le bouton `Quoi de neuf ?` à côté raconte ce que chaque version a
apporté, et s'ouvre de lui-même après une mise à jour.

---

## Installation

### 1. Python

Jkr Studio a besoin de **Python 3.10 ou plus récent**. Si tu ne l'as pas :

```
winget install --id Python.Python.3.12
```

Coche « Add Python to PATH » si l'installateur te le demande.

### 2. Le dossier

Télécharge l'archive depuis la page
[Releases](https://github.com/Jkrshh/JkrStudio-dist/releases), décompresse-la où tu
veux, et garde le dossier entier — le lanceur s'attend à trouver ses voisins.

### 3. Lancer

Double-clique sur **`Jkr Studio.bat`**. Il vérifie ce qu'il faut, démarre le
serveur local et ouvre ton navigateur.

Laisse la fenêtre noire ouverte : c'est le programme. La fermer arrête l'outil.

### 4. Le reste s'installe tout seul

Au premier lancement, une carte dit ce qui manque et propose de l'installer en
un clic :

| Programme | À quoi il sert | Indispensable |
|---|---|---|
| **ffmpeg** | encode et découpe les vidéos | **oui** — rien ne se rend sans lui |
| **exiftool** | écrit les métadonnées des fichiers produits | non, mais recommandé |
| **yt-dlp** | récupère une musique depuis un lien | non |
| **cloudflared** | donne une adresse publique aux vidéos pour Buffer | non, sauf pour publier |

Rien ne s'installe sans que tu l'aies demandé. Chaque programme vient de son
éditeur, par `winget`, le gestionnaire de paquets fourni avec Windows.

---

## Prise en main

### Repurpose — produire les variantes

1. **Sources** — glisse tes reels dans la zone, ou colle un chemin de dossier
   et clique `Charger`. Coche ceux à traiter.
2. **Réglages** — le nombre de comptes décide du nombre de variantes par
   source. L'intensité règle à quel point elles s'écartent de l'original :
   *Équilibré* est invisible à l'œil et suffit à les séparer.
3. **Aperçu** — rend un extrait d'une seule variante, pour juger avant de
   lancer les cent cinquante autres.
4. **Production** — les fichiers atterrissent dans
   `output/<campagne>/<compte>/`.

**Auto batch** : si tes comptes Buffer sont connectés, coche-les dans cette
section. Les dossiers de sortie porteront leur nom, et le Batching saura quoi
envoyer où sans rien reconfigurer. Range-les en dossiers quand tu en auras
trente : clic droit sur un compte, ou bouton `+ Dossier`.

### Edit Studio — monter

Glisse un clip dans la timeline, puis d'autres à la suite. Chaque clip garde
ses propres réglages : cadrage, filtres, découpe.

- **Textes** — `+ Texte` pose un calque, déplaçable directement dans l'aperçu.
- **Images / stickers** — même principe, mêmes poignées.
- **Musique** — glisse un MP3 sur la carte, ou colle un lien. Puis glisse la
  piste sur la timeline. Le bloc s'affiche à la longueur réelle du morceau,
  même s'il dépasse la vidéo. Les languettes aux coins règlent les fondus.
- **Son** — chaque clip porte son propre volume et son bouton de coupure, dans
  ses propriétés. La musique a les siens.
- **Ciseau** — il coupe **l'élément sélectionné** : un clip en deux clips, un
  texte en deux calques, une image en deux images, une musique en deux blocs
  qui gardent chacun leurs fondus et leur volume.
- **Mise en page du texte** — une largeur de bloc, et le texte s'y replie tout
  seul. Le mode *équilibré* répartit les lignes pour qu'elles fassent à peu
  près la même longueur ; *Ajuster la taille* réduit le corps jusqu'à ce que
  tout tienne. `Réorganiser` répare un texte déjà tapé avec des retours à la
  main.
- **Emojis** — bouton sous le champ de texte : 1900 emojis, recherche en
  français ou en anglais, teintes de peau. Le pack choisi (iOS par défaut) est
  dessiné dans l'aperçu **et** dans l'export.
- **Traduction** — clic droit sur un texte → `Traduire`. 85 langues, l'anglais
  américain et britannique distingués, le ton réglable. Le bouton `Traduire`
  applique tes préférences sans rien demander.
- **Transitions** — une pastille apparaît à la jointure de deux clips.

Un montage peut durer **plus longtemps que ses images** : une musique de deux
minutes sous un reel de cinq secondes continue sur fond noir, et l'export en
tient compte.

Le montage attaché s'applique ensuite à **chaque variante**, avec un hook
différent par compte si tu remplis la banque de hooks.

### Batching Studio — programmer

1. **Connecte Buffer** avec ta clé API, à récupérer sur
   `publish.buffer.com/settings/api`. Elle reste sur ton disque, dans
   `profiles/buffer.json`.
2. **Crée les comptes** depuis les canaux Buffer. Chacun porte son calendrier
   hebdomadaire — tu peux reprendre celui que Buffer connaît déjà.
3. **Règle le pays de chaque compte** — clic droit sur un compte **ou sur un
   canal Buffer** → `Plage horaire et pays`.
   Une plage (« entre 12 h et 12 h 30 ») plutôt qu'une heure fixe, et le
   décalage horaire calculé tout seul : un compte américain publie à midi
   **chez lui**, pas à midi heure de Paris. Un drapeau le rappelle dans la
   liste.
4. **Génère le plan** — chaque variante reçoit un compte et un horaire.
5. **Écris une légende, applique-la à la famille** — clic sur un reel, tape la
   légende, puis `Appliquer à la famille` : tous les reels issus de la même
   source en reçoivent une variante. Même sens, tournure légèrement changée,
   emoji différent mais de même charge. 14 légendes au lieu de 140.
6. **Envoie** — le bouton reste grisé tant qu'une étape manque, et
   `Comment ça marche ?` dit laquelle.

Les packs d'emojis ne sont **pas livrés avec le programme** : le pack choisi se
télécharge une fois (environ 20 Mo) sur ta machine, à ta demande, puis
fonctionne hors ligne. Les illustrations d'Apple lui appartiennent — ce que tu
en fais relève de ton usage.

La traduction passe par DeepL si tu renseignes une clé, sinon par Google puis
Microsoft, sans compte ni configuration. Seul le texte du calque quitte ta
machine — jamais un fichier, jamais un nom de compte.

---

## Ce qui fait la différence

### La rotation entre comptes

Dix comptes qui portent le même nom et publient lundi midi **la même source**,
même retravaillée dix fois, forment un motif que personne ne peut manquer. Les
variantes diffèrent au hash, pas à l'œil.

Le mode *Rotation* garantit qu'à un créneau donné, deux comptes ne publient
jamais la même source — c'est un carré latin, brouillé pour qu'aucun décalage
ne soit lisible. Sur 10 comptes et 14 sources, la propriété est exacte.

Chaque compte porte une **identité de rotation**, interne à l'outil : elle
décide de son ordre et du flottement de ses horaires, et ne touche **jamais**
aux fichiers.

### Le quota Buffer

Buffer compte ses limites en **requêtes**, pas en posts : 100 par quart d'heure
et 250 par jour sur l'offre Essentials. Un post par requête rendrait 150 posts
impossibles en une journée.

Jkr Studio groupe donc les envois — **150 posts partent en 6 requêtes** — et
garde en mémoire ce qu'il a déjà lu. Avant chaque appel, un écran annonce
combien de requêtes l'action va consommer et attend ta réponse.

### Les vidéos et Buffer

Buffer ne reçoit pas les fichiers : ses serveurs vont les **chercher** à une
adresse. Une adresse locale ne veut rien dire pour eux.

Le **tunnel** donne une adresse publique temporaire, le temps de l'ingestion.
Il s'ouvre tout seul au moment d'envoyer, et **seule la route des médias est
exposée** — tout le reste répond `accès refusé` à une requête venue de
l'extérieur.

---

## Mises à jour

Au lancement, l'outil regarde s'il existe une version plus récente sur le canal
de distribution, [JkrStudio-dist](https://github.com/Jkrshh/JkrStudio-dist). Si
oui, un bouton apparaît en haut. L'installation ne part que si tu l'acceptes.

Ce canal ne contient que les archives publiées — c'est ce qui permet au dépôt
de source de rester privé sans qu'aucun jeton n'ait à voyager avec le
programme. Si tu préfères sortir GitHub du chemin, renseigne `MANIFESTE` dans
[`app/version.py`](app/version.py) : l'outil ira lire un simple fichier JSON
(`version`, `url`, `notes`) à l'adresse de ton choix, et c'est celui-là qui
fera autorité.

Tes données ne sont jamais touchées : `profiles`, `input`, `output`, `assets`
et `presets` restent en place. La version précédente est mise de côté dans
`_version_precedente` — si quelque chose tourne mal, elle se restaure.

---

## Questions fréquentes

**Le lanceur s'ouvre et se ferme aussitôt.**
Python ou ffmpeg manque. La fenêtre noire l'écrit avant de se fermer — lance-la
depuis un terminal pour lire le message.

**« Video could not be read from its URL »**
Buffer n'atteint pas la vidéo. Ouvre le tunnel, ou renseigne une adresse
publique dans la carte Buffer.

**Mes comptes Buffer n'apparaissent pas dans le plan.**
Un plan se construit à partir des dossiers d'une campagne. Un compte créé
depuis un canal Buffer n'a de dossier que dans les campagnes lancées **après**,
en auto batch. Le panneau Campagne le dit explicitement.

**Une pastille rouge sur un canal.**
Le canal est déconnecté du réseau social. Tu peux quand même programmer ; la
publication échouera tant que tu ne l'auras pas reconnecté dans Buffer.

**Où sont mes fichiers ?**
`output/<campagne>/<compte>/`. Clic droit sur un compte dans le Batching →
*Ouvrir le dossier de sortie*.

---

## In English

Jkr Studio produces, edits and schedules reels in bulk across any number of
accounts — making sure no two accounts ever publish the same thing at the same
time.

The interface is fully bilingual (`EN` / `FR` at the top right) and a **complete
guide lives inside the tool** — the `Guide` button, which opens by itself on
first launch and covers everything in this README and more.

**Requirements**: Windows, Python 3.10+, and ffmpeg. The tool detects what is
missing on first launch and offers to install it in one click, through the
Windows package manager.

**Getting started**: download the latest release, unzip it, double-click
`Jkr Studio.bat`. Leave the black window open — it is the program.

---

## Vie privée

Rien ne sort de ta machine, sauf ce que tu envoies explicitement à Buffer.

- La clé API Buffer reste dans `profiles/buffer.json`, en local.
- Le serveur n'écoute que `127.0.0.1`.
- Le tunnel, quand il est ouvert, n'expose **que** la route des médias, par
  jeton opaque et pour six heures.
- Aucune télémétrie, aucun compte à créer.
