# 🐧 Linux Quest

Mon cours de Linux (Debian), en **sessions de 20 minutes**, à raison d'une par jour.
Objectif : savoir utiliser Linux au quotidien, comprendre ce qui se passe sur ma machine, et à terme **savoir la dépanner**.

> J'apprends en faisant : chaque session présente une seule notion, me la fait pratiquer dans la VM, puis me pose quelques questions. Pas de note, pas d'étoiles, juste une progression.

---

## 📜 Règles

### Le principe
- **Une session = une notion = 20 minutes maximum** : environ 5 minutes de lecture, 10 de pratique, 5 pour répondre aux questions.
- Les sessions se font **dans l'ordre** : chacune n'utilise que ce qui a été vu avant.
- Chaque chapitre se termine par un **défi** : une petite situation à résoudre seul, avec ce que j'ai appris. Pas de note, juste de la pratique.
- Une session peut être refaite quand je veux, pour réviser.

### Déroulé d'une session
1. Je demande à Claude : **« Session X.Y »**.
2. Claude génère le fichier de la session (voir le modèle plus bas) et je le place dans le bon dossier.
3. Je fais la pratique dans la VM.
4. J'écris mes réponses aux questions directement dans le fichier.
5. Je commite : `session X.Y : nom de la session`
6. Je demande à Claude : **« Relis la session X.Y »**. Il me fait un retour court, et je coche la notion dans ce README.

### 🖥️ L'environnement
- **Une VM VirtualBox** : Debian **sans environnement graphique**, avec seulement « serveur SSH » et « utilitaires usuels du système » cochés à l'installation.
- 2 cœurs, 3 à 4 Go de RAM, 15 à 20 Go de disque.
- Je m'y connecte **en SSH depuis mon vrai terminal** (`ssh andre@localhost -p 2222`, grâce à une redirection de port VirtualBox). La fenêtre VirtualBox sert quand le réseau ou le démarrage sont cassés.
- Le mode graphique n'arrive qu'au **chapitre 12**.

**📸 Snapshots**
- Un snapshot **« propre »** juste après l'installation
- Un snapshot **avant chaque défi**
- Un snapshot **avant le chapitre 12** (installation du bureau)

### La documentation
Tout est permis : `man`, `--help`, le wiki Debian, des articles, et Claude (« **Mode doc :** » pour une explication isolée).

---

## 🗂️ Organisation du repo

```
linux-quest/
├── README.md
└── cours/
    ├── 01-premiers-pas/
    │   ├── 1.1-se-connecter.md
    │   ├── 1.2-ou-suis-je.md
    │   └── ...
    ├── 02-manipuler-des-fichiers/
    │   └── ...
    └── ...
```

### Modèle d'un fichier de session

```markdown
# Session X.Y · Titre

🎯 **Objectif** : à la fin de cette session, je sais …

## 📖 Ce qu'il faut savoir
(un peu de théorie, seulement si nécessaire)

## 🛠️ Pratique
1. …
2. …
3. 🧩 À moi de jouer : une petite tâche sans la commande donnée

## ❓ Questions
1. …
   **Ma réponse :**
2. …
   **Ma réponse :**
```

---

## 🤖 Instructions pour Claude (le professeur)

### Quand je demande « Session X.Y »
- Génère le fichier de la session selon le modèle ci-dessus, prêt à être copié dans `cours/`.
- **Une seule notion**, faisable en **20 minutes**.
- **N'utilise que ce qui a déjà été vu** dans les sessions précédentes. Si une commande d'un chapitre ultérieur est indispensable, présente-la comme « à voir plus tard », sans la détailler.
- **Théorie** : courte, sans jargon. Définis chaque terme technique la première fois. Pars de l'usage : à quoi ça me sert, à moi, utilisateur.
- **Pratique** : des étapes concrètes dans la VM, avec les commandes. Termine par une petite tâche « à moi de jouer » où la commande n'est pas donnée.
- **Questions** : 2 à 3, simples, sur ce que j'ai fait et observé, ou sur l'utilité de la notion. Pas de piège, pas de notion qui n'a pas été vue.

