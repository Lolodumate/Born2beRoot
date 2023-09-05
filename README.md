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
- Questions generales sur le systeme d'exploitation.
- Difference entre Aptitude et apt.
- Qu'est-ce que SELinux ?
- Qu'est-ce que AppArmor ?
- Test du service SSH : mise en place d'un nouveau compte.
- Question sur le fonctionnement du service SSH.
- Le pare-feu UFW devra etre actif au lancement de la VM.
- Modification du hostname durant la soutenance.
- Savoir expliquer l'administration des regles de securite des mots de passe.

Commandes :
sha1sum laroges42.vdi : permet d'extraire la signature de la VM.
ssh laroges@localhost -p 4241 : permet d'ouvrir la VM via ssh.
uptime -s : permet de consulter les date et heure de connexion du user.
sudo crontab -l : script


Dossiers et fichiers utiles de la VM :
login.defs : permet de configurer les regles de securite des mots de passe (par exemple la duree de validite avant que le systeme impose au user la creation d'un nouveau).

Ressources :
https://github.com/pasqualerossi/Born2BeRoot-Guide
https://github.com/pasqualerossi/Born2BeRoot-Guide#dont-have-virtual-box-installed

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

- Rediger le script.


1. Machine virtuelle
	
	1.1	Systeme d'exploitation : generalites

	1.2	Presentation de Debian


2. Securite

	2.1	Parefeu

		2.1.1	Definition d'un parefeu

		2.1.2	Presentation de UFW


	2.2	Gestion des mots de passe

		2.2.1	Politique de secu


3. Service SSH
