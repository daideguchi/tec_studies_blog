---
title: "【Github】作ったソースコードを保管する"
date: 2022-08-03T08:44:45+09:00
draft: false
categories:
  - "学習アウトプット"
  - "Github"
tags:
  - "プログラミング"
  - "Github"
  - "サイト作成"
  - "デプロイ"
---

Githubにソースコードを保管するまでの最低限の流れを解説します。

<!--more-->
***
## 1.0_Githubとは
***
Githubとは、プログラミングで作成したポートフォリオ（作品：プロダクト）を保管したり公開したりできるサイトです。  
[Github公式](https://github.com/)  

vsコードなどのエディタでブログラムを作成したら、その成果としてここに保管しておきましょう。  

***
## 2.0_Githubでリポジトリを作成する
***
Githubにアクセスして会員登録を済ませましょう。
![Github](../../img/github.png)  
***
会員登録が終わったら、ダッシュボードの左側の緑色のボタンから、新しいリポジトリ（ソースコード保管庫）を作成します。  
![Github](../../img/github_ripo.png)  
***
## 3.0_リポジトリに名前をつける
***
新しいリポジトリが作成されたら、``Repository name``に任意の名前をつけましょう。
***
![Github](../../img/git_new.png)  
***
以下、二つの項目を選択するラジオボタンがありますが、
- リポジトリを公開する場合は、public
- リポジトリを公開しない場合は、private  

どちらかを選びます。  
***
## 4.0_ターミナルでコマンド入力
***
新しいリポジトリが作成されるので、あとは作成したコードをアップするフェーズです。  
以下、SSHをコピーしておきます。  
***
![Github](../../img/git_ripossh.png)  
***
ここまでできたら、ターミナルを起動、もしくはvscodeのターミナルを開き、アップしたいフォルダのディレクトリまで移動しておきます。  
vscodeのターミナルの場合は、自動的にフォルダの階層までデフォルトで移動されています。  
まずは、新しく作成したリポジトリと、アップしたいフォルダが紐付きます。
```
$ git remote add origin 「コピーしたSSH」
```
次に、Githubにアップロードする準備ファイルを作成します。以下コマンドで、対象フォルダ内に隠しファイルの設定データが格納されます。
```
$ git init
```
続いて、全てのデータをセットします。ピリオド「``.``」を打つことで、全てのファイルを対象とすることができます。  
任意のファイルのみアップしたい場合は、ピリオドではなく、任意のファイル名を入力します。
```
$ git add .
```
次に、アップするデータをコミットします。メッセージを任意で設定します。  
なお、メッセージの設定は必須ですので、忘れないようにしましょう。
```
$ git commit -m "「任意のメッセージ」"
```
最後に、push（アップロード）します。ブランチという概念があり、「``main``」か「``master``」になります。  
ここは個別の環境によっても違いますし、別途設定することもできます。  
うまくいかない場合は、もう一つの方で試してみてください。
```
$ git push origin main もしくは git push origin master
```
これで一応、最低限のアップロード作業は完了です。  
先ほどのリポジトリのページを更新すると、アップロードが完了しているはずです。  
他にもさまざまなコードがありますが、それはまた別の機会に紹介したい思います。