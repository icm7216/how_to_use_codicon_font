# How to use codicon fonts in VS Code markdown


VS Codeのcodicon icon fontをmarkdownで使う

目的は、codiconのchevron-up,down,left,rightをmarkdownプレビューに表示すること。

# codiconフォントをインストール

[microsoft/vscode-codicons](https://github.com/microsoft/vscode-codicons)からcodiconフォント(codicon.ttf)を取得し`C:\WINDOWN\FONTS`にインストールする。
1.  `codicon.ttf`を右クリックし、「その他のオプションを表示」を選択。
2. 「すべてのユーザーに対してインストール」を選択。

# StyleSheetを作成

インストールしたcodiconフォントのコードポイントのうち、U+EAB4, U+EAB5, U+EAB6, U+EAB7 を有効にするスタイルシートを作成。

`my_codicon.css`
```
@font-face {
  font-family: "codicon";
  src: local("codicon.ttf") format("truetype");
  unicode-range: U+EAB4-EAB7
 }

.codicon, i[class*='chevron-'] {
  font: normal normal normal 1em codicon;
  font-family: codicon;
  display: inline-block;
	text-align: center;
}

.chevron-down:before { content: "\eab4" }
.chevron-left:before { content: "\eab5" }
.chevron-right:before { content: "\eab6" }
.chevron-up:before { content: "\eab7" }
```

# settings.jsonに追加

`settings.json`にスタイルシートを登録。
```
  "markdown.styles": [
    "my_codicon.css"
  ]
```

# 表示テスト

## コードポイントを指定

codicon chevron iconのコードポイントはつぎのとおり。
*  U+EAB7: chevron-up
*  U+EAB4: chevron-down
*  U+EAB5: chevron-left
*  U+EAB6: chevron-right


次のようにHTMLでコードポイントを指定して記述するとプレビュー側に表示される。
```
<div>プレビュー側に<i class="codicon">&#xeab7</i>chevron-upと表示される。</div>
```

<div>プレビュー側に<i class="codicon">&#xeab7</i>chevron-upと表示される。</div>


## コードポイントに対応させたクラス名を指定

*  `chevron-up`
*  `chevron-down`
*  `chevron-left`
*  `chevron-right`

次のようにクラス名を指定して記述するとプレビュー側に表示される。

```
<div>プレビュー側に<i class="chevron-up"></i>chevron-upと表示される。</div>
```

<div>プレビュー側に<i class="chevron-up"></i>chevron-upと表示される。</div>


こちらの記述方法は、markdownと混在させてもうまく認識してくれるようだ。
*  <i class="chevron-up"> chevron-up</i>
*  <i class="chevron-down"> chevron-down</i>
*  <i class="chevron-left"> chevron-left</i>
*  <i class="chevron-right"> chevron-right</i>

----
----


<h1>Codicon</h1>

<p>Specify code point</p>
<div>
  <ul>
    <li><i class="codicon">U+EAB7: &#xEAB7 Up</i></li>
    <li><i class="codicon">U+EAB4: &#xEAB4 Down</i></li>
    <li><i class="codicon">U+EAB5: &#xEAB5 Left</i></li>
    <li><i class="codicon">U+EAB6: &#xEAB6 Right</i></li>        
  </ul>
</div>

<p>Specify class name</p>
<div>
  <ul>
    <li><i class="chevron-up"> chevron-up</i></li>
    <li><i class="chevron-down"> chevron-down</i></li>
    <li><i class="chevron-left"> chevron-left</i></li>
    <li><i class="chevron-right"> chevron-right</i></li>
  </ul>
</div>

----
----

# 付録

## codicon以外の関連アイコンのコードポイント

<div>
  <p>Modifier Letter Arrowhead</p>
  <ul>
    <li>U+02C4: &#x02C4 Up</li>
    <li>U+02C5: &#x02C5 Down</li>
    <li>U+02C2: &#x02C2 Left</li>
    <li>U+02C3: &#x02C3 Right</li>
  </ul>

  <p>Black pointing triangle</p>
  <ul>
    <li>U+25B2: &#x25B2 Up</li>
    <li>U+25BC: &#x25BC Down</li>
    <li>U+25C0: &#x25C0 Left</li>
    <li>U+25B6: &#x25B6 Right</li>
  </ul>

  <p>White pointing triangle</p>
  <ul>
    <li>U+25B3: &#x25B3 Up</li>
    <li>U+25BD: &#x25BD Down</li>
    <li>U+25C1: &#x25C1 Left</li>
    <li>U+25B7: &#x25B7 Right</li>
  </ul>

  <p>Black pointing small triangle</p>
  <ul>
    <li>U+25B5: &#x25B5 Up</li>
    <li>U+25BF: &#x25BF Down</li>
    <li>U+25C3: &#x25C3 Left</li>
    <li>U+25B9: &#x25B9 Right</li>
  </ul>

  <p>BLACK MEDIUM POINTING TRIANGLE CENTRED</p>
  <ul>
    <li>U+2BC5: &#x2BC5 Up</li>
    <li>U+2BC6: &#x2BC6 Down</li>
    <li>U+2BC7: &#x2BC7 Left</li>
    <li>U+2BC8: &#x2BC8 Right</li>
  </ul>
</div>



参考: 

*   [css - What characters can be used for up/down triangle (arrow without stem) for display in HTML? - Stack Overflow](https://stackoverflow.com/questions/2701192/what-characters-can-be-used-for-up-down-triangle-arrow-without-stem-for-displa)

*   [microsoft/vscode-codicons: The icon font for Visual Studio Code](https://github.com/microsoft/vscode-codicons)
