# 🐧 Linux Quest

Parcours d'**apprentissage** gamifié de Linux (Debian) : **100 niveaux**, **10 mondes**, un **boss** à la fin de chaque monde.
Objectif : comprendre vraiment comment fonctionne Linux, de la console jusqu'au bureau graphique, et savoir **dépanner ma propre machine**.

> Contrairement à JS Quest, qui évalue mon niveau, Linux Quest est un parcours où **j'apprends** : chaque niveau introduit une notion, puis me la fait pratiquer. Les boss sont les épreuves où je prouve ce que j'ai appris.

---

## 📜 Règles du jeu

### Généralités
- Les niveaux se font **dans l'ordre** : chacun s'appuie sur les précédents.
- Pour passer au monde suivant, il faut **battre le boss avec au moins 2 ⭐**.
- Un niveau peut être **rejoué** plus tard pour récupérer les étoiles manquantes.
- Les **niveaux bonus** sont facultatifs et ne comptent pas dans le total.

### Les étoiles (0 à 3 par niveau)
Pour chaque niveau, je rédige un **compte rendu**. Les étoiles sont attribuées **par Claude, à son jugement**, selon ce que ce compte rendu montre des compétences acquises :

| Étoiles | Ce que montre le compte rendu |
|---|---|
| ⭐ | **La mission est accomplie** : les commandes et leurs sorties prouvent que c'est fait. Sans cette étoile, le niveau n'est **pas validé**. |
| ⭐⭐ | **La notion est comprise** : mes explications sont justes et cohérentes avec ce que j'ai fait et observé. Je sais dire ce que fait chaque commande et pourquoi je l'ai utilisée. |
| ⭐⭐⭐ | **La compétence est acquise** : je vais au-delà de la mission. Je fais des liens avec les niveaux précédents, j'interprète ce que j'observe, je repère les pièges, et je saurais refaire la mission dans un autre contexte. |

- Les étoiles sont **progressives** : si j'enrichis ou corrige un compte rendu plus tard, Claude peut le réévaluer et monter la note. Rien n'est perdu définitivement.
- Les aides que j'ai utilisées sont **déclarées dans le compte rendu**. Elles ne coûtent pas d'étoile par elles-mêmes : ce qui compte, c'est que le compte rendu montre que j'ai compris.

**Score** : 300 ⭐ au maximum. Le niveau réel se lit avec le niveau atteint **et** le total d'étoiles.

### 🖥️ Où faire chaque niveau
**Tout se fait dans la VM**, et presque tout en mode texte :

| Mondes | Environnement |
|---|---|
| 1 à 7, 9 et 10 | La VM, **en mode texte uniquement** (console ou SSH depuis mon vrai terminal) |
| 8 | La même VM, sur laquelle j'installe moi-même le bureau graphique (niveau 72) |
| 99 | Une **deuxième VM**, en netinstall minimal |
| Bonus B4 | Mon vrai PC, **en lecture seule** (observer, ne rien modifier) |

**La VM**
- Debian **sans environnement graphique**, avec seulement « serveur SSH » et « utilitaires usuels du système » cochés à l'installation.
- 2 cœurs, 3 à 4 Go de RAM, 15 à 20 Go de disque (au format qcow2, il ne prend que la place réellement utilisée).
- Outil : **virt-manager** (KVM).
- Je m'y connecte **en SSH depuis mon vrai terminal** dès le niveau 01. La console de virt-manager reste utile quand le réseau ou le démarrage sont cassés.

**📸 Snapshots obligatoires**
- Un snapshot **« propre »** juste après l'installation de la VM
- Un snapshot **avant chaque boss**
- Un snapshot **avant le niveau 72** (installation du bureau)

### La documentation
Tout est permis pour apprendre : `man`, `--help`, `tldr`, le wiki Debian, le wiki Arch, des articles, et Claude pour **expliquer une notion** (« Fiche NN » ou « Mode doc : »).

La seule règle : **pour les boss, je ne lis pas le script de sabotage** avant de l'avoir lancé.

### Workflow
1. **(Facultatif)** Je demande à Claude la **fiche du niveau** : « Fiche NN ».
2. Je réalise la mission.
3. Je rédige le **compte rendu** du niveau (voir le modèle ci-dessous).
4. Un commit par niveau : `niveau NN : nom du niveau ✅`
5. Je demande l'évaluation à Claude : « évalue les niveaux NN à NN ».

