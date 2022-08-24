---
title: "【Tailwind】簡単にcssのコーディングができるツール"
date: 2022-08-08T22:54:19+09:00
draft: false
categories:
  - "学習アウトプット"
  - "フロントエンド"
  - "CSS"
tags:
  - "プログラミング"
  - "フロントエンド"
  - "tailwind"
---

巷で話題のCSSツール「``Tailwind``」をNext.jsに導入した記録
<!--more-->

***

## 1.0_Tailwindとは

***
そもそもTailwindとは、``Bootstrap``のように、CSSをコーディングする際に便利なツールです。  
2021年12月にリリースされたv3.0からは使い勝手も大きく向上したようです。  
自分の場合は、プロダクトのフロントエンドは``Next.js``で組んでいるので、``Next.js用``の``Tailwind``を導入しました。  

**[Tailwind公式_next.js](https://tailwindcss.com/docs/guides/nextjs)**  
**[Tailwind公式](https://tailwindcss.jp/)**  

***

## 2.0_早速インストールする

***

インストールは公式に沿って行うのでそんなに難しいものではありません。  
***

### 2.1_まだ作業ファイルを作成していない場合

- これから一から作業を開始する場合は、以下のコマンドからプロジェクトを立ち上げます。  
ここでは、「my-project」という名称のファイルを作成します。

``cd my-project``でディレクトリをプロジェクトファイルに移動できますが、vsコードで作成したファイルを開いたうえで、vsコードのターミナルを起動すると、ディレクトリは既にプロジェクトの階層まで自動で遷移していますので便利です。  
ちなみに``cd``は``Change Directory(階層の変更)``という意味です。

```
npx create-next-app my-project  
↓
cd my-project
```

***

### 2.2_既にプロジェクトがある場合

まず、作業しているフォルダのターミナルを開きます。  
以下のコマンドで、パッケージをまるっとインストールします。

```
npm install -D tailwindcss postcss autoprefixer
```

次に、設定ファイルを作成します。
```
npx tailwindcss init -p
```
***

## 3.0_インストール後の設定

***
``tailwind.config.js``を開きます。 
contentの配列部分がデフォルトだと空欄になっていると思うので、以下のように編集します。  
動作を軽くさせるために行います。（デプロイ時に、特定のファイルだけCSSを生成させるため）

```java Hello.java {.light .line-number .copy}
/** @type {import('tailwindcss').Config} */ 
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",      //ここを挿入
    "./components/**/*.{js,ts,jsx,tsx}",  //ここを挿入
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```  

続いて、styleフォルダ内の``globals.css``を編集します。  
中身は以下の３行のみで大丈夫です。

```java Hello.java {.light .line-number .copy}
@tailwind base;
@tailwind components;
@tailwind utilities;
```

続いて、不要なcssファイルは削除しておきましょう。  
Next.jsの場合、``homemodule.css``と``pages/api``は必要ないので削除します。

これで一応、最低限の設定は完了しました。  
**注意点ですが、HTMLタグでのclass指定は``className=""``で指定するようにしましょう。**  

***

## 4.0_表示させるページの設定

***
Next.jsのフレームワークを使用している場合は、表示させるページの設定は、基本的には``index.js``をいじります。  
今回は一番最初の確認画面のみ、紹介しておきます。  
例のごとく、``Hello world``と表示させてみましょうか。  
``index.js``を開きます。

```java Hello.java {.light .line-number .copy}
export default function Home() {
  return (
    <h1 className="text-3xl font-bold underline"> //ここのclassNameを色々変えてみましょう。
      Hello world!
    </h1>
  )
}
```  

***

## 5.0_ビルドする

***
設定を反映させて、以下のコマンドでサーバーを立ち上げましょう。
```
npm run dev
```
ターミナル上にローカルのURLが表示されるはずなので、アクセスします。  
``Hello world``が表示されれば成功です。

***

## 6.0_チートシートの紹介

***

classNameにTailwind独自のコードを指定すれば簡単にレイアウトを編集できます。  

classに指定するデザインを選ぶのに、チートシートが役に立ちます。  
**[チートシート](https://nerdcave.com/tailwind-cheat-sheet)**  
***
それでは、次回はNext.jsにインストールしたTailwindを、より詳細に設定していきます。
