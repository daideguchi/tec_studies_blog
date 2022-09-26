---
title: "【solidity】ERC-20準拠のトークン発行やスマートコントラクトをより簡単にするライブラリ「OpenZeppelin」について"
date: 2022-09-26T22:47:23+09:00
draft: false
categories:
  - "学習アウトプット"
  - "solidity"
tags:
  - "プログラミング"
  - "solidity"
---

`OpenZeppelin`の導入部分についての記録
<!--more-->

***

## 1.0_OpenZeppelinとは

***

結論、`OpenZeppelin`とは、solidityのライブラリです。Dappsなどを開発する際に役に立ちます。

さて、ブロックチェーン開発において、必ずと言ってもいいほど登場するのが「トークン」や「NFT」です。

トークンとは、ブロックチェーン上で発行される「価値を持たせた何か（ポイントや株式のようなイメージ）」ものです。

このトークンを発行するにあたっては、ERC20のルールに準拠する必要があり、これは過去の記事でも触れましたのでそちらをご参照してみてください。

[【solidity】ERC-20の主な機能について](./17_ERC-20.md)

このERC-20トークンが実装すべき要件を、あらかじめ関数として定義してくれているので、あとはその定義された関数をインポートして使うだけです。

もちろん、それ以外の関数も多数用意されています。

※ERC-20については、Binance Academyに詳しく書いてあるので、以下転載します。

[Binance Academy ERC-20トークンの紹介](https://academy.binance.com/ja/articles/an-introduction-to-erc-20-tokens)
>ERC-20に準拠するためには、コントラクトにtotalSupply、balanceOf、transfer、transferFrom、approve、およびallowanceの6つの必須関数を含める必要があります。さらに、名前、シンボル、十進法などのオプション関数を指定することが可能です。

***

## 2.0_具体的な導入方法

***

まず、環境として、node.jsがインストールされていることが前提です。

[OpenZeppelin公式ドキュメント](https://docs.openzeppelin.com/)

開発しているディレクトリで以下のコマンドを実行することでインストールが完了します。
```
$ npm install @openzeppelin
```

インストール後はpackage.jsonで確認すると良いと思います。

***

## 3.0_導入後の使い方

***

実際にOpenZeppelinを使用する場合は、以下のようにファイルをインポートして使用します。ここでは、２つのファイルをインポートしています。

```java Hello.java {.light .line-number .copy}
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";//①
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";//②


contract MemberNFT is ERC721 {

  //トークン名とトークンシンボルを定義
  constructor() ERC721("MemberNFT", "MEM") {}


 ////この記事では、この関数に注目してください////////////////////////////
  function nftMint(address to, string calldata uri) external onlyOwner {
        _tokenIds.increment(); //0を1増やして「1」にする
        uint256 newTokenId = _tokenIds.current(); //さらにここで１増やす


      ★  _mint(to, newTokenId); //NFT作成  ①の中に定義あり
      ★ _setTokenURI(newTokenId, uri); //newTokenIdにuriを紐づける  ②の中に定義あり


        emit TokenURIChanged(to, newTokenId, uri);
    }

```

***
***

例えば、上記は`@openzeppelin/contracts/token/ERC721/ERC721.sol`をインポートしています。

では、このインポートしたファイルを見てみましょう。

インポート元のファイルは、`node_modules`ファイルの中に格納されています。

```
①node_modules/@openzeppelin/contracts/token/ERC721/ERC721.sol
②node_modules/@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
```


⇨①ERC721.sol抜粋
```java Hello.java {.light .line-number .copy}
pragma solidity ^0.8.0;

import "./IERC721.sol";
import "./IERC721Receiver.sol";
import "./extensions/IERC721Metadata.sol";
import "../../utils/Address.sol";
import "../../utils/Context.sol";
import "../../utils/Strings.sol";
import "../../utils/introspection/ERC165.sol";

contract ERC721 is Context, ERC165, IERC721, IERC721Metadata {
    using Address for address;
    using Strings for uint256;

    // Token name
    string private _name;

    // Token symbol
    string private _symbol;

    // Mapping from token ID to owner address
    mapping(uint256 => address) private _owners;

    // Mapping owner address to token count
    mapping(address => uint256) private _balances;

    // Mapping from token ID to approved address
    mapping(uint256 => address) private _tokenApprovals;

    // Mapping from owner to operator approvals
    mapping(address => mapping(address => bool)) private _operatorApprovals;

    /**
     * @dev Initializes the contract by setting a `name` and a `symbol` to the token collection.
     */
    constructor(string memory name_, string memory symbol_) {
        _name = name_;
        _symbol = symbol_;
    }


・・・・
・・・・
//以下、関数がたくさん定義されている。ここでは「_mint」関数のみ抜粋

    function _mint(address to, uint256 tokenId) internal virtual {
        require(to != address(0), "ERC721: mint to the zero address");
        require(!_exists(tokenId), "ERC721: token already minted");

        _beforeTokenTransfer(address(0), to, tokenId);

        _balances[to] += 1;
        _owners[tokenId] = to;

        emit Transfer(address(0), to, tokenId);

        _afterTokenTransfer(address(0), to, tokenId);
    }

```

⇨②URIStorage.sol抜粋
```java Hello.java {.light .line-number .copy}
pragma solidity ^0.8.0;

import "../ERC721.sol";
・・・
・・・
・・・
・・・
    function _setTokenURI(uint256 tokenId, string memory _tokenURI) internal virtual {
        require(_exists(tokenId), "ERC721URIStorage: URI set of nonexistent token");
        _tokenURIs[tokenId] = _tokenURI;
    }
```

まず、ERC721.solの冒頭には色々と書いてありますが、ここでもimportだとか、状態変数の定義やmappingとあり、

そこから関数が定義がたくさん定義されています。

NFTを作成する関数である`_mint`は、①の`ERC721.sol`に定義されています。

また、`_setTokenURI`は、②の`URIStorage.sol`に定義されています。

これらをインポートすることによって、**一から定義する手間を大幅に省くことができる**ため、solidityを開発する上ではとても役に立ちます。

***

他にもhardhatやether.jsなど、さまざまなツールがありますので、便利なものはどんどん取り入れていきましょう。
