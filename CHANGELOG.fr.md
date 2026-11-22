# Journal des modifications

*[English version → CHANGELOG.md](CHANGELOG.md)*

Toutes les modifications notables de X5 Studio sont listées ici. Le format suit [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) et la numérotation suit le [versionnage sémantique](https://semver.org/lang/fr/).

## [1.8.2] — 2026-11-22

### Ajouté
- Deux captures d'écran dans `docs/screenshots/` (onglet Rapide et onglet Filtre), affichées dans README.md (anglais) et LISEZMOI.md (français).

### Corrigé
- Le moniteur SysEx affichait les longs messages avec « (194 o) », une unité française restée dans l'interface anglaise. Il indique désormais « 194 bytes », traduit dans chaque langue (« 194 octets » en français).

## [1.8.1] — 2026-11-22

### Corrigé
- **Varier** produisait des changements trop petits pour être entendus : avec l'ampleur par défaut, le cutoff du filtre bougeait d'environ 3 crans sur 99. Le curseur **Ampleur** indique maintenant l'écart maximal en % de la plage de chaque réglage (±12 % par défaut, jusqu'à ±40 %, affiché à côté du curseur), et le cutoff pèse un peu plus.
- Les valeurs en butée (un niveau à 99, une couleur à 0) ne restent plus bloquées : elles rebondissent, si bien que chaque tirage change vraiment chaque réglage coché.
- La case **Timbre** ne modifie plus « Couleur ← vélocité », qui ne s'entend qu'en jouant plus ou moins fort.

### Ajouté
- Une ligne de résumé sous les boutons Varier indique ce qui a bougé, les plus grands changements d'abord (par exemple « Cutoff 70→81 · Couleur 0→9 »).

## [1.8] — 2026-11-22

### Ajouté
- **Inspiration** (onglet Rapide, dans les deux vues) : choisis une famille (Nappe, Basse, Lead, Clavier, Cloche, Percussif, Texture / FX ou Surprise) et un son neuf est créé de zéro. Chaque famille a ses règles (familles de multisounds, formes d'enveloppe, filtre, vibrato, mode Simple ou Double, effets adaptés), pour que le résultat reste jouable. **Un autre** relance la même famille ; **Son précédent** revient en arrière (une étape d'annulation).
- Les nouveaux sons reçoivent un **nom court** (10 caractères, la limite du X5), composé à partir de listes de mots dans la langue de l'interface. Ces listes sont dans les fichiers de langue (`names`), avec l'adjectif après le nom en français, italien et espagnol.
- **Documentation du code :** une présentation au début du script (« How this program works » : le tampon central de 164 octets, le chemin d'un réglage jusqu'au X5, la carte des sections) et une explication du rôle de chaque section. Tous les commentaires du code sont désormais en anglais.

### Corrigé
- L'afficheur du nom coupait le 10e caractère.

## [1.7.1] — 2026-11-22

### Modifié
- **Clavier de test dans une fenêtre flottante**, ouverte avec le bouton **🎹** de l'en-tête, déplaçable par sa barre de titre et redimensionnable. Fermée par défaut, elle mémorise son état. Les touches de l'ordinateur jouent toujours des notes quand elle est fermée. Le moniteur SysEx et le journal se placent maintenant en bas de l'écran et remontent quand le clavier est ouvert.
- **Thème unique (Atelier).** Le thème sombre **Nuit** et son bouton ☾ / ☀ sont désactivés ; le thème reste en commentaire dans le code pour pouvoir être réactivé.

## [1.7] — 2026-11-22

### Ajouté
- **Numéros de page du X5 sur les cartes** (par exemple `4A–4E`), qui correspondent aux pages d'édition Program du X5 (PROG → EDIT). Ils suivent le mode d'oscillateur (Simple/Batterie ou Double) et l'oscillateur édité ; quand les deux oscillateurs sont liés, les deux séries de pages s'affichent.

