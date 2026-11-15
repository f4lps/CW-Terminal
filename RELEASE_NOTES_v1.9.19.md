## CW Terminal V1.9.19

**Le Tracker de CW Terminal fonctionne maintenant comme GridTracker 2.** Bouton « 📍 Tracker », comme avant.

- **Liste des appels** : les stations décodées par WSJT-X, JTDX ou MultiDigi FT8 (messages UDP au format WSJT-X),
  avec pays, continent, zone CQ, dB, fréquence et message. Couleurs d'après ton journal : nouveau pays, nouvelle
  zone CQ, nouvelle grille, nouveau préfixe WPX, nouveau pays sur la bande ou dans le mode, déjà contacté. Fond rouge
  quand une station t'appelle. Les stations entendues apparaissent aussi en losanges sur la carte.
- **Réponse par clic** : un double-clic sur une station (dans la liste ou sur la carte) la fait appeler par WSJT-X ou
  MultiDigi FT8 ; bouton « Stop TX » pour couper l'émission.
- **Filtres** : bande, mode, dB minimum, continent, CQ seulement, déjà contactés masqués, stations qui utilisent
  LoTW ou eQSL. Listes de stations recherchées et d'indicatifs ou pays ignorés. Tu choisis ce que tu chasses.
- **Alertes** : son, voix (indicatif épelé avec l'alphabet radio : Alpha, Bravo…) ou bulle, quand une station
  t'appelle, une station recherchée ou un nouveau pays apparaît.
- **Journaux en ligne** : confirmations eQSL, LoTW et QRZ.com, gardées d'une session à l'autre ; onglet Awards
  (DXCC, zones CQ et ITU, continents, préfixes WPX, grilles) avec contactés, confirmés et ce qui manque.
- **Carte** : ligne jour/nuit, zones CQ et ITU ; renvoi des messages vers d'autres programmes (GridTracker,
  JTAlert…).

**Correction** : CW Terminal envoie ses spots et QSO au port réglé dans le Tracker (2238 sur certains PC), et non plus
toujours au port 2237. Avant, quand GridTracker occupait le port 2237, les spots de CW Terminal n'arrivaient pas.
Une ancienne vérification eQSL trouvait aussi toujours 0 confirmation : c'est corrigé.

- **Windows** : `CW_Terminal_Setup_1.9.19.exe`. Ferme CW Terminal, lance l'installeur : il met à jour sur place et
  conserve tes réglages.
- **Linux** (64 bits, Ubuntu 22.04 / Debian 12 ou plus récent) : `cw-terminal_1.9.19_amd64.deb`, ou
  `CW_Terminal-1.9.19-linux-x86_64.tar.gz` pour les autres distributions.
- **Mac, EN ESSAI** : `CW_Terminal-1.9.19-mac-arm64-essai.dmg` (Apple Silicon, M1 et suivants) ou
  `CW_Terminal-1.9.19-mac-x86_64-essai.dmg` (Intel).

Les identifiants LoTW et la clé du journal QRZ.com se règlent dans le Tracker, bouton « Réglages ».

Rappel V1.9.18 : CW Terminal sur Linux, et sur Mac en essai.

73 de F4LPS