### Quand je demande « Relis la session X.Y »
- Lis mes réponses dans le fichier du repo.
- Réponds **dans le chat, en quelques lignes** : ce qui est juste, et une correction **uniquement si une réponse est fausse**, en une ou deux phrases.
- Ne demande **pas** de réécriture, et n'ajoute pas de notions hors du programme de la session.
- Indique la ligne à cocher et la nouvelle progression.

### Quand ma question commence par « Mode doc : »
Réponds comme une documentation : la notion, la commande, la syntaxe, un exemple isolé.

### Les défis
- Quand je demande « **Prépare le défi X** », fournis ce qu'il faut : des fichiers à placer, une arborescence à créer ou un script à lancer.
- Les scripts qui cassent quelque chose sont **conçus pour la VM uniquement** : ils vérifient qu'ils tournent dans une machine virtuelle et refusent de s'exécuter sinon.
- Ne m'explique pas le contenu du script avant que j'aie fini. Ensuite, révèle tout ce qui avait été mis en place, pour que je vérifie que je n'ai rien oublié.

### Toujours
- **Sécurité** : si une de mes commandes est dangereuse (un `rm -rf` mal placé, un `chmod 777` sur un dossier système, une manipulation hors de la VM), signale-le en priorité.
- L'orthographe n'est pas évaluée.

---

## 🗺️ Programme

Légende : `[x]` = session faite · `[ ]` = à faire

**Progression : 1 / 99 sessions (1 %)**

### 🌱 Chapitre 1 · Premiers pas
- [x] **1.1** · Se connecter à la VM : en console et en SSH, `whoami`, `hostname`
- [ ] **1.2** · Où suis-je ? `pwd`, `ls` et ses options (`-l`, `-a`, `-h`)
- [ ] **1.3** · Se déplacer : `cd`, `~`, `..`, `cd -`, chemins absolus et relatifs
- [ ] **1.4** · Infos sur la machine et la session : `date`, `uname`, `clear`, `exit`
- [ ] **1.5** · 🧩 **Défi : explorer la VM**

### 📄 Chapitre 2 · Manipuler des fichiers
- [ ] **2.1** · Créer : `mkdir` (et `-p`), `touch`, `echo` vers un fichier
- [ ] **2.2** · Lire : `cat`, `less`, `head`, `tail`
- [ ] **2.3** · Copier, déplacer, renommer : `cp` (et `-r`), `mv`
- [ ] **2.4** · Supprimer sans regret : `rm`, `rmdir`, `rm -i`, et les dangers de `rm -r`
- [ ] **2.5** · Les jokers : `*`, `?`, `{a,b}`
- [ ] **2.6** · Éditer un fichier avec `nano`
- [ ] **2.7** · 🧩 **Défi : ranger un dossier en désordre**

### 🧭 Chapitre 3 · Se débrouiller seul
- [ ] **3.1** · Lire le manuel : `man`, `--help`
- [ ] **3.2** · Trouver une commande : `apropos`, `type`, `which`
- [ ] **3.3** · L'historique : `history`, `!!`, `Ctrl+R`
- [ ] **3.4** · Taper moins : la complétion avec `Tab`, `Ctrl+A/E/W/L/C/D`
- [ ] **3.5** · Survivre dans `vim` : entrer, modifier, enregistrer et surtout en sortir
- [ ] **3.6** · 🧩 **Défi : la chasse aux indices**