### Organisation du repo
Un dossier par monde, et **un fichier Markdown par niveau** :
```
linux-quest/
├── README.md
├── monde-01-terminal/
│   ├── 01-premier-contact.md
│   ├── 02-se-deplacer.md
│   └── ...
├── monde-04-scripts/
│   ├── 40-boss-rangement.md
│   ├── 40-boss-rangement.sh   ← scripts et fichiers de config à côté du compte rendu, si le niveau en produit
│   └── ...
└── ...
```

### Le compte rendu
Chaque fichier de niveau est un compte rendu libre, rédigé avec mes mots. Il contient en général :
- **Ce que j'ai fait** : les commandes tapées et leur sortie, en blocs de code
- **Ce que j'ai observé** : ce qui s'est passé, ce qui m'a surpris
- **Ce que j'en ai compris** : pourquoi ça fonctionne comme ça
- **Ce que j'en pense** : les liens avec ce que je connais déjà, les questions qui restent, ce que je ferais différemment
- **Les aides utilisées**

---

## 🤖 Instructions pour Claude (le professeur et l'arbitre)

Tu as **deux rôles** dans ce parcours.

### 🎓 Rôle 1 : le professeur
- Quand je demande **« Fiche NN »**, rédige une courte fiche **« Ce que tu vas apprendre »** : la notion expliquée simplement en quelques paragraphes, les commandes concernées et leurs options utiles, les pièges courants. **Ne donne jamais la solution de la mission.**
- Quand ma question commence par **« Mode doc : »**, réponds comme une documentation : notion, commande, syntaxe, exemple isolé, **jamais appliqué à la mission**.
- Je débute sous Linux (Debian depuis septembre 2026) : explique sans jargon inutile, et définis chaque terme technique la première fois.

### ⚖️ Rôle 2 : l'arbitre
Quand je te demande d'évaluer des niveaux :

