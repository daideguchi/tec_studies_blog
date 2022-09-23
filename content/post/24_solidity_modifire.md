---
title: "【solidity】アクセスの制限をするmodifire構文"
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

<!--more-->


***

## 

***

```java Hello.java {.light .line-number .copy}

    // ④アクセス制限の実装
    modifier onlyOwner {
    // コントラクトを呼び出したアドレスがオーナーと一致するか確認する
    // 一致しない場合は処理を止める
        require(msg.sender == owner); 
        _; // modifierの末尾に必要
    }

```


***

## 

***

***

## 

***