### Modifié
- **Effets :** le placement (page 20A en mode Double) et les balances sec/effet des deux effets (page 20B) sont maintenant réunis dans une seule carte **Placement & balance**, visible dans les deux vues.
- Le réglage Sinus/Triangle des effets s'appelle désormais **Wave Shape** en anglais, comme sur l'écran du X5.

## [1.6] — 2026-11-22

### Ajouté
- **Éditeur d'effets détaillé** (onglet Effets, vue Complet) : tous les réglages de chacun des 47 types d'effet, d'après les tables « Effect Parameter » du manuel Korg. Le temps de réverb s'affiche en secondes, les vitesses de LFO en Hz, les retards en ms et l'égaliseur en dB.
- Pour chaque effet : interrupteur **Actif**, **balance sec/effet** L et R (liées par défaut) et **modulation dynamique** (source : joystick, aftertouch, pédales, EG du VDA ; intensité −15…+15).
- Choisir un type d'effet charge maintenant des valeurs de départ adaptées et active l'effet.

### Modifié
- Les réglages d'effet, changement de type compris, sont envoyés au X5 sous forme de son complet (Program Dump), au plus toutes les 150 ms pendant un geste. L'ordre des Parameter Change d'effet du X5 ne suit pas le manuel : passer par le son complet est la voie fiable.
- Disposition de l'onglet Effets : placement en haut, les deux effets côte à côte.

### Corrigé
- Annuler ou rétablir un changement Actif/coupé d'un effet n'était pas renvoyé au X5.

## [1.5.2] — 2026-11-22

### Modifié
- **Mêmes onglets dans les deux vues.** L'onglet Contrôleurs disparaît : ses réglages Aftertouch et Joystick se trouvent maintenant en bas de l'onglet **Modulation** (ex-« Hauteur & LFO »), en vue Complet seulement.

## [1.5.1] — 2026-11-22

### Modifié
- **L'anglais devient la langue de base de l'interface**, écrite directement dans `x5studio.html`.
- **Le français, l'italien, l'espagnol et l'allemand passent dans un dossier `lang/`**, à raison d'un fichier par langue (`lang/fr.js`, `it.js`, `es.js`, `de.js`). Chaque fichier contient les textes de l'interface et l'aide « ? ». Corriger ou ajouter une langue ne demande plus de toucher au code de l'application.
- Au premier lancement, la langue suit toujours celle du navigateur, et le dernier choix reste mémorisé.
- Si le dossier `lang/` est absent, l'appli continue de fonctionner en anglais et le signale dans le journal.

Aucun changement de fonctions ni de comportement MIDI.

## [1.5] — 2026-11-22

