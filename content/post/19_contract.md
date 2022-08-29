---
title: "【solidity】最初の第一歩。contractを生成する"
date: 2022-08-25T22:12:20+09:00
draft: false
categories:
  - "学習アウトプット"
  - "solidity"
tags:
  - "プログラミング"
  - "solidity"
---

`solidity`でスマートコントラクトを実装するための第一歩目`contract`の記録

<!--more-->

***

## 1.0 スマートコントラクトとは

***

![solidity_logo](../../img/18_solidity_logo.png)

solidityは、そもそもスマートコントラクトを実装させるための言語です。

おさらいで、スマートコントラクトとは、スマートフォンなどの`スマート○○`といった類の一つで、直訳すると、「賢い契約」です。

コンピュータが自動的に契約をしてくれて、しかもブロックチェーン上に記録されることから、改ざんなどができない非常に透明性の高いものになります。

例えるなら、自動販売機で、誰がいつどの飲み物を購入したか、世界中の誰でも正しい情報を確認することができると言うものです。

**[【solidity】そもそもsolidityとは](10_solidity01.md)**

***

## 2.0 まずはcontract(契約)の雛形を作る

***

```java Hello.java {.light .line-number .copy}
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;
```
(参考)[【solidity】REMIX IDEでコーディング前の準備](11_solidity02.md)

まずは、先頭に、

- ライセンスの情報
- solidityのバージョンの指定

が終わったら、早速`contract（契約）`を作成していきます。  
以下、[公式ドキュメント](https://docs.soliditylang.org/en/v0.8.16/contracts.html)からの転用ですが、contract内では、状態変数や関数など、さまざまな情報を定義していきます。

簡単に言うと、**箱を作って、その中に契約の中身を入れていく**といった感じです。

一言に契約と言っても、多岐にわたる機能を持たせることができて、例えば、

- NFTを作ったり(mint)
- トークンを作ったり
- 作ったトークンを売買したり

色々と応用が効きそうです。

ここでは公式ドキュメントのサンプルコーディングに簡単な解説をコメントアウトで載せておきます。

```java Hello.java {.light .line-number .copy}

//箱{}  contract:契約。 契約の名前は「OwnedToken」
contract OwnedToken {
    TokenCreator creator;//「TokenCreator」と言うインスタンスを作り、そのインスタンスを呼び出すための変数が「creator」。その変数「creator」の属性にオーナーのアドレスと名前を下で定義。
    address owner;//ownerをaddress型で定義（オーナーのアドレス）
    bytes32 name;//nameを32文字までのbytes32で定義（オーナーの名前）


//constructor:変数を定義 「一度だけ実行されるやつ」
    constructor(bytes32 name_) { //引数はname_（実際のオーナーの名前を受け取る）
        owner = msg.sender; //msg.senderは送り主（操作する側）のアドレス。それをowner変数に代入

        creator = TokenCreator(msg.sender);//送り主アドレスを引数に入れ、定義されたインスタンスを呼び出し
        name = name_; //受け取った実際の名前を、呼び出されたインスタンス内のnameに格納
    }

//function:関数を定義 「いつでも呼び出せる」
    function changeName(bytes32 newName) public {
        if (msg.sender == address(creator))
            name = newName; //新しいオーナがアクセスしたら、名前を更新
    }

    function transfer(address newOwner) public {
        if (msg.sender != owner) return;
        if (creator.isTokenTransferOK(owner, newOwner))
            owner = newOwner; //新しいオーナがアクセスしたら、アドレスを更新
    }
}
```

今後、どんどん掘り下げていきたいと思います。
