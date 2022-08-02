---
title: "【Hugo】構築したサイトの記事に画像を挿入する"
date: 2022-08-02T20:50:32+09:00
draft: false
categories:
  - "学習アウトプット"
  - "Hugo"
  - "技術"
tags:
  - "プログラミング"
  - "Hugo"
  - "サイト作成"
  - "画像"
---

Hugoで構築したサイトに記事を書いていた時、画像がどうしても表示させられない沼にハマったので、解決法を紹介します。  

<!--more-->

***
## 1.0_マークダウン記法で画像を挿入する
***
そもそも、マークダウン（.mdの拡張子）で画像を挿入したい場合、以下のようなコードを記述します。  
先頭に``!``を記述し、``![画像の名称：任意]（画像のURLもしくはパスを指定）``

```java Hello.java {.light .line-number .copy}
![](relative/path/image.png)
![](/root/path/image.png)
![](http://www.example.com/image.png)
![](http://www.example.com/image.png "Hover Text")
![Alt Text](http://www.example.com/image.png "hover text")
```
ところが、これらの形式で記述しても、うまく画像が表示されません。。

***
## 2.0_"static"フォルダに画像を挿入する。
***
テーマにもよると思いますが、私の場合は、「mainroad」のテーマを使っています。  
[mainroad公式のGithub](https://github.com/Vimux/Mainroad)  
インストールしたテーマのファイルの中に、``static``というフォルダがあります。  
この中に``画像ファイル``を保存することで画像を表示することができます。  

***
#### -> 手順1.staticにimgフォルダを作る  
自分の場合は、``static``フォルダに``img``フォルダを作成して、その中に画像``test.jpg``を挿入しました。  

***
#### -> 手順2.ディレクトリの確認  
```java Hello.java {.light .line-number .copy}
── archetypes
├── config.toml
├── content
│   └── post
│       └── hogehoge.md //ここを編集中
├── data
├── docs
├── img
├── layouts
├── public
├── readme.md
├── resources
├── static
│   └── img
│       └── test.jpg //ここに画像のファイルがある
└── themes
    └── mainroad

```  

***
#### -> 手順3.記事に画像を埋め込むコードを記述  

例えば、現在編集しているファイルが``hogehoge.md``の場合は、２階層戻って、``static``にアクセスするのですが、パスの指定に``static``の記述は不要です。  
そのため、以下のような記述になります。
```java Hello.java {.light .line-number .copy}
![海のフリー画像](../../test.jpg)
```
![海のフリー画像](../../img/test.jpg)  

無事、画像を表示することができました。
