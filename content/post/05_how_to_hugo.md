---
title: "【Hugo】静的サイトジェネレータで無料ブログサイトを作る"
date: 2022-07-31T22:51:11+09:00
draft: false
categories:
  - "学習アウトプット"
  - "Hugo"
tags:
  - "プログラミング"
  - "Hugo"
  - "サイト作成"
---

【わずか５分で無料爆速ブログを作る】hugoで静的サイトジェネレータを開設した記録  
プログラミングを学びながらブログを運営できる

<!--more-->
***
    
<br>

### 1.0_静的サイトジェネレータとは  
***

ブログといえば「アメーバブログ」や「はてなブログ」などのサービスを利用するか、  
有料のサーバーを契約して、「WordPress」で一からブログを作るか。

というイメージが強いと思います。

今回は、「``静的サイトジェネレータ（SSG)``」で無料の爆速ブログを簡単に構築する方法を紹介します。  

概要については、こちらの記事が分かりやすいです。  
[【2021注目】フロントエンド開発「静的サイトジェネレータ](https://fastcoding.jp/blog/all/info/ssg/)
  
上記の記事でも紹介されているとおり、CLI(ターミナルなどのコマンド)や、Githubなど、  
多少プログラミング関連の知識が必要になります。  
また、動的なサイト（例えばPHPを使ってDBとやり取りするとか）は構築できないのもデメリットにはなりますが、  
マークダウン記法を学べることや、Gitの知識が深まるなどの利点もあります。  
なにより、今注目されているフロントエンドの技術というのも魅力の一つだと思います。  
  
***
### 2.0_今回は簡単なHugoを選択
***
上記リンク先にも説明があるように、静的サイトジェネレータにはいくつか種類があります。  

|  利用言語 |  ジェネレータ |
| ---------| ----------- |
|  Go      |  Hugo       |
|  React|  Next.js   |
|  Vue  |  Next.js   |
|  Ruby  |  Jekyll   |

それぞれに特徴はありますが、私は比較的学習コストが低く、直感的に操作のできる「Hugo」を選択しました。

***
### 3.0_サイト構築の手順
***
まずは公式サイトに沿って、簡単なサイトを作ってみましょう。  
[公式サイト->Hugo](https://gohugo.io/)  
  
以下のコマンドをターミナルで実行します。 


  
#### 1.hugoのパッケージをインストールする
```
brew install hugo
  or
port install hugo
```

#### 2.サイトを構築する  
以下コマンドで、現在のディレクトリにファイルが生成されます。  
「quickstart」となっているところはファイルの名称なので、任意で大丈夫です。
```
hugo new site quickstart
```
ファイルが作成されます。  
vscodeのエディタを使っている場合、この時点でvscode内のターミナルを使用すると分かりやすいです。  
その場合は、自動的にフォルダ内の階層に移動してくれるので、以下の``$ cd quickstart``コマンドは不要です。  

#### 3.テーマを追加する
用意されているテーマは無数にあります。有志のクリエイター達がたくさん作成してくれています。  
[Hugoのテーマ集](https://jamstackthemes.dev/ssg/hugo/)  
今回は、公式のデフォルトでもある「Ananke テーマ」を使用します。
```
cd quickstart  
↓  
git init  
↓  
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```
#### 4.コンテンツを追加する
とりあえず、サイトの最低限の体裁は整ったので、記事を一つ追加してみましょう。  
なお、手動で```content/post```内に、フォルダを作成しても大丈夫です。
```
hugo new post/my-first-post.md
```
上記を実行すると、```content/post```に``my-first-post.md``という名前のマークダウンのファイルが作成されています。  
もちろんファイルの名前も自分の好みでオッケーです。  

#### 5.コンテンツを確認する
作成されたファイル``my-first-post.md``を確認すると、以下のような内容になっています。
```java Hello.java {.light .line-number .copy}
---
title: "My First Post"
date: 2019-03-26T08:47:11+01:00
draft: true
---
```
上記のような記述がでデフォルトで表示されます。（設定で変更可能）  
- title: 記事のタイトル
- date: 記事を作成したタイムスタンプ
- draft: trueは下書き、falseは公開
ということで、まずは``draft を falseに変更``しておきましょう。

#### 6.Hugoサーバーを立ち上げる
では、早速、サーバーを起動します。
ちなみに、``-D``を記述することで、下書きの状態も表示してくれるので覚えておきましょう。

```
hugo server -D

                   | EN
+------------------+----+
  Pages            | 10
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  3
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 11 ms
Watching for changes in /Users/bep/quickstart/{content,data,layouts,static,themes}
Watching for config changes in /Users/bep/quickstart/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

下から二行目``Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)``の箇所のURLにアクセスすることで、ローカルホストのサーバーにアクセスすることができます。  
これで一応、サイトが立ち上がります。  
サーバーを閉じる際は、ターミナルで``CtrlキーとCを同時に押す``ことで終了できます。

#### 7.テーマをカスタマイズする
一応、テーマのカスタマイズ方法も触れておきます。  
ここはテーマによって内容が異なるところですが、基本的な情報は共通しており、下記の内容を編集します。
``config.toml``を開きます。
```java Hello.java {.light .line-number .copy}
baseURL = "https://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```
- baseURL:Githubなどにデプロイした時のURLを設定します。
- languageCode: 日本語に設定しておきましょう。``"ja-jp"``
- title: サイトのメインタイトルです。
- theme: 選択したテーマを記述しますが、テーマを適用するためには、別途テーマのインストールが必要になります。

#### 8.ビルドする
最後に、記事の編集を行なった場合や、基本的な情報を変更した場合など、何らかのアクションを行なった場合、  
以下のコマンドを実行します。
```
hugo
```
このコマンド一つで自動的に色々と微調整してくれます。  
***
さて、ここまでで一応サイトを立ち上げることができました。  
次回は、Github Pagesにサイトをデプロイ（公開）する手順を紹介していきます。