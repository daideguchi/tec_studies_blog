---
title: "【Django】Pythonフレームワークの環境構築とインストール"
date: 2022-08-07T22:06:47+09:00
draft: false
categories:
  - "学習アウトプット"
  - "バックエンド"
  - "Python"
tags:
  - "プログラミング"
  - "Python"
  - "Django"
---

今日は、Pythonのフレームワークである``Django``の環境構築の記録を残します。
<!--more-->
***
### 1.0_Djangoとは
***

Djangoとは、Pythonのフレームワークです。  
Djangoを使えば、コンテンツ管理システムやWikiからソーシャルネットワーク、ニュースサイトなど、高品質なWebアプリケーションを簡単に、少ないコードで作成できます。  
ちなみに呼び方は「ジャンゴ」です。
今回開発するプロダクトは、フロントを``Next.js``で、バックを``Django``で構成する予定です。  
最終的には、スマートコントラクトを実装します。

[Django公式](https://pypi.org/search/?q=django)

***
### 2.0_インストール手順
***

まずは、作業ファイルを作成します。  
ここでは、ファイル作成後、ターミナルでそファイルの階層を表示されているところから解説します。  

***
#### 2.1_Pythonをインストールし、仮想環境を構築する
***
まずはPython3系の環境をインストールします。  
```
python3 -m venv myvenv
```  

続いて、以下のコマンドを実行します。  
このコマンドを実行することで、Pythonの仮想環境の構築を行います。
```
source myvenv/bin/activate
```
ターミナルにの先頭に``(myvenv)``と表示されれば成功です。  

***
#### 2.2_requirements.txtファイルの作成
***
次に、Djangoと、使用するパッケージをまとめてインストールするために、``requirements.txt``ファイルを作成します。  
```java Hello.java {.light .line-number .copy}
├── myvenv
├─db.sqlite3
├─repuirements.txt //新規ファイル作成

``` 
作成した``requirements.txt``には、インストールしたいパッケージやフレームワークを記述します。 
ここではバージョンの指定もできますので、インストールしたいバージョンを指定しましょう。  
```java Hello.java {.light .line-number .copy}
Django~=4.0
django-cors-headers~=3.4.0
djangorestframework~=3.11.1
pillow==9.2.0
```  

記述が完了したら、一括でインストールするために、ターミナルで以下を実行します。
```
pip3 install -r requirements.txt  
```

***
#### 2.3_プロジェクトをスタートさせる
***
インストールが完了したらプロジェクトをスタートさせます。
以下、最後のドットは「ディレクトリ直下」にファイルを作成させると言う意味です。
```
django-admin startproject 「任意のプロジェクト名」 .
```  
プロジェクト名のフォルダが作成されるので、その中の``setting.py``を開きます。  
今のうちに、言語とタイムゾーンを日本に設定しておきます。
```java Hello.java {.light .line-number .copy}

~~~~~~

LANGUAGE_CODE = 'ja'

TIME_ZONE = 'Asia/Tokyo'

~~~~~~
```  

#### 2.4_データベースのセットアップ
以下のコマンドを実行しましょう。
```
python3 manage.py migrate 
```
ここまで終わったら、ウェブサーバーを起動します。
```
python3 manage.py runserver
```
実行するとターミナルでは以下のような表示になります。
```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
August 07, 2022 - 22:39:47
Django version 4.1, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
その中に、ローカルのURLが表示されるのでアクセスします。  
私の場合は、``http://127.0.0.1:8000/``と表示されました。  

以下の画面が出力されればDjangoの設定は完了です。 
*** 
![Django](../../img/12_django.png)
***
サーバーを閉じる際は、ターミナルで``control + C``を押下します。
お疲れ様でした。