### Exercice 1. Commandes de base


#### Commencez par mettre à jour votre système avec les commandes vues dans le cours. Donnez les commandes répondant aux questions suivantes :

#### 1. Quels sont les 5 derniers paquets installés sur votre machine ?

La commande qui permet de lister les 5 derniers paquets est : `grep "installed"  /var/log/dpkg.log | tail -5`

#### 2. Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel !).
en apt : `apt list -- installed | wc -l` : 515
en dpkg : `dpkg -l | grep "ii" | wc -l` : 514

#### 3. Combien de paquets sont disponibles en téléchargement ?
`apt list | wc -l`.
```
WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

64118
```
#### 4. Créer un alias “maj” qui met à jour le système
Tout d'abord je vais ajouter mon alias dans le fichier .bashrc avec `nano` 
Dans le bashrc j'ai fait : `alias maj='apt update && apt upgrade`.
Enfin j'ai actualisé le bash: `source ~/.bashrc`

#### 5. A quoi sert le paquet fortunes ? Installez-le.
J'ai fait `apt show fortunes` pour savoir a quoi sert le paquet fortunes,  Il s’agit d’un programme affichant des épigrammes, connues sous le nom de cookies fortune, choisies aléatoirement à partir de fichiers fortune.
Pour installer le paquet fortune il suffit de faire : ` apt-get install fortunes`.

#### 6. Quels paquets proposent de jouer au sudoku ?
Avec `apt-cache search sudoku` il y'a plusieurs résultats :

```
hitori - Jeu de puzzle logique similaire au sudoku
ksudoku - Jeu et Solveur de Sudoku
sudoku - Sudoku en mode console
texlive-games - TeX Live : Composition de jeux
nudoku - ncurses based sudoku games
```

#### 7. Lister les derniers paquets installés explicitement avec la commande apt install

Avec `cat /var/log/dpkg.log`, je remarque notamment que le paquet fortunes a été installé recemment.

### Exercice 2.
#### A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une seule commande, pour n’importe quel programme (indice : la réponse est dans le poly de cours 2, dans la liste des commandes utiles) ? Utilisez la réponse à pour écrire un script appelé origine-commande (sans l’extension.sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.
`which -a ls | xargs dpkg -s 2> /dev/null`

### Exercice 3.
#### Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package spécifié dans cette commande.

```
!/bin/bash
if [ -z "$1" ]; then
        echo "Non installé."
else
        dpkg -S $(which "$1");
        echo "Installé";
fi
```

### Exercice 4.
#### Lister les programmes livrés avec coreutils. A quoi sert la commande ’[’ et comment afficher ce qu’elle retourne ?

La commande permettant de lister les programmes est :`apt show coreutils`

### Exercice 5. aptitude
#### Installez le paquet emacs à l’aide de la version graphique d’aptitude.

Tout d'abord j'installe aptitude avec la commande: `apt install aptitude`.
Ensuite j'ai recherché dans aptitude le paquet emacs avec le / puis j'ai tapé emacs. Pour trouver le paquet j'ai appuyé 2fois sur n pour changer de page et apres etre tombé dessus j'ai installé le paquet : Tout d'abord avec + pour selectionner tous les paquets correspondants et enfin deux fois sur g.

### Exercice 6
#### Installation d’un paquet par PPA
Certains logiciels ne figurent pas dans les dépôts officiels. C’est le cas par exemple de la version ”officielle”
de Java depuis qu’elle est développée par Oracle. Dans ces cas, on peut parfois se tourner vers un ”dépôt
personnel” ou PPA.
1. Installer la version Oracle de Java (avec l’ajout des PPA)
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java12-installer
2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?
Exercice 7. Création de dépôt personnalisé

