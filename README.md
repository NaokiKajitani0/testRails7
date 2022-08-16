# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

* about install bootstrap  
  about CSS
    write Dockerfile
      # install nodejs(LTS)
        RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - && apt-get install -y nodejs

      # install yarn
        RUN npm install --global yarn
        RUN yarn add bootstrap jquery popper.js
  
    write Gemfile
      # Use Sass to process CSS
        gem "sassc-rails"

        gem 'bootstrap', '~> 5.1.3'

    Bundle install 

    application.css → application.scss and application.scss write
      add: 
        @import "bootstrap";
      remove:
        //=require_tree
        // require ??

    application.js write
      import "bootstrap"
      import "../stylesheets/application.scss"

  about JS
    write manifest.js
      //= link bootstrap.min.js
      //= link popper.js
    
    write Dockerfile (reflect package.json)
      RUN yarn add bootstrap jquery popper.js ($yarn add bootstrap jquery popper.js)
      
    write application.js
      import "popper"
      import "bootstrap"

    write importmap
      pin "popper", to: 'popper.js', preload: true
      pin "bootstrap", to: 'bootstrap.min.js', preload: true
        ※注意点としては、まずpopperをbootstrapよりも先に読み込む必要がある。
        https://qiita.com/soma_sekimoto/items/67b7f005b96cd9b3afb1
        さらにコマンドにて("./bin/importmap:install")でもimportmapに書き込みができるが、反映されない様子。
        下記にそちらのコードを記載しておく。
          pin "@popperjs/core", to: "https://ga.jspm.io/npm:@popperjs/core@2.11.6/lib/index.d.ts"
          pin "bootstrap", to: "https://ga.jspm.io/npm:bootstrap@5.2.0/dist/js/bootstrap.esm.js"