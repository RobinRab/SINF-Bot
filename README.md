<h1 align="center">
	🤖 Anon
</h1>

<p align="center">
	<b><i>Un bot parfait sans aucun bug</i></b><br>
</p>

<p align="center">
	<img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/RobinRab/SINF-Bot?color=lightblue" />
	<img alt="Number of lines of code" src="https://img.shields.io/tokei/lines/github/RobinRab/SINF-Bot?color=critical" />
	<img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/RobinRab/SINF-Bot?color=green" />
</p>

<h3 align="center">
	<a href="#-dépendances">Dépendances</a>
	<span> · </span>
	<a href="#%EF%B8%8F-setup-des-tests">Setup</a>
	<span> · </span>
	<a href="#-partager-vos-modifications">Ensemble</a>
	<span> · </span>
	<a href="#-comment-ça-marche">Fonctionnement</a>
</h3>


# 💡 À propos
Ce dépôt contient le code source du bot Anon, du serveur discord Sinf Illégal Family. Tout le monde peut participer à son développement.



# 📖 Dépendances
Pour faire fonctionner le code du bot vous allez avoir besoin d'installer plusieurs dépendances 

## 1. python3.11
Le bot discord qui tourne en permanence demande de nombreuses ressources, il tourne donc sur la dernière version de python (3.11) car elle est plus rapide de 60% et permet l'utilisation de plus d'outils

## 2. git
Pour ce projet git vous aurez besoin d'installer git sur votre machine, ça vous permettra de clone le projet ainsi que d'y apporter des modifications
```
python3.11 -m pip install git
```

## 3. dotenv
Le module dotenv permet de lire un fichier `.env` dans votre dépôt, celui-ci sera nécessaire plus tard
```
python3.11 -m pip install python-dotenv
```

## 4. requests
Le module requests est indispensable pour faire des requêtes à internet. Le bot en aura besoin pour se connecter à l'API de tetrio, ou encore lorsqu'il a besoin de manipuler des fichiers discord
```
python3.11 -m pip install requests
```

## 5. discord
Le module discord est indispensable pour la création d'un bot... discord.
```
python3.11 -m pip install -U discord
```


# 🛠️ Setup des tests
## 1. créer votre bot de test
> ### 1. Connectez vous à discord et rendez-vous sur [Discord Developper Portal](https://discord.com/developers/applications)
> ### 2. Cliquez sur "New Application"
> ### 3. Donnez lui un nom et appuyez sur "create"
> ### 4. Allez dans l'onglet 'Bot' et cliquez sur "Add bot" 
> ### 5. Désactivez "Public bot"
> ### 6. Activez les 3 checks intents 
> ### 7. rejoingnez le serveur de [testing](https://discord.gg/5braTFUa8h)
> ### 8. Dans le portal, allez dans Oauth2/URL GENERATOR, sélectionnez 'bot' puis 'administator' et copiez le lien dans le navigateur
Vous voici désormais prêt avec votre bot pour tous les tests, ceci est nécessaire par sécurité pour le serveur principal ainsi que pour éviter les spams que certains tests peuvent provoquer. <br> Sur votre compte discord, je vous conseille d'aller dans settings/Advanced et d'activer le mode développeur, cela vous permettra de copier l'ID de vos messages, serveurs, etc.

## 2. forker le projet
Pour forker le projet, cliquez sur le bouton "fork" en haut à droite de la page, vous aurez alors une copie du projet sur votre compte github. <br> Vous pouvez maintenant cloner le projet sur votre machine via git et le modifier comme ci-dessous

