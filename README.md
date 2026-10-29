# luajpunct

日本語の句読点（、。）を、全角のコンマやピリオド（，．：U+FF0C、U+FF0E）に置換するスタイルファイルです。

## インストール

`.tex`ファイルと同じディレクトリに`luajpunct.sty`を配置して、LuaLaTeXでコンパイルしてください。当然、スタイルファイルをTeXのシステムディレクトリ内に配置する方法などでもかまいません。

句読点の置換にはLuaのコールバック機能を使用しているため、LuaLaTeX以外でのコンパイルには対応していません。

## 使い方

### パッケージの読み込み

プリアンブルに以下を記述すれば、コンパイル時に自動で句読点が置換されます。
```tex
\usepackage[dot,comma]{luajpunct}
```
オプションはdotとcommaの2つがあり、置換を行ってほしいものを記述します。
```tex
% 句点も読点も置換する
\usepackage[dot,comma]{luajpunct}
% 句点のみ置換する
\usepackage[dot]{luajpunct}
% 読点のみ置換する
\usepackage[comma]{luajpunct}
% 句点も読点も置換しない
\usepackage{luajpunct}
```

### 置換しない句読点

引用文などで、句読点を置換してほしくない場合は`\、`や`\。`を使用します。これらは`、`や`。`に置換されます。この置換はオプションの有無にかかわらず（上記の4つの組み合わせ全てで）行われます。

また、デフォルトで`\verb`・`\verb*`コマンド、`verbatim`・`verbatim*`・`lstlisting`・`minted`環境内の句読点は置換しません。
置換の判定を正常に行うため、これらの環境の`\begin`コマンドおよび`\end`コマンドは、独立した行に記述してください。

### その他のコマンド

`verbatim`・`verbatim*`・`lstlisting`・`minted`環境に加えて、句読点の置換を行わない環境を追加する場合は、プリアンブルなど、その環境を使用する前の行で以下を記述します。
```tex
\luajpunctIgnoreEnv{environment}
```
ここで、`environment`は環境の名前です。この環境についても、`\begin`コマンドおよび`\end`コマンドは、独立した行に記述してください。

また、任意の場所で一時的に句読点の置換を停止する場合は、置換の停止を開始する行の前に
```tex
\luajpunctOff
```
を、停止した句読点の置換を再開する場合は、置換を再開する行の前に
```tex
\luajpunctOn
```
を挿入します。

```tex
句読点が置換される
\luajpunctOff
句読点が置換されない
\luajpunctOn
句読点が置換される
```