### 🔑 Chapitre 4 · Devenir administrateur
- [ ] **4.1** · Le compte root et `sudo` : pourquoi, `su -`, le groupe `sudo`
- [ ] **4.2** · Éteindre et redémarrer : `reboot`, `poweroff`
- [ ] **4.3** · Installer et supprimer un logiciel : `apt update`, `install`, `remove`
- [ ] **4.4** · Mettre à jour et chercher : `apt upgrade`, `search`, `show`
- [ ] **4.5** · Mes premiers outils : installer et essayer `tree`, `htop` et `tldr`
- [ ] **4.6** · 🧩 **Défi : préparer la VM pour la suite**

### 🗂️ Chapitre 5 · Organiser ses fichiers
- [ ] **5.1** · L'arborescence de Linux : `/etc`, `/home`, `/var`, `/usr`, `/tmp`…
- [ ] **5.2** · Fichiers cachés, noms avec des espaces, guillemets et `\`
- [ ] **5.3** · Les liens : `ln -s`, et ce qui se passe quand on supprime l'original
- [ ] **5.4** · Les archives : `tar`, `gzip`, `zip` et `unzip`
- [ ] **5.5** · L'espace disque : `df -h`, `du -sh`
- [ ] **5.6** · Télécharger : `wget`, `curl`
- [ ] **5.7** · Les variables d'environnement : `echo $VAR`, `HOME`, `PATH`, `export`
- [ ] **5.8** · Personnaliser mon terminal : `~/.bashrc`, alias, `source`
- [ ] **5.9** · 🧩 **Défi : le grand déménagement**

### 🔐 Chapitre 6 · Droits et utilisateurs
- [ ] **6.1** · Lire les droits `rwx` avec `ls -l`
- [ ] **6.2** · Changer les droits : `chmod`
- [ ] **6.3** · Propriétaires et groupes : `chown`, `chgrp`, `id`, `groups`
- [ ] **6.4** · Créer et gérer des utilisateurs : `adduser`, `usermod`, `deluser`
- [ ] **6.5** · `/etc/passwd` et `/etc/group` : où Linux range ses utilisateurs
- [ ] **6.6** · Donner des droits limités avec `sudo` : `visudo`
- [ ] **6.7** · Un dossier partagé entre deux utilisateurs
- [ ] **6.8** · 🧩 **Défi : le dossier verrouillé**

### 🔍 Chapitre 7 · Chercher et trier
- [ ] **7.1** · Rediriger : `>`, `>>`, `2>`, `/dev/null`
- [ ] **7.2** · Enchaîner des commandes avec les pipes `|`
- [ ] **7.3** · Chercher dans des fichiers : `grep`
- [ ] **7.4** · Chercher des fichiers : `find`
- [ ] **7.5** · Trier et compter : `sort`, `uniq`, `wc`, `cut`
- [ ] **7.6** · Remplacer du texte : `sed`, les bases
- [ ] **7.7** · 🧩 **Défi : enquête dans les journaux**

### ⚙️ Chapitre 8 · Automatiser
- [ ] **8.1** · Mon premier script : shebang, rendre exécutable, lancer
- [ ] **8.2** · Variables et arguments
- [ ] **8.3** · Conditions et codes de retour (`if`, `$?`)
- [ ] **8.4** · Les boucles
- [ ] **8.5** · Fonctions et gestion des erreurs
- [ ] **8.6** · Planifier une tâche avec `cron`
- [ ] **8.7** · 🧩 **Défi : un script de rangement**

### 🏃 Chapitre 9 · Ce qui tourne sur la machine
- [ ] **9.1** · Les processus : `ps`, `htop`, `pstree`
- [ ] **9.2** · Arrêter un programme : `Ctrl+C`, `kill`, `pkill`
- [ ] **9.3** · Avant-plan et arrière-plan : `&`, `jobs`, `fg`, `bg`, `Ctrl+Z`
- [ ] **9.4** · La mémoire : `free`, et la RAM « utilisée » qui ne l'est pas vraiment
- [ ] **9.5** · Les services : `systemctl status`, `start`, `stop`, `enable`
- [ ] **9.6** · Les journaux : `journalctl`
- [ ] **9.7** · Créer mon propre service
- [ ] **9.8** · Les timers systemd, comparés à `cron`
- [ ] **9.9** · 🧩 **Défi : la machine qui rame**

### 🌐 Chapitre 10 · Le réseau
- [ ] **10.1** · Adresses et interfaces : `ip a`, `ip r`
- [ ] **10.2** · Le DNS : `/etc/hosts`, `/etc/resolv.conf`, `dig`
- [ ] **10.3** · Diagnostiquer : `ping`, `traceroute`
- [ ] **10.4** · Qui écoute sur quel port : `ss -tulpn`
- [ ] **10.5** · SSH avec des clés et `~/.ssh/config`
- [ ] **10.6** · Copier entre machines : `scp`, `rsync`
- [ ] **10.7** · Le pare-feu : `ufw`
- [ ] **10.8** · 🧩 **Défi : plus de réseau**

### 💽 Chapitre 11 · Disques et démarrage
- [ ] **11.1** · Les étapes du démarrage, et `systemd-analyze`
- [ ] **11.2** · GRUB : le menu, et modifier une entrée au démarrage
- [ ] **11.3** · Le mode secours et le mode urgence
- [ ] **11.4** · Identifier le matériel : `lsblk`, `lspci`, `dmesg`
- [ ] **11.5** · Ajouter un disque à la VM et le partitionner
- [ ] **11.6** · Formater : `mkfs`, ext4
- [ ] **11.7** · Monter un disque : `mount`, `umount`, `/etc/fstab`
- [ ] **11.8** · La mémoire virtuelle : un fichier swap
- [ ] **11.9** · Le noyau et ses modules : `uname`, `lsmod`, `modprobe`
- [ ] **11.10** · 🧩 **Défi : le démarrage infernal**

### 🖥️ Chapitre 12 · L'environnement graphique
*📸 Snapshot avant de commencer ce chapitre.*
- [ ] **12.1** · Le schéma général : serveur d'affichage, gestionnaire de fenêtres, bureau
- [ ] **12.2** · Installer XFCE depuis la console
- [ ] **12.3** · X11 ou Wayland : savoir lequel tourne
- [ ] **12.4** · Le gestionnaire de connexion : LightDM
- [ ] **12.5** · Les applications : fichiers `.desktop` et associations de fichiers
- [ ] **12.6** · Le son : PipeWire et `wpctl`
- [ ] **12.7** · 🧩 **Défi : écran noir**

### 🛠️ Chapitre 13 · Le dépannage
- [ ] **13.1** · Ma trousse de secours : démarrer sur un ISO live
- [ ] **13.2** · `chroot` : réparer un système depuis le live
- [ ] **13.3** · Réinstaller GRUB
- [ ] **13.4** · Retrouver l'accès root après la perte du mot de passe
- [ ] **13.5** · Disque plein à 100 % : récupérer le système
- [ ] **13.6** · Réparer `apt` : dépôts mal ajoutés et dépendances cassées
- [ ] **13.7** · Une mise à jour qui casse tout : revenir en arrière
- [ ] **13.8** · Récupérer des fichiers supprimés
- [ ] **13.9** · Sauvegarder et restaurer pour de vrai
- [ ] **13.10** · 🐲 **Défi final : le Chaos**

---

## 💬 Prompts pour une nouvelle conversation

**Pour une session :**
```
Je suis un cours de Linux en sessions de 20 minutes. Tu es mon professeur.
Repo : https://github.com/digital-skylines/linux-quest
Lis le README.md (règles et instructions pour toi), puis [Session X.Y / Relis la session X.Y / Prépare le défi X.Y].
```

**Pour mettre à jour le README :**
```
Mets à jour le README.md de mon repo linux-quest à partir de la version actuelle du repo : coche les sessions relues dans cette conversation, mets à jour la progression, et ajoute les nouvelles règles décidées dans cette conversation. Ne modifie rien d'autre et renvoie-moi le fichier complet.
```
