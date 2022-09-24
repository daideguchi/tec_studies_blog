---
title: "【solidity】アクセスの制限をする修飾子modifierについて"
date: 2022-09-23T18:52:44+09:00
draft: false
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

以下のコードは、オーナーのみが実行できることを定義したものです。

```java Hello.java {.light .line-number .copy}
    // アクセス制限の実装
    modifier onlyOwner {
    // コントラクトを呼び出したアドレスがオーナーと一致するか確認する
    // 一致しない場合は処理を止める
        require(msg.sender == owner); 
        _; // modifierの末尾に必要→元の処理に戻る
    }
```

例えば、下記のコードは、トークンを移転する処理になりますが、

オーナーが所有するトークンは勝手に第三者が別の人に送付するということができないように、上記で定義した`modifierの「onlyOwner」`を下記のように修飾子として使用します。

このトークン移転処理を行う前に、`modifier onlyOwner`を呼び出し、これから処理する人が「トークン所有のオーナーか」どうかを判定します。

問題がなければ、元の処理＝トークン移転処理に戻り、処理を続行します。

この元の処理に戻るというコートは上記で記述している`_;`になります。

```java Hello.java {.light .line-number .copy}

    /// @dev Tokenを移転する
    function transfer(address to, uint256 amount) public onlyOwner {
        if(owner == msg.sender){
            //オーナーが預入している量までしか取引できないようにする
            require(_balances[owner] - _bankTotalDeposit >= amount, "Amounts greater than the total supply cannot be transferred");
        }
        address from = msg.sender;
        _transfer(from, to, amount);
    }
```

***

## 2.0_その他の参考事例

***

①については、NFTを所有しているかどうかの確認のためのもので、NFTを所有していれば、処理を続行させます。

②については、オーナー以外のみ処理をさせるための制限で、現在操作している人（msg.sender)がオーナーでない場合は、処理を続行させます。

```java Hello.java {.light .line-number .copy}
pragma solidity ^0.8.9;

interface MemberToken {
    //MemberNFTが所持しているNFTの個数を返す。balanceOfはERC721.solに規定
    function balanceOf(address owner) external view returns (uint256);
}

contract TokenBank {
    //状態変数の定義
    MemberToken public memberToken;
    .....
    .....
}

以下、modifierーーーーーーーーーーーーーーーーー

 【①】
    /// @dev NFTメンバーのみ。制限したい処理（function）にonlyMenberを加える（visibilityの後ろ）ことで処理の実行制限がかけられる
    modifier onlyMenber() {
        require(memberToken.balanceOf(msg.sender) > 0, "not NFT member");
        _; //後続処理
    }

 【②】
    /// @dev オーナー以外
    modifier notOwner() {
        require(owner != msg.sender, "Owner cannot execute");
        _; //後続処理
    }

ーーーーーーーーーーーーーーーーー

```
