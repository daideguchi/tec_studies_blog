---
title: "【solidity】REMIX IDEでコーディング前の準備"
date: 2022-08-15T12:24:34+09:00
draft: false
categories:
  - "学習アウトプット"
  - "solidity"
tags:
  - "プログラミング"
  - "solidity"
---
REMIX IDEを使用してsolidityを書く事前準備の記録  
``"SPDX"と"バージョンの指定"``
<!--more-->

***
## 1.0_REMIX IDEを起動する
***
まず、*＊[REMIX IDE](https://remix.ethereum.org/)**を起動しましょう。  
以下の画像は、公式ドキュメントから引用していますが、REMIX IDEを開くと、以下のような画面に遷移します。
***
![solidity_logo](../../img/11_solidity02.png)
***

***
## 2.0_任意のファイルを開いてみる
***
試しに、左側のWorkSpaceの階層から、デフォルトで入っている``contract/artifacts/1_Strage.sol``を開いてみましょう。  
```java Hello.java {.light .line-number .copy}
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

~~~~~~~~~~~~~~~~~~~~

```  
冒頭はこのような書き振りになっていると思います。
- 1.SPDXを指定して、ライセンス情報を明らかにする（コメントアウト部分）
- 2.pragma solidity ... でバージョンの指定をする。

***
## 3.0_SPDXの設定をする
***
SPDXとはWikipediaによると、  
>Software Package Data Exchange（SPDX）[1]は、Linux Foundationの傘下のプロジェクトである[2]。SPDXプロジェクトは、組織がソフトウェアライセンスやBills of material（BOM、部品表、ソフトウェア構成表ともいう）に関するメタデータのオープンスタンダードを策定し[3]、関連するフォーマットなどを円滑に利用するためのSPDX のオンラインツールなども整備している。

とあり、``ライセンスを明示するために記述``する必要があります。  
ライセンスと言っても、何も特別な手続きなど不要です。  
記述できる型名は無数にあります。  

以下のサイトに記述内容が網羅されています。  
**↓↓**  
**[SPDXライセンスリスト](https://spdx.org/licenses/)**  
記述方法としては、各solidity(拡張子が.sol)のファイルの冒頭にコメントアウト形式で記述します。  
```java Hello.java {.light .line-number .copy}
// SPDX-License-Identifier: ○○ ←ここにライセンスを明記します。
 ライセンスは上記リスト内の Identifier の部分に該当します
```
主に使用するのは以下のものかと思います。
- MIT(商用利用可能としてオープンするコード)
- Unlicense(商用利用不可のコード)
```java Hello.java {.light .line-number .copy}
// SPDX-License-Identifier: MIT
// SPDX-License-Identifier: Unlicense
~~~~~~~~~~~~~~~~~~~~
```  

これらの記載がないと動かないわけではありませんが、solidity側が明示を求めているので、しっかりと記述していきましょう。

**↓↓**  
[SPDXに関するsolidityドキュメントページ（参考）](https://docs.soliditylang.org/en/v0.6.8/layout-of-source-files.html)  

***
## 4.0_バージョンの指定
***
``solidity``を記述するうえで、バージョンの指定は、**各ファイルで必須**です。  
ライセンス情報の一つ下の行に記述していきます。  
そのため、**何か教材などを参考に開発する場合は、バージョンの指定に注意を払いましょう。**  
また、最新バージョンは、solidity公式より確認することができます。  
**↓↓**  
**[solidity公式](https://docs.soliditylang.org/)**  
なお、バージョンの記述方法も様々ありますが、``pragma solidity 〇〇``という記述方法となります。 
○○の部分には、以下のような記述を取ります。  
不等号で、「○○以上、○○以下のバージョンを使う」のような記述方法をとることもできます。
```
 ^0.8.16
 or
 >=0.7.0 <0.9.0
```
```java Hello.java {.light .line-number .copy}
pragma solidity ^0.8.16
or
pragma solidity >=0.7.0 <0.9.0
~~~~~~~~~~~~~~~~~~~~
```  

この「ライセンス」と「バージョン」は各solidityファイルごとに必ず設定していくようにしましょう。

***
## 5.0_solidity関連のリンク
***
以下、割と使いそうなリンクをひとまずまとめてみました。  

- **[solidity公式Document](https://docs.soliditylang.org/)**
- **[sokidityのGithub](https://github.com/ethereum/solidity/blob/v0.6.8/docs/layout-of-source-files.rst)**
- **[REMIX IDEのエディタ](https://remix.ethereum.org/)**
- **[REMIX IDEの公式](https://remix-project.org/)**
- **[REMIX IDEのGithub](https://github.com/ethereum/remix-ide)**

