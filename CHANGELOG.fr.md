# Journal des modifications

*[English version → CHANGELOG.md](CHANGELOG.md)*

Toutes les modifications notables de X5 Studio sont listées ici. Le format suit [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) et la numérotation suit le [versionnage sémantique](https://semver.org/lang/fr/).

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

[1.5.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5.1
[1.5]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5
[1.4]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.4
