# Video Tutorial

Ce script permet à son utilisateur d'exécuter sélectivement une séquence de commandes afin d'illustrer un processus sans avoir à taper toutes ces commandes dans une fenêtre de terminal

# Table des matières

1.	[Comment utiliser ce script ?](#comment-utiliser-ce-script-)
2.	[Pourquoi ce script ?](#pourquoi-ce-script-)
3.	[Considérations techniques](#considérations-techniques)
4.	[Contribuer](#contribuer)
5.	[Vidéo de démonstration](#vidéo-de-démonstration)

# Comment utiliser ce script ?

Comme ce script permet de fournir des commandes et des descriptions pour montrer comment un processus donné est exécuté, il est nécessaire de fournir des commandes et des descriptions au script afin de les imprimer.

## Invocation

Il existe deux façons d'exécuter ce script :
1.	Vous pouvez exécuter le script en exécutant la commande suivante :
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/nsainton/video_tutorial/master/video.sh)
```
ce qui vous permettra d'exécuter le script avec ses arguments mais sans aucune installation requise.

2.	Vous pouvez installer le script à l'emplacement requis en remplaçant le chemin "$HOME/.local/bin/video.sh" par le chemin du fichier dans lequel vous souhaitez installer le script. Cette ligne de commande ajoutera également le répertoire cible au chemin
```bash
if [ ! -f "$HOME/.local/bin/video.sh" ]
    then curl -fsSL --connect-timeout 10 https://raw.githubusercontent.com/nsainton/video_tutorial/master/video.sh -o "$HOME/.local/bin/video.sh" \
    && { if { echo "$PATH" | grep "$HOME/.local/bin" ; }
        then echo "PATH=\"$HOME/.local/bin:$PATH\"" >> "$HOME/.$(basename $SHELL)rc"; echo "Path : \`$HOME/.local/bin added to path'" ; . "$HOME/.$(basename $SHELL)rc" ; fi ; } \
    && echo "Script installed at : $HOME/.local/bin/video.sh"
else
    echo "Script already installed at : $HOME/.local/bin/video.sh"
fi
```

## Un seul fichier qui stocke les commandes et les descriptions (méthode recommandée)

L'utilisateur peut entrer les commandes et les descriptions dans un seul fichier qui prendra la forme du fichier suivant :
```bash
commande 1 | Description 1
commande 2
commande 3 | Description 3
commande 4
@commande 5
@commande 6
commande 7 | Description 7
```

Dans cet exemple, nous pouvons observer qu'il existe 3 façons d'exécuter une commande dans une séquence avec ce script :
1.	commande | Description : la commande doit être séparée de la description par un séparateur. Le séparateur par défaut est `|' mais un autre séparateur peut être spécifié avec l'option -s séparateur.

<blockquote>

:bulb: Pour utiliser un séparateur qui est une séquence d'échappement (comme `\t` ou `\n`), il est nécessaire de le spécifier avec l'option `-s` de la manière suivante : `-s $'\t'` ou `-s $'\n'`.

Vous pouvez lancer la commande : 
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/nsainton/man_reader/master/man_reader.sh) bash QUOTING
```

</blockquote>

2.    commande : la commande sera imprimée et exécutée mais sans message descriptif
3.    @commande : la commande sera exécutée sans être imprimée (utile pour les commandes de configuration/nettoyage)

Un exemple de fichier de configuration avec un seul fichier de commandes et de descriptions est disponible [ici](/tests_commands/commands_and_descriptions.txt)

> :bulb: Pour tester ce fichier, vous pouvez exécuter : `./video.sh commands_file`

## Commandes et descriptions séparées en deux fichiers

L'utilisateur peut également séparer les commandes et les descriptions en deux fichiers distincts. Le fichier de commandes contiendra les commandes à exécuter et le fichier de descriptions contiendra les descriptions correspondantes.

Le fichier de commandes :
```bash
commande 1
commande 2
commande 3
@commande 4
@commande 5
commande 6
@commande 7
```

Et le fichier de descriptions :
```bash


Description 3


Description 6
```

Voici un exemple de fichier de [commandes](/tests_commands/commands.txt) et un exemple de fichier de [descriptions](/tests_commands/descriptions.txt) qu'il est possible d'utiliser pour tester le script.<br/>

> :bulb: Pour tester ces fichiers, vous pouvez exécuter : `./video.sh commands_file descriptions_file`

> :warning: L'index de la description doit correspondre à l'index de la commande qu'elle décrit.
> Par exemple, la description sur la ligne 3 correspond à la commande 3.

# Pourquoi ce script ?

Ce script a été créé pour permettre à son utilisateur de montrer un processus en exécutant sélectivement une séquence de commandes. Il a été créé pour être utilisé dans le cadre de la rédaction de tutoriels vidéo, mais il peut également être utilisé pour d'autres types de démonstrations.

## Pourquoi est-il utile et quels sont ses avantages ?

Ce script est utile pour les raisons suivantes :
1.	Il permet à l'utilisateur de montrer un processus en exécutant sélectivement une séquence de commandes
2.	Il permet à l'utilisateur de montrer un processus sans avoir à taper toutes les commandes dans une fenêtre de terminal
3.	Il permet à l'utilisateur de montrer un processus sans avoir à éditer une vidéo pour y inclure des commandes

# Considérations techniques

Ce script utilises les descripteurs de fichiers 6 et 7 pour récupérer ses inputs (soit de fichiers soit depuis la ligne de commande) pour n'avoir aucun conflit avec un script qui lit depuis l'entrée standard ou depuis un descripteur de fichier qui n'est ni 6 ni 7.

# Contribuer
Il y a plusieurs façons de contribuer à ce projet :
1.	En m'envoyant un message sur discord (pour les étudiants de 42) ou par [email](mailto:nsainton@student.42.fr?subject=[video_tutorial])
2.	Les Pull Requests sont pour le moment fermées mais seront bientôt ouvertes pour que vous puissiez ajouter toutes vos features au projet.

# Vidéo de démonstration

Cliquez sur la miniature pour voir la vidéo de démonstration