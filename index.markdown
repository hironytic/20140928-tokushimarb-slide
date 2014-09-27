# tokushima.rb 2 slide

### Author

* か (ka)
* [kaosfield](http://www.kaosfield.net)


## はじめに

このスライド自体のリポジトリは [kaosf/20140928-tokushimarb-slide](https://github.com/kaosf/20140928-tokushimarb-slide) にあります

間違いを発見したら Issue あるいは PullRequest を下さい


## 前回までのあらすじ

* 徹底的なオブジェクト指向
* 無名関数
* 高階関数


## 今回の話

Ruby超入門をやろう

(※スライドになるようなネタ他に無かったし…)


## Rubyの始め方


## 手順

1. Linuxのインストールディスクを取り出します
1. インストーラの指示に従います
1. Windowsを消します
1. `apt-get` や `yum` で超簡単にインストール出来ます


ちょっと古いバージョンになりますが  
パッケージ化されていてビルド済みのものを  
インストールするので楽ちんに  
セットアップが出来ます


## 最新版を使う

Qiitaとか探せば rbenv というツールを使ってインストールをする解説記事がきっと山のように出てきますのでそれを参考にしましょう

一応今から軽く解説します


## 私の場合

Ubuntu 14.04 amd64 で Ruby 2.1.3 を使うには

```sh
sudo apt-get install git curl build-essential \
  zlib1g-dev libssl-dev libreadline6-dev \
  libsqlite3-dev postgresql-server-dev-9.3 libxslt1-dev libxml2-dev
git clone https://github.com/sstephenson/rbenv.git $HOME/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> $HOME/.zshenv
echo 'eval "$(rbenv init -)"' >> $HOME/.zshenv
exec $SHELL -l
mkdir -p $HOME/.rbenv/plugins
git clone https://github.com/sstephenson/ruby-build.git \
  $HOME/.rbenv/plugins/ruby-build
git clone https://github.com/ianheggie/rbenv-binstubs.git \
  $HOME/.rbenv/plugins/rbenv-binstubs
rbenv install 2.1.3
rbenv global 2.1.3
rbenv rehash
gem install bundler --no-ri --no-rdoc
rbenv rehash
```


## 参考

* [ubuntu-setup/setup.sh at c02def8f01e81b9f1113cb312fe33c90e28e9bd6 · kaosf/ubuntu-setup](https://github.com/kaosf/ubuntu-setup/blob/c02def8f01e81b9f1113cb312fe33c90e28e9bd6/setup.sh)
* [ubuntu-setup/ruby-setup.sh at c02def8f01e81b9f1113cb312fe33c90e28e9bd6 · kaosf/ubuntu-setup](https://github.com/kaosf/ubuntu-setup/blob/c02def8f01e81b9f1113cb312fe33c90e28e9bd6/ruby-setup.sh)
* [sstephenson/rbenv](https://github.com/sstephenson/rbenv)

あんなコマンド覚えてるわけもなくメモとってそこから開発用マシンの初期化時にコンソールにコピペしてます


## 補足

後でRailsのインストールやってみたい人

```sh
sudo apt-get install sqlite3
```

もやっておくと良いです


## やっぱりWindowsが良い？

Windowsを消しましょうは半分冗談ですが  
MacかLinux(出来ればメジャーなUbuntuが良い)を使うことを割と心の底からオススメします

多分MySQLだのMongoDBだのRMagickだの  
ミドルウェアとの連携をする必要が出てきます

早いこと慣れておいた方が良いです


## Ruby on Windows セットアップ

私はここ3年くらいWindowsでRubyを触ってませんので誰か詳しい人教えて下さい


## Macの人

`Homebrew` を是非インストールして下さい

[Homebrew — The missing package manager for OS X](http://brew.sh/)


## Homebrew is 便利

```sh
brew install rbenv
brew install ruby-build
```

この後

```sh
rbenv install 2.1.3
# 続きは一緒
```

すれば(多分)良いです (※今確かめてない)


## Gem を使おう

Ruby では各種ライブラリ等が  
"Gem" と呼ばれる単位でパッケージ化されてます

Rails なんかも "rails" という名前の Gem  
をインストールすることで使い始めます


## Gem をインストールする

```sh
gem install rails
```

これでいいっちゃいいんですが

```sh
gem install rails --no-ri --no-rdoc
```

このオプション付けてやると早く終わります

ドキュメントの生成をスキップさせます


## 絶対使おう Bundler

```sh
gem install bundler --no-ri --no-rdoc
```

これは絶対入れておかないとダメです

「入れた方がいい」レベルじゃなく  
「無いとヤバい」くらい

gem のインストールの面倒を見てくれる gem です


## rbenv の人は

この状況なら皆 rbenv を使ってるはず

```sh
rbenv rehash
```

これを忘れず実行しておきましょう

複数バージョンを共存させるための  
シンボリックリンクのあれこれを  
いい感じに設定し終えてくれます


## そもそも rbenv とは

RuBy ENVironment って意味だと思う

Ruby を複数のバージョン同時にインストールして  
それの切り替えなんかを面倒見てくれるものです


## なんでそんなこと

Ruby はバージョンアップのサイクルが恐ろしく速いです

新しいバージョンをどんどん試して行きたいというか
試していかないと気付いた時には凄く前のバージョンで留まってる
なんてことにごく普通になりがちです

しかし古いバージョンで動いてるのを  
動かなくさせてしまうかもしれない


## rbenv + ruby-build 便利

rvm とか今は使ってないけどそういうのもあります

色んなバージョンの Ruby (jruby も mruby もある)  
をインストールして使い分けられます

インストール可能な一覧は以下のコマンドで

```sh
rbenv install -l
```


## Ruby プログラムの実行

```ruby
puts "Hello tokushima.rb"
```

こう書いたファイルをファイル名 `a.rb`  
とでもして用意します

```sh
ruby a.rb
#=> Hello tokushima.rb
```

実行出来ました


## ファイル分割

`a.rb` と `b.rb` を同じディレクトリに置いて

```
require './b'
puts(f "shikoku")
```

```
def f(x)
  "Hello #{x}.rb"
end
```

としておきます

```sh
ruby a.rb
#=> Hello shikoku.rb
```

出来ました


## IRB

Ruby のデフォルトの REPL である  
`irb` を触って終わりにしましょう

```sh
$ irb
irb(main):001:0> _
```

ここに Ruby のコードを打っていけば  
結果が表示されます

REPL は Read Eval Print Loop の略


## 最後に

言語仕様を知らない言語に初挑戦するときは  
トライ＆エラーを繰り返すのが一番です

とりあえず色々試せる環境は出来ました

今日これで遊べるといいですね


## Railsインストール出来た？

```sh
rails new my_first_app
```

これでRailsプロジェクトのひな形が作れるよ！


おわり
