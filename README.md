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

Modifié le fichier config/locales/en.yml :
```
en:
  pages:
    index:
      welcome: "Welcome!"
```


Créer un nouveau fichier de traduction appelé fr.yml dans config/locales :
```
fr:
  pages:
    index:
      welcome: "Bienvenue !"
```

Dans le fichier routes, ajouter la contrainte locale :
```
Cvcollect::Application.routes.draw do

  scope ':locale', :constraints => { :locale => /fr|en/ } do
    root :to => 'pages#index' 
  end

  root :to => 'pages#index'
  
end
```

Dans le fichier config/application.rb, mettre la locale par défaut à fr (décommenter ligne 34) :
```
config.i18n.default_locale = :fr
```

Ajouter un before filter permettant de setter la locale (app/controllers/application_controller.rb :
```
class ApplicationController < ActionController::Base
  protect_from_forgery

  before_filter :set_locale

  def set_locale
    I18n.locale = params[:locale] || I18n.default_locale
  end
end
```

Votre application est disponible en français ou en anglais aux adresses :
```
localhost:3000/fr
localhost:3000/en
```

N'oubliez pas de commiter et de pusher votre travail !!!


Objectifs séance 3 :
=====

Créer notre première page
Créer notre premier modèle
Créer notre première migration
Déployer notre application


Travail à faire :

1- Sur la page index, ajouter un lien permettant de changer de langue. Le lien doit envoyer vers l'anglais si nous sommes en français et vers le français si nous commes en anglais.

2- Installer la gem Devise (https://github.com/plataformatec/devise), pour cela, aidez-vous du "Getting started" disponible sur la page Github :
```
gem 'devise' (dans votre Gemfile)
bundle
rails g devise:install
rails g devise User
rake db:migrate
```

Ajouter la ligne suivante dans config/environments/development.rb
```
config.action_mailer.default_url_options = { :host => 'localhost:3000' }
```
 

Dans le layout (app/views/layouts/application.html.erb) que vous pouvez, si vous le souhaitez, convertir en haml, ajouter les lignes suivantes après l'ouverture de <body> :
```
<p class="notice"><%= notice %></p>
<p class="alert"><%= alert %></p>
```

Enfin, dans le fichier config/application.rb, ajouter la ligne :
```
config.assets.initialize_on_precompile = false
```
