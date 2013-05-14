TP BDISE
=====

Objectifs séance 1 :
=====
- Création de binomes
- Installation de votre environnement
- Création d'un compte Github
- Génération d'une nouvelle application
- Commit de l'application


Installation de votre VM :

```
wget -q -O - "$@" https://raw.github.com/jlerpscher/BDISE/master/install-ubuntu.sh | bash
```

Pendant ce temps, amusons-nous !
=====

Trouver tous les membres :
```
Member.all
```

Trouver le membre ayant l'id 1 :
```
Member.find(1)
```

Trouver le(s) membre(s) ayant le prénom Julien :
```
Member.find_by_firstname('Julien')
```

Créer un nouveau membre :
```
Member.create(firstname: 'foo', lastname: 'bar')
```

Trouver le dernier membre :
```
Member.last
```

Trouver tous les membres ordonnés par prénoms :
```
Member.order(:firstname)
```

Changer le nom du membre ayant l'id 3 :
```
Member.fin­d(3).updat­e_attribut­e(:lastname, 'newname')­
```

Supprimer le membre ayant l'id 3 :
```
Member.find(3).destroy
```

Un peu de magie !
=====

Quelle heure est-il ?
```
Time.now
```

Sommes-nous lundi ?
```
Time.now.monday?
```
Sommes-nous mercredi ?
```
Time.now.wednesday?
```

Quel jour était-on il y à 23 jours ?
```
Time.now - 23.days
```

Opérations sur les tableaux : 
```
a = %w(foo bar test hello)
b = %w(foo hello)
a - b
=> ["bar", "test"]
```

Allons-y !
======

Création d'une nouvelle application
```
rails new cvcollect
```

Démarrage du serveur
```
cd cvcollect
rails s
```

Notre nouvelle application est disponible ici :
```
http://localhost:3000
```

Pour les étudiants ayant un message d'erreur au démarrage de l'application :
```
sudo apt-get install libv8-dev
```


Objectifs séance 2 :
=====

- Installer quelques gems
- Apprendre à utiliser le fichier routes.rb
- Créer notre première vue
- Créer notre premier controleur
- Créer notre premier modèle avec notre première migration
- Déployer notre nouvelle application dans le cloud

Pour commencer, voici la liste des gems à ajouter dans le Gemfile :

```
gem 'sqlite3'
gem 'haml'
gem 'bourbon'
gem 'will_paginate'
gem 'rails-i18n'
```

Pour les installer, on utilise la commande :
```
bundle
```

Suppression de la page par défaut de rails : 
```
rm public/index.html
```

Création de notre première route :
```
root :to => 'pages#index'
```

Création de notre controlleur pages :
```
rails g controller pages
```

Renommer le fichiers scss généré en sass :
```
mv app/assets/stylesheets/pages.css.scss app/assets/stylesheets/pages.css.sass
```

Créer l'action index du controlleur pages :
```
class PagesController < ApplicationController
  def index
  end
end
```

Créer une nouvelle vue index.html.haml dans le dossier app/views/pages
```
= t('.welcome')
```
