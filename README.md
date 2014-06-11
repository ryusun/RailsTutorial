RailsTutorial
=============

[rails tutorial](http://railstutorial.jp)  

* Start 2014-06-10 

## Rubyのインストール  
rbenvを使って2.0をインストールした  
rbenvは導入済みだった  

## gemのupdate  
```
gem update --system (version)
```
(version)にバージョンを指定することで、gemの指定したバージョンを取得することが可能。  

## .gemrcにgemの設定を記述する  
```.gemrc
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
```
これでriとrdocのインストールを省くことができる。  
今まで、gem install xx --no-rdoc --no-ri  
と書いていたのが楽になります。  

## rails install  
```rails
gem install rails --version 4.0.5
```
railsの4.0.5のインストール  

```rails
rails -v
```
で、railsのバージョンを確認できる。  

## 最初のアプリケーション  

下記のコマンドでアプリケーションを作成できる。  

```rails
rails new (App Name)
```

* Rails Appのディレクトリ構造  
忘れそうなところだけ記載  

** apps/assets  
アプリケーションで使用するCSS,JavaScriptファイル、画像などのアセット  

** lib/assets  
ライブラリで使用するCSS,JavaScriptファイル、画像などのアセット  

** public  
エラーページなど、一般(Webブラウザなど)に直接公開されるデータ  

** bin/rails  
コード生成、コンソールの起動、ローカルのWebサーバーの立ち上げなどに使用するRailsスクリプト  

** test  
アプリケーションのテストで使用していたが、あとで出てくるspecディレクトリがあるため、現在は使用されない。  

** vendor  
サードパーティのプラグインやgemなど  

** vendor/assets  
サードパーティのプラグインやgemで使用するCSS、Javascriptファイル、画像などのアセット  

** Rakefile  
rakeコマンドで使用可能なタスク  

** Gemfile  
このアプリケーションに必要なGemの定義ファイル  

** Gemfile.lock  
アプリケーションのすべてのコピーが同じgemのバージョンを使用していることを確認するために使用されるgemのリスト  

** config.ru  
Rackミドルウェア用の設定ファイル  

今までなんとなく見てました...。 


## 1.2.4 Bundler  

* Bundlerの文法  
Gemfileを開くと、GemとBundlerの文法例がコメントで書かれているので読んでおこう。  

* gemコマンドで取得されるバージョン  
特定のバージョン番号指定がない限り、Bundlerは自動的に最新バージョンのgemを取得してインストールする  

* gemのバージョン指定方法   

```
gem 'uglifier', '>=1.3.0'
```

この意味するところは、1.3.0以上であれば、最新バージョンをインストールするという意味。  

```
gem 'coffee-rails', '~> 4.0.0'
```

これの意味するところは、4.0.0よりも大きく、4.1よりも小さい場合にインストール  

つまり、  

```
>= と書くと、bundle installの実行時に必ずアップグレードされる  
~> と書くと、マイナーなアップグレードしかしない  
```

しかし、マイナーなアップグレードでも問題を引き起こす場合があるので、  
できるだけバージョンをピンポイントで指定したほうが良い。  

GemFileでバージョンを指定したら、bundle update , bundle install でアプリケーションの動作環境が整う。  


* bundle updateについて  
Rails gemのバージョンを変更した場合に行う必要がある。  

## 1.2.5 rails server  

```shell
cd rails_app

rails server
```

で、開発マシンでのみブラウズ可能なローカルWebサーバーが起動します。  
JavaScriptランタイムがインストールされていないというエラーが出た場合は、
[github](https://github.com/sstephenson/execjs)
にある、インストール可能なランタイムを確認する。 Node.jsがおすすめ。  

ローカルWebサーバーには、
http://localhost:3000/  
にブラウザでアクセスできます。  

Ctrl-C  
でサーバーをシャットダウンできます。  



