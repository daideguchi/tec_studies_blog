---
title: "【solidity】4つのvisibilityと呼ばれるアクセス修飾子（権限）について"
date: 2022-08-29T20:27:57+09:00
draft: false
categories:
  - "学習アウトプット"
  - "solidity"
tags:
  - "プログラミング"
  - "solidity"
---

`contract`にアクセスする権限を設定する`Visibility`を学習した記録

<!--more-->

---

## 1.0 ここで言う「アクセス権限」とは

---

![solidity_logo](../../img/18_solidity_logo.png)

solidity で記述された contract(契約プログラム)では、アクセスの権限を設定することができます。

例えば、自動販売機で、今からまさに「麦茶」を買おうとしている人がいるとして、他の人が遠隔操作で、「コーヒー」のボタンを押しては困りますよね。

自動販売機でボタンを押せるのは、実際にお金を入れた人です。solidity ではこの人をオーナーと呼ぶとわかりやすいかもしれません。

と言うことで、この自動販売機にお金を入れて、ボタンを押した際に走るプログラム一つにも、`アクセスする権限`は`オーナーのみ`と設定するのが妥当かと思います。

---

## 2.0 Visibility とは

---

この、アクセス権の設定を「Visibility」の設定と言います。

**[solidity 公式：Visibility](https://solidity-by-example.org/visibility/)**

具体的には、それぞれの処理ごとに`4つ`の権限を付与することが可能です。

以下、公式から転用します。

```
① public - any contract and account can call
② private - only inside the contract that defines the function
③ internal- only inside contract that inherits an internal function
④ external - only other contracts and accounts can call
```

さて、一つずつ簡単に解説します。
ちなみに、継承とは、コントラクト（作った契約）を呼び出して、転用するようなイメージです。

- `public` : 誰でもアクセス可能。デフォルトはこれ
- `private` : オーナーのみがアクセス可能。ただし宣言したらそのコントラクト内のみ使用可能 ⇨ 継承先ではアクセスできない
- `internal` : オーナーのみ。継承したコントラクト先からはアクセス可能。継承コントラクトのデフォルトはこれ
- `external` : 外部からのみアクセス可能

図解の方がわかりやすいかもしれません。
|  修飾子 | コントラクト外部 | コントラクト内部 |継承先|
| ---------| ----------- | ----------- |-----------|
| `public` |  ○|○|○|
| `private`|  ×|○|×|
| `internal` | ×|○|○|
|`external`|○|×|×|

---

特に、トークンのやり取りなどが発生するコントラクトでは、この辺りをしっかりと設計・整理しておかないと、大変なことになると思います。

誰かよくわからない人にアクセスされて資産を持っていかれた、なんてことにならないようにしなければいけませんね。

---

## 2.0 どのように定義するか

---

では、具体的な使い方を簡単に解説します。

定義の仕方は、各 function などに付けていきます。

以下、公式のソースコードにコメントアウトで説明書きを載せます。

```java Hello.java {.light .line-number .copy}

/// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

contract Base {

//②
    function privateFunc() private pure returns (string memory) {
                       // ^^^^^^^^^ここに記述。このfunctionは外部からアクセスできない
        return "private function called";
    }



//①
    function testPrivateFunc() public pure returns
                          // ^^^^^^^^^ここに記述。このfunctionは誰でも実行できる
    (string memory) {
        return privateFunc();
    }

//③
    function internalFunc() internal pure returns (string memory)
                         // ^^^^^^^^^ここに記述。このfunctionはを継承したfunctionからは、オーナーであればアクセス可能
    {
        return "internal function called";
    }

//④
    function externalFunc() external pure returns (string memory)
                         // ^^^^^^^^^ここに記述。外部からのみアクセス可能
        return "external function called";
    }


```

今後、どんどん掘り下げていきたいと思います。
