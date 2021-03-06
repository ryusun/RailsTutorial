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

## 1.2.6 Model-View-Controller(MVC)  
app/ディレクトリ配下にある、「model」、「views」、「controllers」という3つのサブディレクトリがある  

下記は、大切なことだと思うので、引用して貼り付けた。  


>MVCでは、ドメインロジック (ビジネスロジックともいいます) と、グラフィカルユーザーインターフェイス (GUI) と密に関連する入力/表示ロジックを分離します。
>
>Railsアプリと通信する際、ブラウザは一般的にWebサーバーにrequest (リクエスト) を送信し、これはリクエストを処理する役割を担っているRailsのcontroller (コントローラ) に渡されます。  
>コントローラは、場合によってはすぐにview (ビュー) を生成してHTMLをブラウザに送り返します。  
>動的なサイトでは、一般にコントローラは (ユーザーなどの) サイトの要素を表しており、データベースとの通信を担当しているRubyのオブジェクトであるmodel (モデル) と対話します。  
>モデルを呼び出した後、コントローラは、ビューをレンダリングし、完成したWebページをHTMLとしてブラウザに返します。  

# 1.3 Gitによるバージョン管理  
gitインストール後にやるべきこと  

* git config --global user.name "name"  
* git config --global your.email@example.com  

* git config --global alias.co checkout  
checkoutが長いので、coというエイリアスにする設定  

* git config --global core.editor "subl -w"  
comment用のエディタにサブライムテキストを指定する方法  

* .gitignoreファイルの見直し  
デフォルトである程度設定されているが、見直しをしておく  
下記を追加する.  

>doc/
>*.swp
>*~
>.project
>.DS_Store
>.idea
>.secret

* git checkout -b "branch-name"  
ブランチ作れる  

* git branch  
ブランチ見れる -a はリモートのブランチも見れる  

* git mv A B  
AをBに変更(rename)  

* git add (ファイル名やパス)  
追加されたファイルをgitの管理下に追加  
これをやらないとバージョン管理できないよ。  

* コミットメッセージは現在形で.  
これは知らなかった。  
基本的に現在形で書いていたけど、意識して書くようにする。  

>コミットメッセージは現在形で書くようにしましょう。
>Gitのモデルは、(単一のパッチではなく) 一連のパッチとしてコミットされます。
>そのため、コミットメッセージを書くときには、そのコミットが「何をしたのか」と履歴スタイルで書くよりも「何をする」ためのものなのかを書く方が、後から見返したときにわかりやすくなります。
>さらに、現在形で書いておけば、Gitコマンド自身によって生成されるコミットメッセージとも時制が整合します。
>詳細についてはGitHubに投稿された「最新のコミット方法 (英語)」を参照してください。

* git commit -am "message"  
-aはすべての変更を意味するので取り扱いに注意  

* マージについて  

```
git checkout master  
```

でマージ先に移動します。ここではmasterにマージ  

```
git merger "branch-name"  
```

でブランチをマージできる  

* ブランチの削除  
不要になったブランチは下記のコマンドで削除できます  

```
git branch -d "ブランチ名"

git branch -D "ブランチ名"
```
-dではマージ済みのブランチを削除可能  
-Dではマージしていないブランチも削除可能(取り扱い注意)  

# 1.4 デプロイする  

* herokuを使う  
herokuの無料プランがデフォルトで使用するDBがPostgreSQLなので、production用のgemとして、  
pg gemをインストールする必要がある。  

* 疑問  
ProductionとDevelopmentの環境、ここではDBが違うことによる不都合とかはないのか？  

* 疑問はこの先解明するとして、続ける。  

```Gemfile
group :production do
    gem 'pg' , '0.15.1'
    gem 'rails_12factor', '0.0.2'
end
```

* production以外を適用するコマンド  

```bundle
bundle install --without production
```

この状態でコミットしておく  

```git
git commit -a -m "Update gemfile.lock for heroku"
```