## 3. créer le fichier `.env`
Dans le dossier principal, créer un fichier `.env` contenant toutes vos variables personnelles, celles-ci ne seront pas partagées avec les autres développeurs. <br> Le fichier `.env` doit contenir les variables suivantes:
```py
BOT_PREFIX = "!!"
DISCORD_API_TOKEN = "your secret token here"

BOT_ID = int
GUILD_ID = 1079214079161417879
ERROR_CHANNEL_ID = 1079217228081283122

ANON_SAYS_ID = 1079223122592550982
GENERAL_ID = 1079214079161417882
CONFESSION_ID = 1079217281449590836
CUTIE_ID = 1079337720041705472
```
**BOT_PREFIX** est le préfixe que vous voulez donner à votre bot, par exemple `!!` ou `?` <br>
**DISCORD_API_TOKEN** est le token de votre bot que vous trouverez dans dans le portal/bot/ <br> 
**BOT_ID** est l'ID de votre bot, vous pouvez le trouver dans "General Information" du portal <br>
Les autres ID correspondent déjà à ceux sur le serveur de test, vous pouvez les laisser tels quels

## 4. Lancer le bot 🚀
```py
python3.11 src/main.py
```
Le bot devrait maintenant être en ligne, vous pouvez le tester comme vous le souhaitez. Pour l'arrêter, appuyez sur `CTRL + C` dans le terminal

# 📡 Partager vos modifications
Premièrement, vous devez connecter votre fork au projet original 
```
git remote add upstream https://github.com/RobinRab/SINF-Bot
```
Lorsque votre nouvelle commande a bien été testée et que vous souhaitez la partager avec les autres développeurs, suivez ces étapes dans votre terminal:
```
git fetch upstream
git merge upstream/main
git add .
git commit -m "explication de vos changements"
git push origin main
```
Les explications dans l'ordre sont les suivantes : 
> #### git se connecte à la branche en ligne
> #### git merge la branche en ligne à vos changements pour pas que votre request ait du retard
> #### git ajoute tous les fichiers modifiés
> #### git commit vos changements avec un message explicatif
> #### git push vos changements sur votre fork
Ensuite, vous devez créer une pull request. <br> Pour cela, rendez-vous sur votre fork du projet, cliquez sur le bouton "pull request" et suivez les instructions. <br> Une fois la pull request créée, un développeur va la vérifier et la merger dans le projet principal <br> <br> 

# 📝 Comment ça marche?
## `Main.py`
Le fichier `main.py` est le fichier principal, c'est lui qui va lancer le bot et qui va importer les commandes qui se trouvent sous forme d'extensions 
```py
bot = commands.Bot( 
	command_prefix=[settings.BOT_PREFIX, f"<@!{settings.BOT_ID}> "],
	case_insensitive=True,
	help_command=None,
	intents=intents,
	strip_after_prefix=True
)
bot.tree.synced : bool = False
```
créer l'objet bot, il est aussi possible de lui ajouter des attributs comme `bot.tree.synced` qui permet de savoir si l'arbre a été synchronisé ou non

```py
@bot.event
async def on_ready():
	for ext in settings.extensions:
		await bot.load_extension(ext)
		log("INFO", f"{ext} loaded ")
```
Lorsque le bot est prêt, il va charger toutes les extensions qui se trouvent dans le fichier `settings.py`

## `settings.py`
Le fichier `settings.py` contient toutes les variables globales du projet, il défini les variables, les routes, les extensions ainsi que un logger pour garder une trace des erreurs. C'est un fichier senssible, il ne devrait pas être modifé excepté en cas d'ajout de fonctionnalités

## `utils.py`
Le fichier `utils.py` contient toutes les fonctions utiles au projet, vous pouvez ajouter dans ce fichier toutes les fonctions qui seront utilisées dans plusieurs fichiers

## `.gitignore`
Le fichier `.gitignore` permet d'ignorer certains fichiers lors de l'upload sur github, il est important de ne jamais supprimer des lignes

## `cmds/` 

#### Le dossier `cmds/` contient tous les fichiers qui contiennent les commandes du bot, il est important de respecter leur structure. 
<br>

---

## Vous trouverez plus d'informations sur le code en lisant la [documentation](https://discordpy.readthedocs.io/en/stable/)
--- 