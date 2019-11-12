Consultation de l’historique et des modifcations
Nous avons déjà présenter dans la première partie les commandes pour consulter
l’historique.
Placez vous dans votre projet, nous allons consulter les deux derniers commit,
n’oubliez pas pour sortir de l’historique il faut taper la lettre “q” de votre clavier.
git log --oneline -2
Vous pouvez également consulter les commits d’un auteur en particulier :
git log --author "Antoine07"
Mais vous pouvez consulter l’historique à l’aide des commandes suivantes également
:
git log --since=1.day
git log --before="2019-09-01"
Vous pouvez également consulter l’historique d’un fichier uniquement :
git log calzone.txt
Vous pouvez également visualiser les modifications au sein d’un fichier ou de
l’ensemble/d’un ensemble des fichier(s) :
git log -p calzone.txt
# dans l'ensemble des commits
git log -p
# Ou pour les derniers commits
git log -2 -p
Exercice d’application
Modifiez la recette Calzone de la manière suivante
Pizza : Calzone
Coulis de tomate -->[modifiez en]--> Coulis de tomates cerises
mozzarella
jambon supérieur
champignons de Paris frais
oeuf
Puis faite un commit et visualisez les changements à l’aide de la commande git
log :
git log -p calzone.txt
1
Vous devriez voir maintenant, + et - sont respectivement ajouté et retiré
- Pizza : Calzone
-Coulis de tomate
+Pizza : Calzone
+Coulis de tomates cerises
mozzarella
jambon supérieur
champignons de Paris frais
Pour visualisez les changements ligne par ligne :
git log -p --word-diff calzone.txt
# l'option -U1 permet d'avoir que les lignes changées sans les méta-info
git log -p -U1 --word-diff calzone.txt
Une autre commande permet également de visualiser les statistiques des modifications
des fichiers :
git log --stat calzone.txt
Option –graph
Une dernière commande qui nous fera prendre conscience d’un point du cours
que nous reverrons : visualisation du graphe du dépôt :
git log --pretty=format:"%h %s" --graph
L’option de commande pretty permet de modifier le rendu des logs.
Remarque : Git est un graph orienté de commit, la notion de branche est une
notion primordiale dans Git.
Rechercher dans les logs
La commande suivante permet de rechercher des logs (messages des commits)
: E expression pour recherche les/l’occurence(s) et i pour insensible à la casse
(majuscule/minuscule) :
git log -E -i --grep='Pizza'
D’autres commandes possibles :
git log -S "Pizza"
# Plus dynamique
git log -G "Pizza(1|2)
2
Exercice recherche dans les logs
Recherchez les logs dans lequel le mot “Pizza” apparaît.
git blame
Il parfoit utile de savoir qui a fait la modification, lorsqu’on travaille à plusieurs
sur un même projet :
git blame calzone.tx
# b058c4f1 (Antoine07 2019-10-06 09:14:14 +0200 1) Pizza : Calzone
# b058c4f1 (Antoine07 2019-10-06 09:14:14 +0200 2) Coulis de tomates cerises
# ...
Visualiser les différences
Vous pouvez lorsque faite une modification dans un fichier avant de l’indexé
visualiser les modifications à l’aide de la commande suivante :
git diff
Exercice d’application sur les différences dans un fichier
Modifiez sans indexé le fichier calzone.txt en ajoutant la ligne suivante et tapez
la commande git diff dans le terminal :
supplément : gruyère + 5 €
git diff
La commande git diff affiche les modifications avant l’indexation. Si vous tapez
la commande diff avec l’option suivante vous ne verrez pas les modifications,
l’option –cached permet de visualiser les modifications de votre fichier avec le
dernier commit :
git diff --cached
Ajoutez dans l’index les modifications et retapez la commande ci-dessus vous
verrez maintenant les modifications :
git add calzone.txt
# git diff n'affiche plus rien
# par contre avec l'option --cached on affiche les diff dans l'index
git diff --cached
3
Voir modification après avoir commité
Vous pouvez voir les différence après avoir commité les changements, supposons
que l’on veuille voir les modifications un commit en arrière :
git diff HEAD~1
HEADˆ1 pour reculé d’un commit en arrière.
Visualiser entre deux positions du HEAD
Si on souhaite visualiser les différences entre le HEAD et un état antérieur du
dépôt, par exemple 3 commits avant :
git diff HEAD~3 HEAD
Visualiser les modifications entre deux commits donnés
Mais vous pouvez également voir les modifications entre deux commits :
# récupérez les haches des deux derniers commits
git log --oneline
# et étudier les différences entre deux commits
git log f5541d6 b058c4f
diff stat
Dernière commande : faire des stat sur les différences opérées dans les fichiers:
git diff --stat
# calzone.txt | 2 +-
Résumé git diff
git diff
Changements dans le répertoire de travail qui ne sont pas encore dans l’index.
git diff --cached
Changements dans l’index et le fichier dans l’espace de travail.
git HEAD
Changements dans le répertoire de travail et le dernier commit.
4
git restore
Annuler les modifications dans l’espace de travail (WD : working directory)
Modifiez le fichier calzone.txt comme suit, on met 300 euros pour le supplément
gruyère quelque chose d’absurde (. . . )
Pizza : Calzone
Coulis de tomates cerises
mozzarella
jambon supérieur
champignons de Paris frais
oeuf
supplément : gruyère + 300 €
Pour remettre le dépôt dans l’état dans lequel il se trouvait juste avant cette
modification absurde il suffit de tapez :
git restore calzone.txt
Par contre si on refait la modification et que l’on ajoute le fichier dans l’index il
faudra alors taper :
git restore --staged
• Créez le fichier calzone_super.txt avec le contenu suivant :
Pizza : Calzone Super
Coulis de tomates cerises & tomates russes
mozzarella
jambon supérieur
champignons de Paris frais
oeuf & lardon
supplément : gruyère + 5 €
Exercice restore
• Re-modifiez le fichier calzone.txt en mettant l’option gruyère à 300 euros
Le dépôt se retrouve donc dans l’état suivant :
• Un fichier modifier & un fichier non suivi
Ajoutez ces fichiers dans l’index. Remettez tout dans l’espace de travail.
Exercice working directory & index
1/ Excluez le fichier calzone_super.txt du versionning.
5
2/ Ajoutez le fichier calzone.txt dans l’index. Puis modifier ce même fichier
changez encore l’option supplément gruyère mettez + 8.5 euros :
Pizza : Calzone Super
Coulis de tomates cerises & tomates russes
mozzarella
jambon supérieur
champignons de Paris frais
oeuf & lardon
supplément : gruyère + 8.5 €
Dans quel état est votre dépot ?
Application
• Pour terminer voici la commande qu’il faut appliquer pour remettre le
dépôt dans l’état dans lequel il se trouvait avant ces derniers changements
: annulation des modifications de l’index et du WD. On se basera sur le
dernier commit pour le/les fichier(s) à remettre au(x) prope(s) dans le WD.
Le fichier calzone.txt est remi dans son état iniatial, nous avons annulé
tous ses changements :
git restore --source=HEAD --staged --worktree calzone.tx
Modifier un message de commit
• On peut modifier un message de commit à deux conditions :
1/ Qu’il n’y a pas eu d’autre commit entre temps
2/ Qu’on a pas “pusher” le commit sur une branche distante (serveur distant).
Exercice ajouter un index
Ajoutez un fichier index.txt il listera l’ensemble de nos pizzas non vegan :
Pizzas : liste
- calzone
- bellachao
- specials
- grill
- merguez
Faites un nouveau commit avec le message suivant “Ajout de la liste complète
de nos pizzas non vegan”
6
Puis modifiez le fichier index.txt pour ajouter la liste complète des pizzas avec
les pizzas vegans cette fois. Mais nous aimerions modifier maintenant le dernier
message de commit dans ce cas utilisez l’option –amend comme suit :
# Avant toute chose
git status
# vérifiez les deux derniers commits avant
git log -2
git commit -m "liste complète de toutes les pizzas" --amend
# vérifiez les deux derniers commits après
git log -2
Faites un git log pour vérifier qu’il n’y a pas eu de création d’un nouveau commit.
Pour terminez vous avez également une option intéressante :
$ git commit --amend --no-edit
Elle permet de ne pas changer le message du dernier commit tout en ne recréant
pas un commit pour les modifications apportées dans un fichier.
git reset HEAD~1
Nous parlerons ici que du cas où nous reculons d’un commit dans l’historique.
Parfois vous souhaiterez annuler des actions ou même les supprimer après avoir
fait un commit.
Voici quelques commandes qui vous permettrons d’annuler sans perte vos données
:
# Annule le dernier commit et met tout dans le WD sans perte (revient au commit précédent -1)
$ git reset HEAD~1
# Annule le dernier commit et met tout dans la staging area sans perte
$ git reset --soft HEAD~1
Exercice key_private & reset
Créez un nouveau dépôt example-reset_soft, les fichiers créés ci-dessous ne
nécessitent pas de contenu, ils seront utilisés uniquement pour exemple :
• Initialisez un nouveau dépôt.
• Dans ce dépôt créez un fichier file1.txt (commit).
7
• Créez maintenant un fichier .gitignore ne mettez rien pour l’instant dans
ce fichier (commit).
• Créez un autre fichier file2.txt (commit).
• Créez un fichier key_secret.sh et mettez des clés secrètes dans ce fichier
(commit).
Vous vous apercevez maintenant que vous avez commité des clés secrètes.
• 1/ Corrigez le problème.
• 2/ Excluez le fichier key_secret.sh de l’historique de Git.
git reset [commit]
Vous pouvez annuler plusieurs commits en revenant en arrière dans l’historique,
mais dans ce cas attention à la cohérence de votre historique.
Supposons que nous ayons l’historique suivant et la copie de travail est propre :
124f561 (HEAD -> master) file33
6695308 file22
0637561 file11
8ef0ef2 ignore
0a70edb file2
bf3f73c first commit
Alors si vous tapez la commande suivante :
git reset 8ef0ef2
Le HEAD -> master se déplacera sur ce commit en annulant les autres commits
(messages) sans perte :
8ef0ef2 (HEAD -> master) ignore
0a70edb file2
bf3f73c first commit
Aucun fichier(s) ou modification(s) ne seront/ n’est perdu(s). Tout est replacé
dans le WD.
git reste –hard
Parfois vous voudriez supprimer un commit avec le(s) fichier(s). Bien sûr cette
commande est très dangeureuse car vous ne pourrez pas retrouver dans ce
cas votre travail. Donc elle est à faire avec beaucoup de prudence.
# Annule le dernier commit et supprime les modifications...(danger)
$ git reset --hard HEAD~1
8
git checkout
Nous allons utiliser cette commande pour remettre un fichier dans son état
initial.
Exercice d’application checkout
• Créez un dépôt example-checkout
• Initialisez le dépôt
Chaque étape ci-dessous doit donner lieu à un commit :
• Créez un fichier index.html dans lequel vous mettez uniquement la chaîne
de caractères suivante : Hello world.
• Créez le fichier category.html.
• Modifiez le fichier index.html dans lequel vous mettez maintenant du code
HTML et dans le body et un h1 la chaîne de caractères “Hello World”. Le
message du commit s’appelera “refonte de la page d’accueil”.
Vous devriez avoir quelque chose qui ressemble à l’historique suivant :
5050a3a (HEAD -> master) refonte de la page d'accueil
9b85968 add category
8a56381 add index
Nous aimerions annuler la refonte de la page d’accueil et revenir dans l’état
initial. Dans ce cas vous pouvez utiliser la commande suivante :
# Permet de revenir avant la refonte
$ git checkout 9b85968 index.html
$ git status
# modifié : index.html
En interprétant le message du git status que proposez-vous comme solution pour
valider les modifications et donc revenir dans l’état initial du fichier index.html
(avant la refonte) ?
9