# izneo-get
Ce script permet de récupérer une BD présente sur https://www.izneo.com/fr/ dans la limite des capacités de notre compte existant.

Le but est de pouvoir lire une BD sur un support non compatible avec les applications fournies par Izneo. 
Il est évident que les BD ne doivent en aucun cas être conservées une fois la lecture terminée ou lorsque votre abonnement ne vous permet plus de la lire.


## Utilisation
### izneo_get
### izneo_get_selenium
**Utilisation**  
```
python izneo_get_selenium.py [-h] [--session-id SESSION_ID] [--cfduid CFDUID]
                    [--output-folder OUTPUT_FOLDER]
                    [--output-format {jpg,both,cbz}] [--config CONFIG]
                    [--from-page FROM_PAGE] [--limit LIMIT] [--pause PAUSE]
                    [--full-only] [--continue] [--user-agent USER_AGENT]
                    [--webp WEBP] [--tree] [--force-title FORCE_TITLE]
                    [--encoding ENCODING]
                    url

Script pour sauvegarder une BD Izneo.
Ce script utilise désormais un driver Chrome piloté par Selenium.

positional arguments:
  url                   L'URL de la BD à récupérer ou le chemin vers un
                        fichier local contenant une liste d'URLs

optional arguments:
  -h, --help            show this help message and exit
  --session-id SESSION_ID, -s SESSION_ID
                        L'identifiant de session
  --cfduid CFDUID, -c CFDUID
                        L'identifiant cfduid
  --output-folder OUTPUT_FOLDER, -o OUTPUT_FOLDER
                        Répertoire racine de téléchargement
  --output-format {jpg,both,cbz}, -f {jpg,both,cbz}
                        Répertoire racine de téléchargement
  --config CONFIG       Fichier de configuration
  --from-page FROM_PAGE
                        Première page à récupérer (défaut : 0)
  --limit LIMIT         Nombre de pages à récupérer au maximum (défaut : 1000)
  --pause PAUSE         Pause (en secondes) à respecter après chaque
                        téléchargement d'image
  --full-only           Ne prend que les liens de BD disponible dans
                        l'abonnement
  --continue            Pour reprendre là où on en était
  --user-agent USER_AGENT
                        User agent à utiliser
  --webp WEBP           Conversion en webp avec une certaine qualité (exemple
                        : --webp 75)
  --tree             Pour créer l'arborescence dans le répertoire de
                        téléchargement
  --force-title FORCE_TITLE
                        Le titre à utiliser dans les noms de fichier, à la
                        place de celui trouvé sur la page
  --encoding ENCODING   L'encoding du fichier d'entrée de liste d'URLs (ex : "utf-8")
```

Exemple :  
Pour récupérer la BD dans un répertoire d'images (fichier de config présent) :  
```
python izneo_get.py https://www.izneo.com/fr/manga-et-simultrad/shonen/assassination-classroom-4744/assassination-classroom-t1-19197
```


Pour récupérer la BD dans une archive CBZ en forçant le titre (fichier de config présent) :  
```
python izneo_get.py https://www.izneo.com/fr/manga-et-simultrad/shonen/assassination-classroom-4744/assassination-classroom-t1-19197 -f cbz --force-title "[Yusei Matsui] Assassination Classroom - Tome 1"
```

Pour récupérer la BD dans une archive CBZ avec des images converties en WEBP (fichier de config présent) :  
```
python izneo_get.py https://www.izneo.com/fr/manga-et-simultrad/shonen/assassination-classroom-4744/assassination-classroom-t1-19197 -f cbz --webp 70
```

Pour récupérer une liste de BDs, dans un répertoire d'images correspondant à l'arborescence du serveur, sans fichier de config présent :  
```
python izneo_get.py /tmp/input.txt -c abcdef12345678901234567890123456789012345678 -s abcdefghijkl123456789012345 -o /tmp/DOWNLOADS --tree
```


CFDUID est la valeur de "cfduid" dans le cookie.  
SESSION_ID est la valeur de "c03aab1711dbd2a02ea11200dde3e3d1" dans le cookie.  

