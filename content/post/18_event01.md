---
title: "【solidity】eventとemitでブロックチェーン上にトランザクションを記録する"
date: 2022-08-24T12:56:29+09:00
draft: false
categories:
  - "学習アウトプット"
  - "solidity"
tags:
  - "プログラミング"
  - "solidity"
---

`event`と`emit`について学んだ記録
<!--more-->

***

## 1_0 eventについて

***
![solidity_logo](../../img/18_solidity_logo.png)

solidityをコーディングしているとよく出てくる`event`について。

まず、前提として、`contract構文`の中で記述する内容です。

`event`とは簡単にいうと、**「ブロックチェーン上のトランザクションに記録すること」**。

以下の例では、「TokenURIChanged」というeventを記述しています。

- ①address indexed toは、「送り先のアドレス」
- ②uint256 indexed tokenIdは、「数値型のトークンのID（何番目に発行されたトークンか）」
- ③string uriは、「文字列のURI（NFTを識別するコード）」

これらを記録する。と言う認識で大丈夫だと思います。

例えば、`「誰にどのtokenId,URIでNFTをmint（作成）したか」`を記録する際などに使います。

```java Hello.java {.light .line-number .copy}
    event TokenURIChanged(
        address indexed to,
        uint256 indexed tokenId,
        string uri
    );
```

なお、`indexed`は、eventパラメータの修飾子で、このindexedを付与することで、etherscan（トランザクションなどが確認できるツール）などで検索しやすくなるという利点があります。

[etherscanのリンク](https://etherscan.io/)

***

## 2_0 emitについて

***

`emit`とは、`event`を発火させる際に使用します。

つまり、**emitが実行されたタイミングでeventの内容が記録される**という理解で良いです。

以下のコードは、NFTをmint（作成）するコードです。

NFTを作成した後に、`emit`で「TokenURIChanged」と言う`event`を呼び出し、上記①〜③までの情報をブロックチェーン上に記録すると言う意味合いです。

```java Hello.java {.light .line-number .copy}

    function nftMint(address to, string calldata uri) external onlyOwner {
        _tokenIds.increment(); //0を1増やして「1」にする
        uint256 newTokenId = _tokenIds.current(); //さらにここで１増やす
        _mint(to, newTokenId); //NFT作成
        _setTokenURI(newTokenId, uri); //newTokenIdにuriを紐づける

        emit TokenURIChanged(to, newTokenId, uri);
        ^^^^//ここのemitのタイミングで「TokenURIChanged」が発火
    }
```
