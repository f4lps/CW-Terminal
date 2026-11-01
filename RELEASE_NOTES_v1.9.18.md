## CW Terminal V1.9.18

**CW Terminal arrive sur Linux, et sur Mac en essai.** Rien ne change pour Windows.

- **Windows** : `CW_Terminal_Setup_1.9.18.exe`. Ferme CW Terminal, lance l'installeur : il met à jour sur place et
  conserve tes réglages.
- **Linux** (64 bits, Ubuntu 22.04 / Debian 12 ou plus récent) : `cw-terminal_1.9.18_amd64.deb`, ou
  `CW_Terminal-1.9.18-linux-x86_64.tar.gz` pour les autres distributions.
- **Mac, EN ESSAI** : `CW_Terminal-1.9.18-mac-arm64-essai.dmg` (Apple Silicon, M1 et suivants) ou
  `CW_Terminal-1.9.18-mac-x86_64-essai.dmg` (Intel).

Installation sous Linux, puis déconnexion et reconnexion pour avoir accès aux ports série :

```
sudo apt install ./cw-terminal_1.9.18_amd64.deb
sudo usermod -aG dialout $USER
```

La voix (TTS) utilise `espeak-ng` sous Linux et la voix du système sur Mac, sur la sortie son par défaut.

Sur Mac : le programme n'est pas signé par Apple. Au premier lancement, fais clic droit > Ouvrir, puis autorise le
micro : c'est lui qui donne accès à l'entrée audio de la radio.

**Important.** Les versions Linux et Mac démarrent et leurs fonctions ont été contrôlées sur ordinateur, mais elles
n'ont pas encore été essayées avec une vraie radio. Pour les premières émissions, utilise une charge fictive. La
version Mac est un essai : merci de signaler ce qui ne marche pas à developpement@lesf4.fr.

Absent hors Windows pour le moment : OmniRig. HRD fonctionne seulement à travers le réseau.

Rappel V1.9.17 : fréquence toujours présente dans les logs, recherche QRZ des préfixes chiffrés.

73 de F4LPS
