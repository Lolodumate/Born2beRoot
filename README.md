# Born2beRoot
Projet 42 - Born2beRoot
Notes projet Born 2 be Root :

Prerequis : 
- Utiliser VirtualBox (obligatoire).
- Rendre fichier signature.txt dans le depot Git.

Sujet obligatoire :
- Systeme d'exploitation : Debian (recommande).
- SELinux :
	- Doit rester actif,
	- Sa configuration doit etre adaptee au sujet.
- AppArmor doit egalement rester actif.
- Creer au moins deux partitions chiffrees avec LVM.
- Utiliser le parefeu UFW.
- Service SSH actif uniquement sur le port 4242. Le user root ne doit pas pouvoir s'y connecter.
- Configurer le systeme d'exploitation avec le pare-feu UFW et ne laisser ouvert que le port 4242.
- Hostname de la VM : login + 42 (laroges42). Soutenance : modification du hostname.
- Regles de securite de password fortes (regles indiquees page 6 du sujet).
- Installer et configurer sudo (configuration "stricte" : voir consignes en page 7).
- Creer un user avec mon login en plus du user root.
- User laroges doit appartenir aux groupes user42 et sudo.
- Apres configurationm changer tous les passwords.
- Creer un script en bash nomme monitoring.sh : voir consignes page 8.

Attention au consignes de rendu du projet ! Voir consignes page 12 (encadre en bas de page).