### Ajouté
- Interrupteur **Essentiel / Complet**, à gauche des onglets, mémorisé d'une séance à l'autre. **Essentiel** (par défaut) garde les réglages principaux : multisounds, enveloppes du filtre et de l'ampli, cutoff, couleur, sensibilité à la vélocité, vibrato, LFO de filtre, type des effets. **Complet** affiche tous les paramètres du Program, comme avant. Les deux vues modifient le même son ; basculer de l'une à l'autre n'envoie rien au X5.
- En vue Essentiel sont masqués : l'onglet Contrôleurs, les curseurs détaillés des temps et niveaux d'EG (les éditeurs d'enveloppe restent), le suivi de clavier, les interrupteurs de sensibilité −/0/+, le Pitch EG, le panoramique et les envois C/D, le retard de l'osc 2, Hold, ainsi que la synchro et le suivi de clavier des LFO.

## [1.4] — 2026-11-21

Première publication sur GitHub.

### Ajouté
- Bouton **● Édition / ○ Jeu** dans l'en-tête. Il indique si le X5 est en mode édition, et un clic rend la main au synthé par un passage en mode Program (`F0 42 3n 36 4E 02 00 F7`).
- Le X5 est remis automatiquement en mode Program (jeu) à la fermeture ou au rechargement de la page.
- **Retour en édition :** après une sortie, le réglage suivant envoie un passage en Prog Edit, attend 100 ms, puis renvoie le son entier, pour que le synthé et l'éditeur restent identiques.
- **Reprise après un réglage refusé (NAK) :** l'appli remet le X5 en édition et lui renvoie le son, en ignorant les refus répétés que le synthé envoie souvent.
- L'appli suit les changements de mode faits sur la face avant du X5. **Détecter** demande aussi au synthé son mode actuel (Mode Request).
- Le moniteur SysEx traduit les messages de changement, de demande et de réponse de mode.

## [1.3] — 2026-11-21

### Ajouté
- Thème **Atelier** (clair, inspiré de l'esthétique des modules Eurorack) : cartes façon façade de module avec vis, boutons blancs, une couleur par section (oscillateurs, filtre, ampli, hauteur & LFO, effets).
- Thème **Nuit** (l'ancien style sombre), à basculer avec le bouton ☾ / ☀, et mémorisé.

### Corrigé
- **Pitch EG :** « Niveaux ← vélocité » et « Temps ← vélocité » étaient inversés.
- **Envois bus C / D** inversés.
- **Mode Batterie :** les numéros de kits sont maintenant justes (0–1 = kits utilisateur, 8–15 = kits ROM 1–8).
- Le remplissage des enveloppes pouvait disparaître sur certaines pages.

Ces corrections viennent des tables MIDI officielles du X5DR transcrites dans le projet [x5dr-editor](https://github.com/Baylo1/x5dr-editor) de Mark Baylis.

## [1.2] — 2026-11-21

### Ajouté
- Interface en **français, anglais, italien, espagnol et allemand**, avec un sélecteur à drapeaux. Au premier lancement, l'appli prend la langue du navigateur.
- Aide traduite dans les cinq langues.

### Modifié
- Distribution sous **licence MIT**.

## [1.1] — 2026-11-21

### Ajouté
- **Moniteur SysEx :** fenêtre déplaçable et redimensionnable qui affiche chaque message envoyé et reçu, traduit en clair, avec copie, pause et filtre des notes.
- **Délai d'envoi :** pause réglable après chaque message SysEx (0 à 150 ms, 20 ms par défaut). Les messages partent dans l'ordre, en tenant compte du temps réel de transmission MIDI.
- Messages plus clairs quand le navigateur bloque l'accès MIDI, avec un bouton pour réessayer.
- Mention de copyright.

## [1.0] — 2026-11-21

### Ajouté
- Éditeur Web MIDI en un seul fichier pour les Programs des Korg **X5 / X5D / X5DR / 05R/W** (Chrome / Edge).
- Tous les paramètres d'un Program : oscillateurs (340 multisounds, recherche par famille), VDF, VDA, Pitch EG, LFO, aftertouch et joystick, ainsi que le type et le placement des effets.
- Enveloppes à modifier à la souris, 10 macros, **Varier** (variations aléatoires), annuler/rétablir, comparaison **A/B**.
- Édition en direct (Parameter Change) ou envoi manuel (Program Dump), lecture du X5, écriture dans un emplacement mémoire.
- Clavier à l'écran et clavier de l'ordinateur, phrases de test, rejeu automatique après chaque réglage.
- Librairie : lire ou envoyer une banque de 100 sons, ouvrir et enregistrer des fichiers `.syx`, garder des sons dans le navigateur.

### Corrigé (par rapport au panel Ctrlr 05R/W dont il s'inspire)
- Les valeurs négatives partaient en octets MIDI invalides.
- Les sensibilités à la vélocité et au clavier ont leurs trois états (−/0/+).
- Le suivi de clavier a ses quatre modes (Off/Bas/Haut/Tout).

[1.8.2]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.8.2
[1.8.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.8.1
[1.8]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.8
[1.7.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.7.1
[1.7]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.7
[1.6]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.6
[1.5.2]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5.2
[1.5.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5.1
[1.5]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5
[1.4]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.4
