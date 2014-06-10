RailsTutorial
=============

[rails tutorial](http://railstutorial.jp)  

* Start 2014-06-10 

* Rubyのインストール  
rbenvを使って2.0をインストールした  
rbenvは導入済みだった  

* gemのupdate  
```
gem update --system (version)
```
(version)にバージョンを指定することで、gemの指定したバージョンを取得することが可能。  

* .gemrcにgemの設定を記述する  
```.gemrc
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
```
これでriとrdocのインストールを省くことができる。  
今まで、gem install xx --no-rdoc --no-ri  
と書いていたのが楽になります。  

* rails install  
```rails
gem install rails --version 4.0.5
```
railsの4.0.5のインストール  

```rails
rails -v
```
で、railsのバージョンを確認できる。  

* 最初のアプリケーション  


