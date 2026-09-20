# CW Terminal — Mise en route rapide

Ce guide te mène de l'installation au premier décodage, puis à la connexion de ta radio
(Icom, Yaesu, HRD, OmniRig, FLRig, SDRuno). Compte 10 minutes pour décoder, 20 de plus pour piloter la radio.

> ⚠️ **Sécurité radio.** Pour tes premiers essais d'**émission**, mets une **charge fictive** (ou
> vérifie que l'antenne est en bon état) et garde la main près du bouton d'arrêt. Une radio mal
> réglée peut rester en émission. **Se connecter n'émet jamais rien** (la V1.8 envoyait un « VVV » à la
connexion Yaesu, c'est supprimé depuis la V1.9) : seul le bouton **ENVOYER**, une macro F1–F10 ou
**TUNE** fait émettre la radio.

---

## 1. Installer et lancer

1. Télécharge `CW_Terminal_Setup_X.Y.exe` sur la page **Releases** et lance-le. Si une ancienne version
   est installée, elle est mise à jour sur place et tes réglages sont conservés. Ferme CW Terminal avant
   d'installer (et **ferme aussi toute ancienne copie** : elle pourrait garder ton port COM ouvert).
2. Lance **CW Terminal** (menu Démarrer ou Bureau). La version s'affiche dans la barre de titre.
3. Clique **⚙ Réglages** (zone d'envoi) et renseigne **indicatif, prénom, QTH, locateur** : ils servent
   aux macros et au log.

## 2. Décoder tout de suite, sans radio branchée

Le décodage ne demande **aucune connexion CAT** : il lui suffit du son de ta radio.

1. Panneau **Décodeur → Audio → Device** : choisis l'entrée qui reçoit le son du récepteur
   (carte son / entrée ligne, « USB Audio CODEC » de la radio, ou un **câble audio virtuel** si le son vient
   d'un logiciel : SDR, HRD, Win4Icom…). Sample Rate : **48000 Hz** en général.
2. Mets ta radio en **CW**, sur un signal.
3. Clique **▶ DÉCODAGE**. Le waterfall s'anime, le texte décodé s'écrit dans la zone du bas.

**Réglage du niveau (important) :** vise des crêtes audio de **20 à 50 %** de l'échelle et **jamais
d'écrêtage**. Un son trop faible (quelques %) dégrade la copie des signaux faibles.

**Le décodeur en 30 secondes**
- **Pitch** : la fréquence de la note CW (trait rouge du waterfall). Clique dans le waterfall pour la placer,
  **LOCK** pour la figer, **AFC** pour recentrer le signal.
- **Multi** : 5 décodeurs en parallèle sur les signaux voisins, fusionnés en un seul texte.
- **Moteur Fit** (groupe **Contrôle**) : le nouveau décodeur, meilleur sur signaux faibles, QSB (fading)
  et manipulation à la main. Décoche-le pour revenir à l'ancien décodeur si besoin.
- **Vitesse** : détectée automatiquement (WPM affiché dans Stats).

## 3. Quelle connexion radio choisir ?

Les onglets se trouvent en haut, dans **Radio / connexion**.

| Tu as… | Onglet à utiliser |
|---|---|
| Un Icom branché en USB directement au PC (IC-7300, IC-7610, IC-9700…) | **Icom CI-V** |
| Un Yaesu récent en USB (FTDX10, FT-991/991A, FTDX101…) | **Yaesu CAT** |
| Ham Radio Deluxe (ou Win4Icom, qui reprend son serveur) déjà connecté à ta radio | **HRD / Icom** ou **HRD / Yaesu** |
| OmniRig déjà réglé sur ta radio | **OmniRig** |
| FLRig déjà réglé sur ta radio | **FLRig** |
| Un récepteur SDRplay piloté par SDRuno | **SDRUno** |
| Juste écouter et décoder | *(aucune connexion à faire, voir § 2)* |

Bouton **Auto Config** : recharge ton dernier port/protocole et cherche HRD. Il **ne connecte pas** tout seul.
Bouton **Connecter** : ouvre la connexion et affiche un message de diagnostic (fréquence lue, ou raison de l'échec).

> Un seul logiciel à la fois peut ouvrir un port COM. Si le message dit « port occupé », **ferme HRD,
> Win4Icom, DXLog, OmniRig, WSJT-X… et toute autre copie de CW Terminal** qui utilise ce port, puis réessaie.

---

## 4. Icom en USB direct (onglet « Icom CI-V »)

CW Terminal envoie le CW par **commande CI-V** au manipulateur interne de la radio : pas besoin de
ligne DTR/RTS. Il passe la radio en **mode CW** à la connexion.

**Sur la radio** (menu SET → Connectors, les noms varient un peu selon le modèle et le firmware) :

| Réglage radio | Valeur |
|---|---|
| **CI-V Address** | l'adresse de ta radio (voir plus bas) |
| **CI-V USB Baud Rate** | **Auto** ou **19200** (CW Terminal ouvre le port à 19200) |
| **CI-V USB Port** | **Unlink from [REMOTE]** (port CAT dédié) |
| **CI-V Transceive** | **OFF** (évite le bruit sur le bus) |
| **USB SEND** / **USB Keying (CW)** | **OFF** (le CW passe par CI-V, pas par DTR/RTS : évite toute émission parasite) |
| Manipulateur / break-in | **BK-IN** en semi ou full pour que la radio passe seule en émission |

**Dans CW Terminal**
1. Onglet **Icom CI-V**, protocole **Icom Direct CI-V**.
2. **Port** : le port de la radio (souvent « Silicon Labs CP210x USB to UART Bridge »).
3. **Adr CI-V** : **Auto** (recommandé) ou l'adresse exacte.
   Adresses proposées : `0x94` IC-7300, `0x98` IC-7610, `0x88` IC-7100, `0xA2` IC-9700, `0x70` IC-7600,
   `0x6E` IC-7700, `0x76` IC-7800. « Auto » essaie ces adresses ainsi que `0x7C` et `0x90`.
   ⚠️ **IC-705 (`0xA4`) : non proposée** dans la liste, et non testée par « Auto » — utilise plutôt
   HRD, OmniRig ou FLRig pour cette radio.
4. **Connecter**. Le message doit indiquer la fréquence lue ; elle s'affiche en grand (VFO-A).
   Si tu lis « **Connecté mais fréquence non lue** », c'est presque toujours l'adresse CI-V ou la vitesse.

## 5. Yaesu récent (onglet « Yaesu CAT »)

Le protocole est le **CAT ASCII** des Yaesu récents. Ces radios créent **deux ports COM USB** :

| Port | Rôle | Vitesse |
|---|---|---|
| **Enhanced COM Port** (numéro impair) | CAT : fréquence, mode | **38400 bauds**, 2 bits d'arrêt |
| **Standard COM Port** (le suivant) | **Manipulation CW par DTR** | 4800 bauds |

**Sur la radio** (menus CAT et CW, noms variables selon le modèle) :

| Réglage radio | Valeur |
|---|---|
| **CAT RATE** (du port Enhanced) | **38400** |
| **PC KEYING** (menu CW) | **DTR** |
| **BK-IN** | activé (semi break-in) : c'est lui qui passe la radio en émission |
| **CAT RTS** | **Disable**, sauf si ton câble en a besoin pour l'alimentation |
| Mode | **CW** — CW Terminal **ne change pas le mode** d'un Yaesu (pour éviter une porteuse continue) : mets la radio en CW toi-même |

**Dans CW Terminal**
1. Onglet **Yaesu CAT**, protocole **Yaesu CAT**.
2. **Port** : le port **Enhanced** (CAT).
3. **Port CW** : **Auto** (il essaie les numéros voisins) ou le port **Standard** que tu choisis toi-même.
   « Aucun » = pas de manipulation locale.
4. **Connecter**. La connexion n'envoie rien. Pour **tester la manipulation**, écris `VVV` dans la zone
   d'envoi et clique **ENVOYER** (charge fictive ou antenne en bon état) : la radio doit émettre du CW.

Modèles : prévu et testé pour FTDX10 / FT-991 / FTDX101. Les FT-891 et FT-710 utilisent le même protocole
mais n'ont pas été vérifiés avec CW Terminal. Les anciens Yaesu (FT-847/857/897) ne sont **pas** pris en charge.

## 6. Ham Radio Deluxe (onglets « HRD / Icom » et « HRD / Yaesu »)

HRD sert d'intermédiaire : CW Terminal parle en réseau à HRD, qui pilote la radio.

**Dans HRD Rig Control**
1. Connecte-toi normalement à ta radio (modèle, port COM, vitesse).
2. Laisse HRD **ouvert et connecté** pendant que tu utilises CW Terminal.
3. Vérifie le **serveur TCP** de Rig Control (menu variable selon la version, cherche « IP Server ») :
   port **7809** par défaut. Ne change que si tu l'as modifié toi-même.

**Dans CW Terminal**
1. Onglet **HRD / Icom** ou **HRD / Yaesu** selon ta radio.
2. **Hôte** `127.0.0.1` (même PC), **Port** `7809` (ou ta valeur). **Auto Config** peut détecter le port.
3. **Connecter**.

**Comment part le CW ?**
- **HRD / Icom** : le PTT passe par HRD et le CW est envoyé **en audio USB** (une note générée par le
  programme). CW Terminal bascule temporairement la radio en **DATA-U/USB** pendant l'envoi puis restaure
  le mode. Le son CW est joué sur la **sortie audio par défaut de Windows** : règle-la (Paramètres Windows →
  Son) sur l'**USB Audio CODEC de la radio** ou sur ton **câble audio virtuel** relié à la radio, et vérifie
  que la radio accepte l'audio USB en émission (entrée USB / DATA). Le choix « Device » du panneau Décodeur
  ne concerne que la **réception**.
- **HRD / Yaesu** : fréquence et PTT par HRD, **manipulation par DTR sur le Standard COM Port** (réglage
  « Port CW » à côté). Radio en CW, **PC KEYING = DTR**.

**Win4Icom Suite** : il reprend le même serveur HRD (port 7809). La procédure est identique.

> Le **log** vers HRD Logbook est une fonction distincte (voir § 10).

## 7. OmniRig, FLRig, SDRuno

**OmniRig** — installe OmniRig et règle **Rig1** ou **Rig2** (modèle de radio, port COM, vitesse, bits de
données, parité, arrêt). Dans CW Terminal, onglet **OmniRig** : choisis **Rig1/Rig2**, puis **Connecter**.
Les boutons d'état affichent si OmniRig répond. Fréquence, mode et PTT passent par OmniRig.

**FLRig** — lance FLRig, règle ta radio (modèle, port, vitesse) et vérifie que le serveur XML-RPC est actif.
Dans CW Terminal, onglet **FLRig** : hôte `127.0.0.1`, port `12345` (par défaut), **Connecter**.
Fréquence, mode et PTT passent par FLRig.

**SDRuno / SDRplay** — le récepteur est suivi via **OmniRig Rig1** (profil TS-2000) : SDRuno suit la
fréquence de CW Terminal. Réception seule (pas d'émission).

---

## 8. Envoyer du CW

1. Écris ton texte dans la zone **« Texte à envoyer en CW… »**, règle **WPM**, puis **ENVOYER**.
   **STOP** interrompt immédiatement.
2. **Macros F1–F10** : un clic les envoie, un **double-clic** les édite. Variables utiles : `{ME}`
   (ton indicatif), `{DE}` (indicatif reçu), `{RST}`, `{QTH}`, `{NAME}`, `{NR}` (numéro de série).
3. **Mode Contest** : charge des macros de contest et **incrémente automatiquement le numéro** (`{NR}`).
   **NR↺** remet à 001.
4. **TX Continu** : envoie au fil de l'eau ce que tu tapes.
5. Boutons de réponse rapide : **APPEL**, **TNX**, **CONTEST**, **SK**, **DX** (double-clic pour modifier le modèle).

## 9. Le reste de l'écran en bref

- **Fréquence** (VFO-A / VFO-B) : clique sur un chiffre puis molette pour changer ; **Bandes** en un clic.
- **SPLIT** : RX sur VFO-A, TX sur VFO-B, offset par les boutons kHz ; **⇄** inverse RX/TX.
- **SCAN ▲ / ▼** : balaie la bande et s'arrête sur un signal CW.
- **TUNE** : lance l'accordeur (Icom CI-V ou HRD). **Ne l'utilise pas pendant un QSO.**
- **Propagation** (bandeau du bas) : SFI, K, A, mise à jour automatique.
- **Mode RX** : masque le panneau d'émission (utile pour n'écouter que le décodage).
- **ABR / CORR** : abréviations CW et correction des indicatifs et Q-codes.
- **Lecture / VOCAL** : lecture vocale du texte décodé, saisie vocale du texte à envoyer.

## 10. Logger un QSO

Bouton **LOG** : la fenêtre propose l'envoi vers **HRD Logbook, N1MM+, DXLog, Win-Test, WinRef, eQSL,
ClubLog, WaveLog, Log32, Log4OM, LoTW, QRZ.com** ou un **fichier ADIF**.
Pour les envois réseau (UDP), **le port doit être exactement celui affiché dans le logiciel de log**.
Ports habituels : N1MM+ 12060, DXLog 2333, Win-Test 9871, Log4OM 2237, Log32 2000 — vérifie toujours dans ton logiciel.
Pour **HRD Logbook** : *File → QSO Forwarding* (le nom varie selon la version) pour lire le port UDP ADIF.

## 11. Mises à jour et téléchargements

Au démarrage, CW Terminal vérifie **silencieusement** s'il existe une version plus récente. Si oui : une
**info-bulle** et le bouton **🔔 Mise à jour disponible** apparaissent dans la barre d'état ; un clic ouvre les
nouveautés et le téléchargement. Réglages → **Mises à jour** : vérification manuelle, désactivation de la
vérification automatique, et **compteur de téléchargements**. Rien n'est envoyé sur toi, rien n'est installé
sans ton action.

---

## Dépannage

| Symptôme | Cause probable | Que faire |
|---|---|---|
| « Port COMx occupé par un autre logiciel » | Un autre programme tient le port | Ferme HRD / Win4Icom / DXLog / OmniRig / une autre copie de CW Terminal, réessaie |
| « Port introuvable » | Câble ou pilote | Vérifie le Gestionnaire de périphériques ; pilote **CP210x** pour beaucoup d'Icom/Yaesu |
| « Connecté mais fréquence non lue » (Icom) | Mauvaise adresse CI-V ou vitesse | **Adr CI-V = Auto**, CI-V USB Baud Rate = Auto/19200, CI-V Transceive OFF |
| Yaesu : aucune réponse | Mauvais port ou vitesse | Port **Enhanced**, **CAT RATE = 38400** |
| La radio n'émet pas le CW (Yaesu) | Manipulation | PC KEYING = DTR, port CW = Standard COM, BK-IN activé, radio en **CW** |
| La radio n'émet pas le CW (Icom) | Mode / break-in | Radio en **CW**, BK-IN activé, CI-V USB Port « Unlink from REMOTE » |
| Rien ne se décode | Audio | Bon **Device**, niveau 20–50 %, radio en CW, pitch sur le signal |
| Beaucoup de `E` `T` parasites | Bruit / niveau trop bas | Monte le niveau audio, active **Moteur Fit**, place le pitch sur le signal |
| Un texte double ou décalé | Deux copies ouvertes | Ferme l'autre copie de CW Terminal |

Pour de l'aide : **F4LPS — developpement@lesf4.fr**. 73 !
