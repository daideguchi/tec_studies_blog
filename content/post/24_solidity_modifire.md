---
title: "【solidity】アクセスの制限をするmodifier構文"
date: 2022-09-23T18:52:44+09:00
draft: true
categories:
  - "学習アウトプット"
  - "ビジネス系"
  - "その他"
tags:
  - "プログラミング"
  - "ビジネス"
  - "test"
---

例えばオーナーのみ実行したいときに処理のアクセス制限をする`modifier`についての記録
<!--more-->

***

## 1.0_modifierの使い方

***

基本的に`modifier`は、一連の処理の中で使います。

[solidity公式ドキュメント_modifier](https://solidity-jp.readthedocs.io/ja/latest/structure-of-a-contract.html#function-modifiers)



```java Hello.java {.light .line-number .copy}
    // アクセス制限の実装
    modifier onlyOwner {
    // コントラクトを呼び出したアドレスがオーナーと一致するか確認する
    // 一致しない場合は処理を止める
        require(msg.sender == owner); 
        _; // modifierの末尾に必要→元の処理に戻る
    }
```

例えば
```java Hello.java {.light .line-number .copy}

```

***

## 

***

***

## 

***