* herokuにログインしよう  
herokuのページで会員登録する。  
あとは、ツールをインストール  
install後は /usr/local/heroku
にPATHが通っていれば下記のコマンドを実行してログインできる  


```
heroku loguin
```

* gitにpushするだけでデプロイが終わる素晴らしいツール  

```heroku
cd first_app
heroku create
```

これで、デプロイ用の環境ができた。  

git push するだけだが、remoteの設定は必要  

```
git remote add heroku git@heroku.com:gitリポジトリ名
```

で設定したら、

```
git push heroku master
```

で、デプロイ完了という驚異的なスピード  

```
heroku open
```

でサイトが閲覧できる。  
rails4はまだ対応していないようで、エラーですが。  

さて、サンプルアプリケーションの名前を変更してみる  

```
heroku rename <name*
```

これで終わり。  
tutorialofrails  
に変更してみた  


これで環境作成は終わり。時間取れないと長いなー  

次がやっとrailsですｗ  

# 第2章 デモアプリケーション  

* scaffoldジェネレータを使ってdemoアプリを作る  
Railsの概要をつかむのに便利なのでまずは使ってみよう  

* rails new demo_app  
でデモアプリを生成。  
Gemfileはfirst_apnと同じ  

アプロの作成の前に、構造を表すためのデータモデルの作成を行う。  
デモアプリはマイクロブログらしい  

## 2.1.1ユーザーのモデル設計  

* ユーザーモデル  
ユーザーテーブルですね  

|id|name|email|
|:--|:--|:--|
|integer|string|string|


* マイクロポストモデル  
ポストされたデータのモデル  

|id|content|user_id|
|:--|:--|:--|
|integer|string|integer|

という形式で、ポストとユーザーをuser_idで紐付けするシンプルな構造  

## 2.2 Usersリソース  
ユーザー用のデータモデルを、そのモデルを表示するためのWebインターフェイスに従って実装する  

* scaffoldジェネレータで生成  
railsのscaffoldは、rails generateスクリプトにscaffoldコマンドを渡して生成する。  
scaffoldのコマンド引数には、リソース名を単数形にしたもの(この場合はUser)を使用し、  
必要に応じて、データモデルの属性をオプションとしてパラメータに追加する。  

```
rails generate scaffold User name:string email:string
```

**[重要]idパラメータはRailsによって、自動的に主キーとしてデータベースに追加されるので不要**  

ジェネレートしたリソースは次のコマンドでデータベースにマイグレートできます  

```
bundle exec rake db:migrate
```

rails server  
コマンドでローカルサーバーを起動する  
ちなみに、  
rails s  
で起動する  

* rakeについて  
rakeはRuby版のmakeコマンド  
Makefileをrubyで記述できるようにしている。  
rake db:migrateでDBに簡単にmigrateできるのも利点  
rake -T dbオプションをつけて実行すると様々なデーベースタスクが用意されているのがわかる  

```
bundle exec rake -T db
```

rakeで実行可能なタスクをすべて表示するには以下を実行します  

```
bundle exec rake -T
```

## 2.2.1 ユーザーページを表示する  
http://localhost:3000  
にアクセスすると、デフォルトのRailsページが見える。  
実はUsersリソースを作成した時に、これ以外の様々な「ユーザーを扱うためのページ」がすでに作成されている  
/usersを表示すると、すべてのユーザーの一番が表示される  
/users/newを表示すると、新規ユーザー作成ページが表示される。  

* ユーザーに関連するページについて  


|URL|アクション|用途|
|:--:|:--:|:--:|
|/users|index|すべてのユーザーを一覧するページ|
|/users/1|show|id=1のユーザーを表示するページ|
|/users/new|new|新規ユーザーを作成するページ|
|/users/1/edit|edit|id=1のユーザーを編集するページ|

※ scaffoldすげー便利だな… でもこのページはいらないってなったらどうすんだ？  
単純に削除ですかね？  

上記のページを操作して、ユーザーの追加、変更、削除をやってみた  
削除はJavascriptで行われるようだ。  

## 2.2.2 MVCの挙動  