1. **Lis** ce README, l'énoncé de chaque niveau (liste ci-dessous) et le **compte rendu** de chaque niveau, ainsi que les scripts et fichiers de config éventuels.
2. **Attribue les étoiles à ton jugement**, selon le tableau des étoiles : la mission est-elle accomplie ? Les explications sont-elles **justes et cohérentes** avec les commandes et les sorties ? Le compte rendu montre-t-il que la compétence est **réellement acquise** ?
3. **Justifie ta note** en quelques lignes : ce qui montre la compréhension, et ce qui manque pour l'étoile suivante.
4. **Corrige les erreurs de compréhension** : si une explication est fausse ou approximative, dis-le clairement et explique la bonne version. C'est un parcours d'apprentissage.
5. Si un point du compte rendu est ambigu, tu peux me poser **une ou deux questions** avant de trancher.
6. **Scripts** (monde 4 et suivants) : signale **directement** les points cosmétiques (nommage, code commenté, indentation). Pour les points logiques (bugs, cas limites, gestion des erreurs, chemins avec des espaces), donne d'abord la **catégorie**, puis le détail seulement si je le demande. Ne donne pas de script corrigé.
7. **Sécurité** : si une de mes commandes est **dangereuse** (un `rm -rf` mal placé, un `chmod 777` sur un dossier système, une manipulation hors de la VM), signale-le **en priorité**, même si la mission est réussie.
8. **L'orthographe** n'est pas évaluée.
9. **Pas de complaisance** : une étoile non méritée fausse ma progression. Mais une note n'est jamais définitive : si j'améliore un compte rendu, réévalue-le.
10. **Récapitulatif** : termine par le score (niveau validé, total d'étoiles) et la ligne à mettre à jour dans ce README.

### 😈 Les boss
- Pour **chaque boss**, c'est toi qui prépares l'épreuve quand je te la demande (« Prépare le boss NN ») : un script de sabotage, une arborescence piégée ou des fichiers de test à traiter.
- Je récupère tes fichiers dans la VM par SSH (copier-coller dans le terminal, ou `scp` depuis mon vrai PC).
- Les scripts de sabotage sont **conçus pour la VM uniquement** : ils vérifient qu'ils tournent bien dans une machine virtuelle et refusent de s'exécuter sinon. Ils ne cassent **que la VM**, jamais le réseau ou les données de ma vraie machine.
- Livre le script **sans en expliquer le contenu**. Je le lance sans le lire, après un snapshot.
- Après le boss, révèle **tout ce qui avait été cassé**, pour que je vérifie que je n'ai rien oublié.

---

## 🗺️ Les niveaux

Légende : `☆☆☆` = pas encore fait · `⭐☆☆` = mission accomplie · `⭐⭐☆` = notion comprise · `⭐⭐⭐` = compétence acquise

### 🌱 Monde 1 : Les fondamentaux du terminal
- `☆☆☆` **01** · Premier contact : se connecter à la VM en console puis en SSH depuis mon PC, `whoami`, `hostname`, `date`, `uname -a`, `clear`, `exit`, `reboot` et `poweroff`
- `☆☆☆` **02** · Se déplacer : `pwd`, `cd` (`cd ..`, `cd ~`, `cd -`), `ls` et ses options (`-l`, `-a`, `-h`), chemins absolus et relatifs
- `☆☆☆` **03** · Créer et supprimer : `mkdir` (et `-p`), `touch`, `echo` vers un fichier, `rmdir`, `rm` (et `-r`, `-i`)
- `☆☆☆` **04** · Copier, déplacer, renommer : `cp` (et `-r`), `mv`, et les jokers (`*`, `?`, `{a,b}`)
- `☆☆☆` **05** · Lire des fichiers : `cat`, `less`, `head`, `tail` (et `-f`), `wc`, `file`, `stat`
- `☆☆☆` **06** · Éditer avec `nano` : ouvrir, modifier, chercher, enregistrer, quitter
- `☆☆☆` **07** · Survivre dans `vim` : les modes, insérer, enregistrer, quitter (avec ou sans enregistrer), supprimer une ligne, annuler, chercher
- `☆☆☆` **08** · Lire la doc : `man` (naviguer, chercher, les sections), `--help`, `apropos`, `type`, `which`
- `☆☆☆` **09** · L'historique et les raccourcis : `history`, `!!`, `!n`, `Ctrl+R`, la complétion avec `Tab`, `Ctrl+A/E/W/L/C/D`
- `☆☆☆` **10** · 👹 **BOSS : Chasse au trésor** (une arborescence piégée préparée par Claude : trouver les indices en naviguant, lisant et éditant des fichiers)

### 🗂️ Monde 2 : Le système de fichiers
- `☆☆☆` **11** · L'arborescence de Linux : à quoi servent `/etc`, `/var`, `/usr`, `/home`, `/tmp`, `/opt`, `/boot`, `/dev`, `/proc`
- `☆☆☆` **12** · Fichiers cachés, noms avec des espaces et caractères spéciaux : guillemets simples et doubles, échappement avec `\`
- `☆☆☆` **13** · Liens physiques et symboliques : `ln`, la notion d'inode, et ce qui se passe quand on supprime l'original
- `☆☆☆` **14** · Les variables d'environnement : `echo $VAR`, `PATH`, `HOME`, `export`, `env`
- `☆☆☆` **15** · Personnaliser `~/.bashrc` : alias, prompt personnalisé, `source`
- `☆☆☆` **16** · Les archives : `tar` (créer, lister, extraire), `gzip`, `zip` et `unzip`
- `☆☆☆` **17** · Devenir administrateur : le compte root, `su -`, `sudo`, et ajouter mon utilisateur au groupe `sudo`
- `☆☆☆` **18** · Installer des logiciels, les bases : `apt update`, `upgrade`, `install`, `remove`, `search` (installer `tree`, `htop` et `tldr`)
- `☆☆☆` **19** · Télécharger et mesurer : `wget`, `curl`, puis l'espace disque avec `df -h` et `du -sh`
- `☆☆☆` **20** · 👹 **BOSS : Le grand déménagement** (réorganiser une arborescence en désordre selon un cahier des charges : dossiers, liens, archives, fichiers cachés)

### 🔐 Monde 3 : Droits et utilisateurs
- `☆☆☆` **21** · Lire les droits `rwx` et les changer avec `chmod`, en notation symbolique et octale
- `☆☆☆` **22** · Propriétaires et groupes : `chown`, `chgrp`, `id`, `groups`
- `☆☆☆` **23** · Créer et gérer des utilisateurs : `adduser`, `usermod`, `deluser`
- `☆☆☆` **24** · `/etc/passwd`, `/etc/shadow`, `/etc/group` : les comprendre ligne par ligne
- `☆☆☆` **25** · `sudoers` en détail : `visudo`, donner des droits limités à un utilisateur, et pourquoi on ne travaille pas en root
- `☆☆☆` **26** · `umask` : les droits par défaut des nouveaux fichiers
- `☆☆☆` **27** · Les droits spéciaux : setuid, setgid, sticky bit (pourquoi `/tmp` est en `drwxrwxrwt`)
- `☆☆☆` **28** · Les ACL : des droits plus fins avec `getfacl` et `setfacl`
- `☆☆☆` **29** · Un dossier partagé entre deux utilisateurs, sans rien ouvrir de trop
- `☆☆☆` **30** · 👹 **BOSS : Le dossier verrouillé** (un utilisateur a perdu l'accès à ses fichiers : trouver pourquoi et corriger sans tout passer en 777)

### 🧵 Monde 4 : Texte, pipes et scripts
- `☆☆☆` **31** · Rediriger les flux : `>`, `>>`, `2>`, `&>`, `/dev/null`, `<`
- `☆☆☆` **32** · Les pipes et `grep` : chercher dans des fichiers et dans des sorties de commandes
- `☆☆☆` **33** · `find` en profondeur : chercher par nom, taille, date, droits, puis agir avec `-exec`
- `☆☆☆` **34** · `sort`, `uniq`, `wc`, `cut`, `tr` : compter et trier des données
- `☆☆☆` **35** · `sed` : remplacer du texte en masse
- `☆☆☆` **36** · `awk` : extraire des colonnes et calculer
- `☆☆☆` **37** · Premier script bash : shebang, rendre exécutable, variables, arguments, `if`, codes de retour (`$?`)
- `☆☆☆` **38** · Boucles et fonctions bash, gestion des erreurs avec `set -euo pipefail`
- `☆☆☆` **39** · Améliorer mon `update-all.sh` existant : options, couleurs, gestion d'erreurs, résumé final
- `☆☆☆` **40** · 👹 **BOSS : Script de rangement** (sur un dossier en désordre fourni par Claude : trier par type et par date, avec un mode simulation et un journal)

### 📦 Monde 5 : Paquets et logiciels
- `☆☆☆` **41** · `apt` en profondeur : `full-upgrade`, `autoremove`, `show`, `policy`, la différence entre `apt` et `apt-get`
- `☆☆☆` **42** · `dpkg` : installer un `.deb`, lister les fichiers d'un paquet, trouver à quel paquet appartient un fichier
- `☆☆☆` **43** · Les dépôts : `sources.list`, les sections `main`, `contrib`, `non-free` et `non-free-firmware`, et les clés de signature
- `☆☆☆` **44** · Stable, testing, sid et backports : comprendre les branches de Debian et leurs risques
- `☆☆☆` **45** · Dépendances : `apt-cache depends`, `rdepends`, et pourquoi un paquet refuse de s'installer
- `☆☆☆` **46** · Créer mon propre paquet `.deb` pour un de mes scripts, l'installer avec `apt`, puis le désinstaller proprement
- `☆☆☆` **47** · Compiler un petit logiciel depuis ses sources : `./configure`, `make`, `make install`, puis le désinstaller proprement
- `☆☆☆` **48** · Épingler (`apt-mark hold`) et figer une version
- `☆☆☆` **49** · Logs et historique d'apt : retrouver ce qui a été installé, et quand
- `☆☆☆` **50** · 👹 **BOSS : apt est cassé** (dépendances brisées, dépôt mal ajouté : réparer sans réinstaller)

### ⚙️ Monde 6 : Processus et services
- `☆☆☆` **51** · `ps`, `top` et `htop` : lire les colonnes (PID, PPID, état, %CPU, RES), et l'arbre des processus avec `pstree`
- `☆☆☆` **52** · Les signaux : `kill`, `SIGTERM` et `SIGKILL`, `killall`, `pkill`
- `☆☆☆` **53** · Avant-plan et arrière-plan : `&`, `jobs`, `fg`, `bg`, `Ctrl+Z`, `nohup`
- `☆☆☆` **54** · La mémoire et `/proc` : `free`, la RAM « utilisée » qui ne l'est pas vraiment (le cache), le système vu comme des fichiers
- `☆☆☆` **55** · Qui utilise quoi : `lsof`, `fuser`, et les priorités avec `nice` et `renice`
- `☆☆☆` **56** · systemd : `systemctl status`, `start`, `stop`, `enable`, `disable`, lister les services
- `☆☆☆` **57** · `journalctl` : lire et filtrer les journaux par service, par démarrage, par priorité
- `☆☆☆` **58** · Écrire ma propre unité de service systemd
- `☆☆☆` **59** · Planifier des tâches : les timers systemd, et `cron` pour comparer
- `☆☆☆` **60** · 👹 **BOSS : La machine qui rame** (un script de sabotage ralentit la VM et casse un service : trouver tous les coupables)

### 🚀 Monde 7 : Démarrage et disques
- `☆☆☆` **61** · Les étapes du démarrage : UEFI, GRUB, noyau, initramfs, systemd, et ce qui le ralentit avec `systemd-analyze`
- `☆☆☆` **62** · GRUB : le menu, modifier une entrée au démarrage, `/etc/default/grub` et `update-grub`
- `☆☆☆` **63** · Les targets : démarrer en mode secours et en mode urgence, et quand s'en servir
- `☆☆☆` **64** · Identifier le matériel : `lsblk`, `lspci`, `lsusb`, `dmesg`
- `☆☆☆` **65** · Ajouter un disque virtuel à la VM et le partitionner : `fdisk` ou `parted`, MBR ou GPT
- `☆☆☆` **66** · Systèmes de fichiers : formater en ext4 et en btrfs avec `mkfs`, vérifier avec `fsck`
- `☆☆☆` **67** · Monter et démonter : `mount`, `umount`, `blkid`, et monter automatiquement avec `/etc/fstab` et les UUID
- `☆☆☆` **68** · La mémoire virtuelle : créer un fichier swap, l'activer au démarrage, régler `swappiness`
- `☆☆☆` **69** · Les modules du noyau : `lsmod`, `modinfo`, `modprobe`, blacklister un module
- `☆☆☆` **70** · 👹 **BOSS : Le démarrage infernal** (la VM ne démarre plus : `fstab` erroné, service bloquant… réparer depuis le mode secours)

### 🖥️ Monde 8 : Environnements graphiques
*📸 Snapshot avant le niveau 72 : c'est ici que la VM passe en mode graphique.*
- `☆☆☆` **71** · Le schéma général : serveur d'affichage, compositeur, gestionnaire de fenêtres, environnement de bureau
- `☆☆☆` **72** · Installer un bureau depuis la console : XFCE, minimal, paquet par paquet, en comprenant le rôle de chacun
- `☆☆☆` **73** · X11 ou Wayland : différences, savoir lequel tourne, et ce que ça change
- `☆☆☆` **74** · Les gestionnaires de connexion (LightDM, GDM, SDDM) : en changer et les dépanner
- `☆☆☆` **75** · Installer un deuxième environnement de bureau et comparer
- `☆☆☆` **76** · Un gestionnaire de fenêtres minimaliste (i3), configuré à la main
- `☆☆☆` **77** · Les fichiers `.desktop` et les associations de fichiers (`xdg-mime`)
- `☆☆☆` **78** · Les dossiers XDG et mes dotfiles, versionnés dans un repo Git
- `☆☆☆` **79** · Le son : PipeWire, `wpctl`, et pourquoi le son disparaît
- `☆☆☆` **80** · 👹 **BOSS : Écran noir** (la session graphique ne démarre plus : réparer depuis une console texte avec `Ctrl+Alt+F3`)

### 🌐 Monde 9 : Réseau
- `☆☆☆` **81** · Interfaces et adresses : `ip a`, `ip r`, adresse IP, masque, passerelle
- `☆☆☆` **82** · Configurer le réseau : `/etc/network/interfaces` et une IP fixe, puis NetworkManager et `nmcli` s'il est arrivé avec le bureau
- `☆☆☆` **83** · DNS : `/etc/resolv.conf`, `/etc/hosts`, `dig`, et la différence entre « pas Internet » et « pas de DNS »
- `☆☆☆` **84** · Diagnostiquer : `ping`, `traceroute`, `mtr`
- `☆☆☆` **85** · Ports et connexions : `ss -tulpn`, qui écoute quoi
- `☆☆☆` **86** · SSH en profondeur : clés, `~/.ssh/config`, tunnels, `scp` et `rsync`
- `☆☆☆` **87** · Pare-feu : `ufw`, puis `nftables` pour comprendre ce qu'il y a dessous
- `☆☆☆` **88** · Partager des fichiers entre mon PC et la VM (NFS ou Samba)
- `☆☆☆` **89** · Lire le trafic avec `tcpdump` : capturer une requête HTTP et une résolution DNS, puis les analyser
- `☆☆☆` **90** · 👹 **BOSS : Plus de réseau** (la VM n'accède plus à Internet, pour trois raisons différentes cachées : les trouver toutes)

### 🛠️ Monde 10 : Le Donjon du dépannage
- `☆☆☆` **91** · Ma trousse de secours : démarrer la VM sur un ISO live Debian, et préparer une vraie clé USB live pour mon PC
- `☆☆☆` **92** · `chroot` depuis le live : réparer un système qui ne démarre pas
- `☆☆☆` **93** · Réinstaller GRUB après l'avoir cassé
- `☆☆☆` **94** · Retrouver l'accès root après la perte du mot de passe
- `☆☆☆` **95** · Disque plein à 100 % : récupérer le système
- `☆☆☆` **96** · Une mise à jour qui casse tout : revenir en arrière proprement
- `☆☆☆` **97** · Récupérer des fichiers supprimés ou une partition abîmée (`testdisk`, `photorec`)
- `☆☆☆` **98** · Sauvegardes : `rsync`, snapshots btrfs sur un disque dédié, et une restauration testée pour de vrai
- `☆☆☆` **99** · Installer Debian en netinstall minimal sur une deuxième VM, puis construire mon système pièce par pièce
- `☆☆☆` **100** · 🐲 **BOSS FINAL : Le Chaos** (un script de sabotage casse plusieurs choses à plusieurs niveaux : démarrage, paquets, droits, réseau, graphique. Tout réparer en documentant mon diagnostic)

### 🎁 Niveaux bonus (facultatifs, après le monde 8)
- `☆☆☆` **B1** · Flatpak et Flatseal : sandbox et permissions des applications
- `☆☆☆` **B2** · Polices, thèmes, icônes et curseurs
- `☆☆☆` **B3** · Wireshark : analyser du trafic en mode graphique
- `☆☆☆` **B4** · Observer le matériel réel de mon PC, en lecture seule : pilotes (`lspci -k`), firmwares, santé des disques (`smartctl`)
- `☆☆☆` **B5** · udev : réagir au branchement d'une clé USB (redirigée vers la VM)

---

## 🏆 Rangs

| Niveaux | Rang |
|---|---|
| 1 à 20 | Utilisateur averti |
| 21 à 40 | Bricoleur du terminal |
| 41 à 60 | Mécanicien du système |
| 61 à 80 | Maître de sa machine |
| 81 à 100 | Dépanneur légendaire |

**Total : 0 / 300 ⭐**

---

## 💬 Prompts pour une nouvelle conversation

**Pour apprendre ou évaluer :**
```
Je fais un parcours d'apprentissage gamifié de Linux. Tu es mon professeur et l'arbitre qui évalue mes niveaux.
Repo : https://github.com/digital-skylines/linux-quest
Lis le README.md (règles et instructions pour toi), puis [Fiche NN / évalue les niveaux NN à NN / prépare le boss NN].
```

**En fin de session, pour mettre à jour le README :**
```
Mets à jour le README.md de mon repo linux-quest à partir de la version actuelle du repo : les étoiles de chaque niveau évalué dans cette conversation, le total d'étoiles, et les nouvelles règles décidées dans cette conversation. Ne modifie rien d'autre et renvoie-moi le fichier complet.
```