Notes pour la soutenance :
********************************************************************************************************************************************
- Questions generales sur le systeme d'exploitation.
====================================================
	> Pourquoi ai-je choisi Debian ?
		
		>> Parce que plus simple a installer et a configurer.


	> Quelles sont les differences entre Debian, Rocky et CentOS ?

	Ressources :
	https://fr.wikipedia.org/wiki/CentOS
	https://waytolearnx.com/2019/04/difference-entre-centos-et-debian.html

		>> Debian vs CentOS :
			* Le noyau (Kernel) de Debian a peut fonctionner avec seulement 64 Mo (256 Mo recommandes).
			* Debian est un OS adapte aux serveurs car il est repute stable et safe.
			* CentOS est complementaire a Red Hat Enterprise Linux (RHL).
			* Debian a plus de packages que CentOS (commande dpkg --list pour consulter la liste des packages installes).
			* Les versions de CentOS sont maintenues pendant 10 ans, tandis que Debian necessite un minimun de connaissances sur Linux.
			* Mises a jour de l'OS tres compliquee pour CentOS et facile pour Debian.
			* GUI : compliquee pour CentOS et user friendly pour Debian.
			

	> Qu'est-ce qu'une VM ?

		>> C'est une ressource qui utilise un logiciel (au lieu d'un hardware pour les OS classiques) pour installer et lancer des programmes.
		>> Chaque VM a son propre OS qui est bien separe de l'OS du hardware. Il est donc possible d'avoir plusieurs VM sur une seule et meme machine physique.
		>> Une VM permet de tester un logiciel, un programme ou une application dans un environnement securise et isole.
		>> Une VM fonctionne en simulant une machine physique.

	> Description des etapes de l'installation de la VM.

	> Qu'est-ce que LVM ?
	
	Ressource : https://doc.ubuntu-fr.org/lvm

	> LVM (Logical Volume Manager) permet la gestion de volumes logiques sous Linux similaire a un partitionnement de disques.
	> Avantages :
		>> Gestion plus souple et plus simple des tailles des systemes de fichiers, et sans risque.
		>> Permet de redimensionner les partitions sans formatage.
		>> Permet de rajouter des disques a la volee.
		>> Pas necessaire de connaitre l'emplacement exact des donnees sur le disque.
		>> Permet d'ajouter de l'espace memoire a tout moment.
		>> Possibilite de creer des snapshots (sauvegarde d'etat) de volume sans perturber le fonctionnement de la machine.
	> Inconvenients :
		>> Risque de perte de donnees en cas de defaillance du disque physique.
		>> Solution preventive possible avec l'utilisation d'un disque RAID.

	> Description de la partition chiffree avec LVM (commande lsblk pour acceder aux partitions).

********************************************************************************************************************************************
- Differences entre Aptitude et apt-get.
========================================
	Ressource : https://fr.linux-console.net/?p=1157#gsc.tab=0

	> Il s'agit de deux outils de gestion de package : activites, installations, suppressions, recherches, etc...
	> Ces deux outils sont initialement concus pour Debian, mais ont ete rendus compatibles avec RPN Package Manager.
	> Apt (Advanced Packiging Tool) : 
		>> Logiciel gratuit open source.
		>> Pas d'interface graphique. Ne fonctionne qu'en ligne de commande.
	> Aptitude :
		>> Gestionnaire de package avance avec une interface utilisateur basee sur la bibliotheque ncurse.
		>> Aptitude peut egalement emuler la plupart des commandes apt-get.
	> Differences :
		>> Aptitude =  haut niveau (interface utilisateur). Apt = bas niveau (ligne de commande).
		>> Aptitude a plus de fonctionnalites aue apt-get. Aptitude permet notamment de realiser des recherches de package, marquer un package a installer, le conserver pour mise a niveau, etc...
		>> Aptitude a une meilleure gestion des paquets. Par exemple :
			* Lors de la suppression d'un package,  Aptitude supprime automatiquement les packages inutilises. Apt-get necessite que le user demande explicitement leur suppression via la ligne de commande (-auto-remove ou apt-get autoremove).
			* Aptitude propose des commandes (why et why-not : commandes non disponible dans apt-get) qui permettent d'obtenir des informations sur certaines actions (interet, raisons de blocage, etc...).
			* Aptitude est capable de faire des suggestions au user en cas de probleme d'installation/suppression d'un package.
		>> D'une maniere generale Aptitude est plus complet et plus "intelligent" que apt-get dans la mesure ou :
			* D'une part il a plus de fonctionnalites.
			* D'autre part il va prendre des initiatives (suppression automatique de packages non utilises par exemple) et etre force de proposition en cas de conflits ou problemes. Avec apt-get le user doit utiliser des options ou variantes supplementaires en ligne de commande.

********************************************************************************************************************************************
- Qu'est-ce que SELinux ?
=========================
	> SELinux (Security-Enhanced Linux) est une architecture de securite pour systemes Linux qui permet aux administrateurs de mieux controler les acces au systeme.	

- Qu'est-ce que AppArmor ?
	
	> Le systeme de securite Linux fournit la securite MAC (Mandatory Access Control). Ce systeme d'administration permet de restreindre les actions que les processus peuvent realiser. Ce systeme est inclus par defaut avec Debian.
	> La commande aa-status permet de verifier s'il est actif.

********************************************************************************************************************************************
- Service SSH
=============
	> Qu'est-ce que SSH ?

		>> SSH (Secure SHell) est un mecanisme d'authentification entre un client et un environnement hote. 
		>> SSH encrypte les communications.
		>> Il est possible de se connecter a SSH sur un terminal Mac ou Linux.


	> Test du service SSH : mise en place d'un nouveau compte.

		>> sudo systemctl status ssh
		>> getent group sudo
		>> getent group user42
		>> sudo adduser new username
		>> sudo groupadd groupname
		>> sudo usermod -aG groupname username
		>> sudo chage -l username
		>> hostnamectl
		>> hostnamectl set-hostname new_hostname

********************************************************************************************************************************************
- Le pare-feu UFW devra etre actif au lancement de la VM.
=========================================================
	> sudo ufw status

********************************************************************************************************************************************
- Qu'est-ce que Cron (ou Crontab) ?
===================================
	> Il s'agit d'un planificateur de taches qui permet de lancer des applications de facon reguliere.
	> Dans le cadre du projet Born2beRoot, nous nous en servons pour afficher les informations du statut systeme toutes les 10 minutes dans le terminal de commandes de la VM.
	> crontab -l : permet a l'administrateur root d'afficher le contenu du fichier crontab.
	> mm hh jj MMM JJJ [user] tache > log : Exemple de masque de la ligne de commande qui permet de determiner la frequence d'execution du script Crontab.
	> m h dom mon dow * : Masque de la ligne de commande qui permet de determiner la frequence d'execution du script Crontab.
		>> m : minute.
		>> h : heure.
		>> dom : jour du mois.
		>> mon : mois.
		>> dow : jour de la semaine.
		>> * : joker pour n'importe laquelle des donnees precedentes.
	> */10 * * * * /usr/local/bin/monitoring.sh
		>> La syntaxe '*/10' permet d'executer le script monitoring.sh toutes les 10 minutes.
		>> Si a la place de '*/10', nous avions renseigne '10', alors le script s'executerait toutes les heures a Xh10m precises.

********************************************************************************************************************************************
- Modification du hostname.
===========================
	> hostnamectl : permet de monitorer le nom du hostname.
	> hostnamectl set-hostname new_hostname : permet de modifier le nom du hostname.

********************************************************************************************************************************************
- Configuration de la politique de securite des mots de passe.
==============================================================
	Ressources: 
	https://debian-facile.org/doc:securite:passwd:libpam-pwquality
	https://kifarunix.com/enforce-password-complexity-policy-on-ubuntu-18-04/
	https://manpages.ubuntu.com/manpages/impish/fr/man5/login.defs.5.html

	> sudo apt-get install libpam-pwquality : permet d'installer la bibliotheque de verification de la qualite des mots de passe.
	> sudo vim /etc/pam.d/common-password : ouverture du fichier de configuration des mots de passe.
	> Detail des options de configuration dans la ligne de commande (ligne 25 dans le fichier common-password) :
		>> retry=3 : Le user a trois essais pour saisir un mot de passe. Apres lesquels, abandon de la procedure.
		>> minlen=10: Le nombre de caracteres contenus dans le mot de passe doit etre de 10 au minimum. 
		>> ucredit=-1 : Le nombre de majuscules dans le mot de passe doit etre de 1 au minimum.
		>> dcredit=-1 : Le nombre de chiffres dans le mot de passe doit etre de 1 au minimum.
		>> maxrepeat=3 : Un meme caractere pourra etre present au maximum 3 fois dans le mot de passe.
		>> reject_username : Rejete le mot de passe s'il contient le nom du user, y compris s'il est saisi a l'envers.
		>> difok=7 : Le nouveau mot de passe doit comporter au moins 7 caracteres qui n'etaient pas presents dans le precedent.
		>> enforce_for_root : Renvoi un message d'erreur de la verification, y compris pour le root. Option absente par defaut : la bonne pratique est de l'ajouter systematiquement.

	> sudo vim /etc/login.defs : ouverture du fichier de configuration de la duree de validite :
		>> PASS_MAX_DAYS 30 : La modification du mot de passe est rendue obligatoire au bout de 30 jours. Possibilite d'entrer la valeur -1 pour desactiver cette option.
		>> PASS_MIN_DAYS 2 : La modification d'un mot de passe qui vient d'etre cree ne pourra pas etre faite avant 2 jours. Possibilite d'entrer la valeur -1 pour desactiver cette option.
		>> PASS_WARN_AGE 7 : Le user recevra un message d'avertissement 7 jours avant l'expiration de son mot de passe. Possibilite de desactiver cette option en entrant un nombre negatif ou en la laissant non renseignee.

********************************************************************************************************************************************
- Modification des mots de passe.
=================================
	> En mode user (laroges) :
		>> passwd ou sudo passwd.
		>> Entrer le mot de passe actuel.
		>> Entrer le nouveau mot de passe (attention aux a la politique de securite en vigueur).
		>> Confirmer le nouveau mot de passe.
		>> Si le nouveau de mot de passe est rejete et que le nombre d'essais a ete atteint, la procedure prend fin et le systeme indique explicitement au user que le mot de passe n'a pas ete modifie.

	> En mode administrateur (root) :
		>> pass ou sudo passwd + nom du user.
		>> Le systeme ne demande pas le mot de passe courant.
		>> Entrer et confirmer le nouveau mot de passe selon le meme principe que pour le user dans le point precedent.

********************************************************************************************************************************************
Commandes :
> lsblk : permet de consulter le "partitionnement".
> dpkg --list : permet de consulter la liste des packages installes.
> apt-cache policy <paquet> : permet de voir si un paquet est a jour.
> cd /usr/local/bin/ && nano monitoring.sh : permet de consulter le fichier de monitoring.
> sudo crontab -u root -e : permet d'editer le Cron.
> change script to */1 * * * * sleep 30s && script path : permet de lancer le script toutes les 30 secondes (supprimer la ligne de commande pour arreter le processus).
> su - : permet de se connecter en tant qu'administrateur (root).
> sudo ufw status : permet de verifier le statut du parefeu UFW.
> sudo systemctl status ssh : permet de controler le statut du systeme SSH.
> sha1sum laroges42.vdi : permet d'extraire la signature de la VM.
> ssh laroges@localhost -p 4243 : permet d'ouvrir la VM via ssh.
> uptime -s : permet de consulter les date et heure de connexion du user.
> sudo crontab -l : script
> aa-status : permet de verifier le statut de la securite MAC.


Dossiers et fichiers utiles de la VM :
> login.defs : permet de configurer les regles de securite des mots de passe (par exemple la duree de validite avant que le systeme impose au user la creation d'un nouveau).
> /var/log/sudo/sudo.log : chemin du fichier qui contient les informations de log sudo.

Autres :
- Le GUI (Graphical User Interface) est l'interface utilisateur de la VM.
- IMPORTANT : Le Snapshot1 correction aux parametres initiaux de la VM. Par consequent Snapshot1 ne doit JAMAIS etre ecrasee ! 
- Snapshot1 permet de "jouer" avec la VM en modifiant ses differents parametres, ajoutant/modifiant/supprimant des users, etc... (qui peuvent etre sauvegardes sous Snapshot2 par exemple) tout en ayant la possibilite de revenir aux parametres par defaut.

Ressources :
https://github.com/pasqualerossi/Born2BeRoot-Guide
https://github.com/pasqualerossi/Born2BeRoot-Guide#dont-have-virtual-box-installed
https://www.pierre-giraud.com/shell-bash/commande/

********************************************************************************************************************************************

A faire :
- Corriger la configuration du clavier dans la VM (a mettre en QWERTY) : FAIT !
	
	Methodologie pour memo :
		*J'ai reussi a mettre mon clavier en qwerty dans ma vm !!!
		*La manip qu'on faisait etait bonne, mais il manquait une commande a la fin.
		*En resume :
		*	sudo dpkg-reconfigure keyboard-configuration
		*	Options : Keyboard = 11. Apple aluminium (ANSI) && English(US)
		*	sudo systemctl restart console-setup.service
		*Enfin, saisie du mot de passe et bingo !
		*Source : https://forums.linuxmint.com/viewtopic.php?t=276831

- Rediger et expliquer le script en Bash.
	
	Objet : afficher des informations toutes les 10 minutes sur tous les terminaux (RTFM wall).
	
	Construction du script :
		
	> Commandes bash :

		- Architecture du systeme et version de kernel
			uname -a

		- Nombre de processeurs physiques
			grep "physical id" /proc/cpuinfo | sort | uniq | wc -l

		- Nombre de processeurs virtuels
			grep "processor" /proc/cpuinfo | wc -l

		- RAM disponible actuelle sur le serveur et taux d'utilisation en pourcentage
			free -m | awk '$1 == "Mem:" {print $2}'
			free -m | awk '$1 == "Mem:" {print $3}'
			free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}'

		- ROM disponible actuelle sur le serveur et taux d'utilisation en pourcentage
			df -BG | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}'
			df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}'

		- Taux d'utilisation actuelle des processeurs en pourcentage
			ft -BM | grep '^/dev/' | grep -v '/boot$/ | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}'

		- Date et heure du dernier redemarrage
			who -b | awk '$1 == "system" {print $3 " " $4}'

		- Statut du LVM (actif ou non)
			if [ $(lsblk | grep "lvm" | wc -l) -eq 0 ]; then echo no; else echo yes; fi

		- Nombre de users utilisant le serveur
			users | wc -w

		- Adresse IPv4 du serveur et adresse MAC
			hostname -I
			ip link shoz | grep "ether" | awk '{print $2}'

		- Nombre de commandes executees avec le programme sudo
			journalctl _COMM=sudo | grep COMMAND | wc -l

	> Toutes ces commandes ont fait l'objet de creations d'alias pour rendre la commande wall plus lisible.	


1. Machine virtuelle
	
	1.1	Systeme d'exploitation (OS) : generalites

		1.1.2	Kernel
			
			Ressource : https://www.jedha.co/blog/kernel-definition-utilite
	
			> Definition :
				
			Le Kernel est le "noyau" de l'OS. C'est un logiciel qui permet la communication entre les parties hardware et software de la machine.

			
	1.2	Presentation de Debian
	
		1.2.1	Origine story
		
			OS open source developpe par la base du volontariat.

		1.2.2	


2. Securite

	2.1	Parefeu

		2.1.1	Definition d'un parefeu

		2.1.2	Presentation de UFW


	2.2	Gestion des mots de passe

		2.2.1	Politique de securite

		

3. Service SSH


4. Administration

	3.1	Gestion des utilisateurs