Pour les obtenir, identifiez vous sur https://www.izneo.com/fr/ et recherchez votre cookie avec votre navigateur web.

#### Chrome  
Menu --> Plus d'outils --> Outils de développements  
Application / Storage / Cookies  
et recherchez le cookie "https://www.izneo.com".  


#### Firefox  
Menu --> Developpement web --> Inspecteur de stockage --> Cookies  
et recherchez le cookie "https://www.izneo.com".  


Ces valeurs peuvent être stockées dans le fichier de configuration "izneo_get_selenium.cfg".  


### izneo_list
**Utilisation**  
```
python izneo_list.py [-h] [--session-id SESSION_ID] [--cfduid CFDUID]
                     [--config CONFIG] [--pause PAUSE] [--full-only]
                     [--series] [--force-title]
                     search

Script pour obtenir une liste de BDs Izneo.

positional arguments:
  search                La page de série qui contient une liste de BDs

optional arguments:
  -h, --help            show this help message and exit
  --session-id SESSION_ID, -s SESSION_ID
                        L'identifiant de session
  --cfduid CFDUID, -c CFDUID
                        L'identifiant cfduid
  --config CONFIG       Fichier de configuration
  --pause PAUSE         Pause (en secondes) à respecter après chaque appel de
                        page
  --full-only           Ne prend que les liens de BD disponible dans
                        l'abonnement
  --series              La recherche ne se fait que sur les séries
  --force-title         Ajoute l'élément "--force-tilte" dans la sortie
```

Exemple :  
Pour récupérer la liste des liens d'une série (fichier de config présent) :  
```
python izneo_list.py https://www.izneo.com/fr/manga-et-simultrad/shonen/naruto-567
```

Pour récupérer la liste des liens d'une série, dans la limite des albums complets inclus dans l'abonnement en ajoutant le tag "--force-title" (fichier de config présent) :  
```
python izneo_list.py https://www.izneo.com/fr/manga-et-simultrad/shonen/naruto-567 --full-only --force-title
```

Pour récupérer la liste des liens d'albums qui correspondent à la rechercher "largo" (fichier de config présent) :  
```
python izneo_list.py "largo"
```

Pour récupérer la liste des liens de séries qui correspondent à la rechercher "largo" (fichier de config présent) :  
```
python izneo_list.py "largo" --series
```


## Installation
### Prérequis
- Python 3.7+ (non testé avec les versions précédentes)
- pip
- Librairies SSL
- Drivers Chrome

#### Sous Windows
##### Python
Allez sur ce site :  
https://www.python.org/downloads/windows/  
et suivez les instructions d'installation de Python 3.

##### Pip
- Téléchargez [get-pip.py](https://bootstrap.pypa.io/get-pip.py) dans un répertoire.
- Ouvrez une ligne de commande et mettez vous dans ce répertoire.
- Entrez la commande suivante :  
```
python get-pip.py
```
- Voilà ! Pip est installé !
- Vous pouvez vérifier en tapant la commande :  
```
pip -v
```

##### Librairies SSL
- Vous pouvez essayer de les installer avec la commande :  
```
pip install pyopenssl
```
- Vous pouvez télécharger [OpenSSL pour Windows](http://gnuwin32.sourceforge.net/packages/openssl.htm). 

##### Drivers Chrome
- Il faut télécharger le fichier "chromedriver.exe" [sur le site de Chromium](https://chromedriver.chromium.org/downloads) et le copier dans le répertoire 
```
bin\
```
- Il est possible de le renommer en "chromedriverXX.exe" où "XX" est le numéro de la version. Le système ira chercher celui qui convient à votre version de Chrome installée.


#### Sous Linux
Si vous êtes sous Linux, vous n'avez pas besoin de moi pour installer Python, Pip ou SSL...  

### Téléchargement
- Vous pouvez cloner le repo git :  
```
git clone https://github.com/izneo-get/izneo-get.git
```
ou  
- Vous pouvez télécharger uniquement le binaire Windows (expérimental).  


### Configuration
(pour la version "script" uniquement)
```
pip install -r requirements.txt
```
