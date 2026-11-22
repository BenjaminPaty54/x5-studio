# X5 Studio

*[English version → README.md](README.md)*

Éditeur de sons pour **Korg X5, X5D, X5DR et 05R/W**, qui fonctionne directement dans le navigateur (Chrome ou Edge) grâce à Web MIDI. Il permet de créer ou de retoucher un Program (un son, ou « patch ») et de l'entendre aussitôt sur le synthé, sans le vieux logiciel d'édition des années 1990.

L'application tient en un fichier HTML, `x5studio.html`, accompagné d'un dossier `lang/` qui contient les traductions. Rien à installer, aucune connexion Internet nécessaire. Garde le dossier `lang/` à côté de `x5studio.html` : sans lui, l'appli fonctionne quand même, mais uniquement en anglais.

L'interface existe en **français, anglais, italien, espagnol et allemand** : clique sur un drapeau en haut à droite. Au premier lancement, l'application prend la langue du navigateur. L'anglais est intégré à la page ; les autres langues viennent du dossier `lang/` (voir [Traductions](#traductions)).

Deux vues : **Essentiel** (les réglages principaux, pour fabriquer ou retoucher un son vite) et **Complet** (tous les paramètres du Program), à basculer à gauche des onglets.

Deux thèmes : **Atelier** (clair, inspiré de l'esthétique des modules Eurorack) et **Nuit** (sombre), à basculer avec le bouton ☾ / ☀.

© 2026 Benjamin PATY (BenjaminPaty54)

---

## Ce qu'il faut

- Un Korg X5, X5D, X5DR ou 05R/W (ils partagent le même moteur et le même format SysEx).
- Une interface MIDI reliée à l'ordinateur, branchée dans les deux sens :
  - MIDI OUT du synthé → MIDI IN de l'interface ;
  - MIDI OUT de l'interface → MIDI IN du synthé.
- **Google Chrome** ou **Microsoft Edge** (Safari ne gère pas le MIDI dans les pages web).
- Python 3 pour lancer un petit serveur local. Il est présent sur la plupart des Mac.

## Réglages sur le synthé

1. **GLOBAL → MIDI Filter → EX = ENA** : indispensable, sinon aucun message SysEx ne passe.
2. **Memory Protect Program = OFF** : seulement si tu veux écrire des sons dans la mémoire.
3. Note le **canal MIDI global**. L'application sait aussi le trouver toute seule.

## Lancer l'application

Il faut ouvrir la page dans son propre onglet, servie par un mini-serveur local. Ouverte depuis un aperçu de fichier, ou parfois par simple double-clic, le navigateur bloque l'accès au MIDI.

```
cd dossier/contenant/x5studio.html
python3 -m http.server 8000
```

Ouvre ensuite **http://localhost:8000/x5studio.html** dans Chrome et accepte l'accès aux appareils MIDI. Laisse le Terminal ouvert pendant l'utilisation.

## Premiers pas

1. En haut de la page, choisis la **sortie** et l'**entrée** MIDI de ton interface, puis clique **Détecter** : le synthé et son canal sont trouvés automatiquement.
2. Mets le synthé en mode **PROG** sur le son à retoucher, puis clique **⇩ Lire le X5**.
3. Modifie le son. En mode **Direct**, chaque réglage part tout de suite vers le synthé.
4. Pour garder le résultat, choisis un emplacement (A00 à A99) et clique **Écrire**.

> ⚠️ Avant d'expérimenter, sauvegarde tes sons : onglet **Librairie → Lire la banque du X5 → Télécharger la banque .syx**.

## L'interface

| Zone | À quoi elle sert |
|---|---|
| **Rapide** | Dix macros (Brillance, Attaque, Relâche, Vibrato, Épaisseur…) qui agissent sur plusieurs paramètres à la fois. Chaque geste ajoute ou retire par rapport au son actuel, puis la macro revient au centre. Le bouton **Varier** propose de petites variations aléatoires. |
| **Oscillateurs** | Mode Simple / Double / Batterie, choix parmi les 340 multisounds (recherche, familles, tirage au hasard), octave, niveau, panoramique, envois. |
| **Filtre (VDF)** et **Ampli (VDA)** | Enveloppes modifiables à la souris, sensibilité à la vélocité et au clavier. Tu peux éditer l'oscillateur 1, l'oscillateur 2, ou les deux à la fois (« liés »). |
| **Hauteur & LFO** | Pitch EG, LFO de filtre, vibrato. |
| **Contrôleurs** | Aftertouch et joystick. |
| **Effets** | Choix des deux effets et de leur placement. |
| **Librairie** | Lire ou envoyer une banque de 100 sons, ouvrir et enregistrer des fichiers `.syx`, garder ses sons favoris dans le navigateur. |

Outils toujours visibles :

- **Clavier** à l'écran ou clavier de l'ordinateur (rangée du milieu = touches blanches), **▶ Tester** pour jouer une note, un accord ou un arpège, option **Rejouer à chaque réglage**.
- **↶ / ↷** pour annuler ou rétablir (Ctrl/⌘+Z), **A/B** à maintenir appuyé pour réentendre le son d'origine, et **Revenir à l'origine**.
- **● Édition / ○ Jeu** : indique si le synthé est en mode édition. Un clic lui rend la main (mode Program) ; c'est aussi fait automatiquement quand tu fermes la page. Si le X5 refuse un réglage (par exemple après un passage par sa face avant), l'appli le remet en édition et lui renvoie le son.
- **SysEx** : petite fenêtre qui affiche chaque message envoyé ↑ ou reçu ↓, traduit en clair avec ses octets. Le curseur **Délai** ajoute une pause après chaque message SysEx (20 ms par défaut).
- Double-clic sur un curseur pour retrouver sa valeur d'origine, molette pour un réglage fin.

## Limites actuelles

- **Programs uniquement.** L'application édite les sons individuels (Programs). Elle ne crée ni ne modifie les **Combinations** (Combis), qui superposent ou répartissent plusieurs Programs des banques pour former des ensembles plus riches. Une Combi qui utilise un Program retouché en profitera, mais la Combi elle-même s'édite encore sur le synthé.
- **Réglages Global, mode Multi et banque GM du X5DR** : non pris en charge.
- **Effets** : on choisit le type des deux effets et leur placement, mais pas leurs réglages internes (durée de réverbération, temps de retard…). Ces réglages sont conservés tels quels et repartent avec le son.
- **Kits de batterie** : on peut choisir un kit en mode Batterie, mais pas modifier son contenu.
- **Écriture en mémoire** : le format de la commande d'écriture a été déduit, faute de documentation officielle. L'application affiche la réponse du synthé ; vérifie aussi sur son écran que le son a bien été écrit.
- **Lecture de la banque** : sur certains appareils, il faut lancer le transfert depuis le synthé (GLOBAL → MIDI Data Dump).
- **Navigateurs** : Chrome et Edge uniquement.

## En cas de problème

| Message ou symptôme | Solution |
|---|---|
| « Midi has been disabled in this document by permissions policy » | La page est affichée dans une autre page (un aperçu, par exemple). Ouvre-la via `http://localhost:8000/…`. |
| « Accès MIDI refusé » | Clique sur l'icône à gauche de l'adresse → Paramètres du site → Appareils MIDI → Autoriser, puis recharge la page. |
| Aucun port MIDI dans la liste | L'ordinateur ne voit pas l'interface. Sur Mac, regarde dans Configuration audio et MIDI → Studio MIDI. |
| **Détecter** ne répond pas | Vérifie les câbles dans les deux sens et le réglage **MIDI Filter EX = ENA**. |
| Le son change mal ou par à-coups | Augmente le **Délai** dans la fenêtre SysEx. |

## Notes techniques

Messages Korg SysEx, Model ID `36h` :

| Fonction | Message |
|---|---|
| Passage en édition Program | `F0 42 3n 36 4E 03 00 F7` |
| Modification d'un paramètre | `F0 42 3n 36 41 aL aH vL vH F7` (adresse et valeur sur 14 bits ; valeurs négatives en complément à deux) |
| Demande du son affiché / réponse | `F0 42 3n 36 10 F7` → `40h`, 164 octets codés 7→8 bits (194 octets au total) |
| Banque complète | demande `1Ch`, réponse `4Ch` (100 × 164 octets, 18 750 octets au total) |
| Écriture | `F0 42 3n 36 11 00 pp F7` |

`n` = canal MIDI − 1.

## Traductions

L'anglais est écrit directement dans `x5studio.html`. Chaque autre langue est un fichier du dossier `lang/` :

```
x5studio.html
lang/
  fr.js   it.js   es.js   de.js
```

Chaque fichier associe chaque texte anglais de l'interface à sa traduction, et contient aussi l'aide de la fenêtre « ? ». Pour corriger une traduction, il suffit de modifier le bon fichier. Pour ajouter une langue :

1. copie `lang/fr.js` en `lang/xx.js` (`xx` = le code de la langue, par exemple `pt`) ;
2. change `code` et `name` en haut du fichier, puis traduis la partie droite de chaque ligne et l'aide ;
3. ajoute `<script src="lang/xx.js"></script>` à côté des autres lignes de langue, dans le `<head>` de `x5studio.html`.

Garde tels quels les repères `{0}`, `{1}` et les balises HTML. Un texte manquant s'affiche simplement en anglais.

## Remerciements

La carte des paramètres s'appuie sur l'étude du panel Ctrlr « 05R/W » de Mauro De Carolis (en corrigeant plusieurs erreurs d'encodage), complétée par le manuel de référence Korg X2/X3, puis corrigée grâce aux tables MIDI officielles du X5DR transcrites dans le projet [x5dr-editor](https://github.com/Baylo1/x5dr-editor) de Mark Baylis (licence MIT). La gestion du mode édition (rendre la main au synthé, reprise après un refus) suit le comportement documenté dans ce projet. Pour éditer les Combinations, le mode Multi, les réglages Global et les kits de batterie, cet éditeur est un bon complément à X5 Studio.

## Copyright

© 2026 Benjamin PATY (BenjaminPaty54). Distribué sous [licence MIT](LICENSE) : chacun peut utiliser, modifier et partager ce logiciel, à condition de conserver la mention de copyright.

Korg, X5, X5D, X5DR et 05R/W sont des marques de Korg Inc. Ce projet est indépendant et n'est ni affilié à Korg ni approuvé par Korg.
