# 01 Premier contact

## Connection à mon SSH

- je me suis connecté une fois dans la fenêtre VirtualBox pour tester.

- Pour me connecte à ma VM j'utilise sur mon terminal : `ssh andre@localhost -p 2222`
- Ensuite ça me demande le mot de passe de la session.
- Je suis connecté sur : `andre@linuxquest`

Explications de la commande :  
- `ssh`: sert à lancer la connexion ssh
- `andre`: sert à ce connecter à l'utilisateur `andre`
- `@`: sert à séparer le username du hostname
- `localhost -p 2222`: En fait je passe par mon localhost pour me connecter à ma machine. Ce qu'il s'est passé c'est que mon localhost:2222 est monté sur la machine `linuxquest:22`. Donc en me connectant à mon localhost:2222, je me connecte directement vers linuxquest:22. J'ai paramétré ça sur virtualbox dans la partie réseau. Tu n'as pas a savoir comment j'ai fait, c'est hors du cours et je ne veux pas perdre du temps a expliquer ça.


## Les commandes

- `whoami`: Affiche qui je suis, mon nom d'utilisateur étant `andre`, il m'affiche donc cela. C'est la partie à gauche de `andre@linuxquest`.
- `hostname`: Affiche le nom de la machine sur laquelle je me trouve. Ici c'est `linuxquest`. C'est la partie à droite de `andre@linuxquest`.
- `date`: Affiche la date et l'heure courante. Dans mon cas : `lun. 16 nov. 2026 08:56:24 CET`. `CET` est pour "Central European Time"
- `uname -a`: D'après la commande `man`, `uname` sert à afficher des infromations sur le système. L'option `-a` est la raccourci pour `--all` qui permet d'afficher "toutes les informations dans l'ordre suivant, hormis celles de -p et -i s'elles sont inconnues (valeur « unknown »)". Je vois qu'il est possible d'avoir pas mal d'informations interessante comme le nom de l'arcitecture de la machine ou encore le processor aussi avec cette commande. J'ai aussi appris que `-n` affiche finalement mon hostname comme `hostname`. Le résultat de la commande `uname -a` affiche `Linux linuxquest 6.12.117+deb13-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.117-1 (2026-11-12) x86_64 GNU/Linux`. De ce que j'ai compris, cette longue chaine est l'équivalent des options : `-s -n -r -v -m -o`
    - `-s`: `Linux`
    - `-n`: `linuxquest`
    - `-r`: `6.12.117+deb13-amd64`
    - `-v`: `#1 SMP PREEMPT_DYNAMIC Debian 6.12.117-1 (2026-11-12)`
        - `#1` indique le numéro de compilation du noyau.
        - `SMP`: Ca veut dire que le noyau peut utiliser plusieurs coeurs ou processeurs.
        - `PREEMPT_DYNAMIC`: le noyau prend en charge un mode de préemption configurable à l’exécution. Le mode actif dépend de la configuration de la distribution; le libellé seul ne précise pas lequel est actuellement utilisé.
    - `-m`: `x86_64`
    - `-o`: `GNU/Linux`
- `clear`: Je connaissais déjà, ça permet d'effacer le contenu du terminal.
- `exit`: Sert à fermer le shell de la session. En tout cas c'est comme ça que je le comprend vu qu'il n'y a pas de `man exit` et que quand j'utilise exit ça me sort du terminal de la VM.
- `reboot`: Ca permet de redémarrer. Ma VM a redémarré avec `sudo reboot`. Mon terminal a quitté la VM.
- `poweroff`: Sert à éteindre la machine. Ma VM s'est éteinte avec `sudo poweroff`. Mon terminal a quitté la VM.

Concernant `reboot` + `poweroff`, j'ai constaté en lisant le manuel qu'ils partageaient les mêmes options et donc qu'il est possible d'éteindre, de redémarrer ou d'arrêter la machine avec eux selon les options que l'on applique mais par défault, reboot sert à redemarrer et poweroff à éteindre. Dernière chose, il n'est possible de lancer ces commandes qu'en utilisant `sudo` car sinon j'ai ce message : `-bash: poweroff : commande introuvable`.

Raison :
- En tapant une commande, le shell cherche dans une liste de dossiers précise enregistrée dans la variable PATH.
- poweroff et reboot sont rangé dans `/usr/bin`. Sudo a accès à ces dossiers mais pas l'utilisateur courant.