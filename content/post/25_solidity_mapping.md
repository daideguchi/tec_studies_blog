---
title: "【solidity】配列のようなイメージのmappingの定義について"
date: 2022-09-25T16:19:40+09:00
draft: false
categories:
  - "学習アウトプット"
  - "solidity"
tags:
  - "プログラミング"
  - "solidity"
---

配列[]のようなイメージの`mapping`のイメージを学習した記録
<!--more-->

***

## 1.0_mappingの使い方

***
mappingは簡単にいうと、配列のような仕組みの構文で、「key」と「value」を定義するような概念です。
例えば、名簿管理の際に、出席番号（key）と名前・学年(value)のように、出席番号順に情報を管理するイメージをするとわかりやすいです。

[solidity公式ドキュメント_mapping](https://solidity-jp.readthedocs.io/ja/latest/types.html#mapping-types)

基本的な構文は以下のとおりです。
```
  mapping(key => value) public ステート変数名
```

***

## 2.0_実際に使ってみる

***

以下の構文は、アカウントの管理を想定して記述しています。

まずは、struct（構造体）に①名前と②メールアドレスを「userinfo」として格納します。

さらに、`mapping`を使い、userinfoをaccountsという配列に入れていくようなイメージです。

ここでは、keyを登録した順番。uintで数値です。

valueはstructに格納されている2つの情報を格納します。

```java Hello.java {.light .line-number .copy}

//アカウントの情報（名簿）
struct userinfo {
	string name;  // 名前
	string email; // Emailアドレス
}

//keyはuint(数値)、valueはuseinfo構造体の情報が入る。
//これらの情報を変数accountsに格納している
mapping(uint => userinfo) private accounts;
```

例えばaccountsに以下のような３人分のデータをあらかじめ登録してみます。
```

accounts[0].name = "aaaaa";
accounts[0].email = "aaaaa@com";
accounts[1].name = "bbbbb";
accounts[1].email = "bbbbb@com";
accounts[2].name = "ccccc";
accounts[2].email = "ccccc@com";
```

結果は以下の表のように整理されます。

|  `key` | `値`       | `name` |`email`    |
| -----  | ----       | ------- |------   |
| 0      |accounts[0]|aaaaa     |aaaaa@com|
| 1      | accounts[1]|bbbbb    |bbbbb@com|
| 2      | accounts[2]|ccccc    |ccccc@com|
