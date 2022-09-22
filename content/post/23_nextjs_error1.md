---
title: "【next.js】HTMLの記法の間違いで出現するエラーを解消した話"
date: 2022-09-22T18:35:17+09:00
draft: false
categories:
  - "学習アウトプット"
  - "フロントエンド"
  - "next.js"
tags:
  - "プログラミング"
  - "フロントエンド"
  - "next.js"
---

タイポが原因で出現したエラー`Hydration failed because the initial UI does not match what was rendered on the server.`を解消した記録
<!--more-->

***

## 1.0_エラーの出現

***

next.jsでwebページを作っていたところ、突然次のようなエラーが出現しました。  
`Hydration failed because the initial UI does not match what was rendered on the server.`

![solidity_logo](../../img/23_nextjs.png)

***
これは、直訳すると、**「初期UIがサーバーでレンダリングされたものと一致しないため、Hydrationに失敗しました。」**
と言っています。

この`Hydration`とは簡潔に言うと、`コーディングしたjavascriptをもとに、HTMLを自動生成してくれる機能（インタラクティブな状態にすること⇨操作可能の状態にすること）`です。

[nextjs公式ドキュメント「Hydration」の説明箇所](https://nextjs.org/docs/basic-features/pages#pre-rendering)

***

## 2.0_なぜこのエラーが出現したか

***

結論、私の場合は、`HTMLの記述がおかしかった`という内容になります。

まず、next.jsでは「レンダリング」と言い、記述したjsファイルやjsxファイルを自動で定期的にHTMLを作成＆更新をしてくれています。

ここで更新されたHTMLがページとして表示される訳です。

自動的に作成されている「.next」というフォルダの中で、レンダリングされたページのHTMLを確認することができます。

ということで、記述していたjsファイル内のHTMLが、おかしい場合はレンダリングがうまくできずにこのようなエラーが発生したのではないかと思います。

エラーは具体的に下記の流れです。

```

①作業の過程でHTMLの記法ミス
②レンダリングがうまくいかない(変な感じで変換)
③うまく書けていた時にレンダリングされたUIと一致しない。
④エラー発生

```

簡潔ですが、例えば、以下のような誤った記述ケースだと、同様のエラーが発生するかと思います。

```java Hello.java {.light .line-number .copy}

// <p>の中に<div>が入るのはおかしい！
<p>
  <div>
  "Hello world"
  </div>
<p>

```

***

## 3.0_結論

***

この「
`Hydration failed because the initial UI does not match what was rendered on the server.`
」
エラーが発生したら、まずは発生したページファイル内（jsやtsなど）の記述の中で、`HTMLにおかしな点はないか。`というのを確認してみてください。
