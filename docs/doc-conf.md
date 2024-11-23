# ドキュメントの構成

## チャプター

Markdownファイルはチャプターを構成し、チャプターごとにページが分けられます。チャプターはサブチャプターを持つことができます。

## SUMMARY.md

文章を構成するチャプターを列挙します。左側に表示されるサイドバーを構成し、目次の役割を持ちます。

連番を持たないプレフィックス/サフィックチャプターを持つことができます。プレフィックスキャプチャーはトップページになります。

セクションを使用してタイトルをつけることができ、ネストもできます。

```md
# Summary

[Introduction](README.md)

# User Guide

- [Installation](guide/installation.md)
- [Reading Books](guide/reading.md)
- [Creating a Book](guide/creating.md)

# Reference Guide

- [Command Line Tool](cli/README.md)
    - [init](cli/init.md)
    - [build](cli/build.md)
    - [watch](cli/watch.md)
    - [serve](cli/serve.md)
    - [test](cli/test.md)
    - [clean](cli/clean.md)
    - [completions](cli/completions.md)

-----------

[Contributors](misc/contributors.md)
```

## 開発リポジトリに同梱する場合の構成

開発リポジトリにドキュメントを同時に保存する場合、`src`はプログラムのソースが置かれるため、別のフォルダに変更します。GitHubでは`docs`フォルダと`README.md`ファイルが特別な役割を持ちます。GitHub上の見え方を考慮すると以下のようするのが良いです。

```
/
|-docs
|  |- SUMMARY.md
|  |- README.md
|- book.toml
```

`README.md`の内容は2つ考えられます。

* 簡単な説明とメインチャプターまとめたインデックスページとする
* `SUMMARY.md`と同じ内容とする

サブチャプターを含むような規模の文章の場合、`README.md`はメインチャプターのみ書く方が見通しが良いかもしれません。そして、このファイルはプレフィックスチャプターとして利用できるでしょう。

文章の規模が小さい場合や、より簡易にする場合は、`SUMMARY.md`と同じで良いでしょう。手動で内容をコピーして同期する方法もありますが、シンボリックリンクを作成するのが簡単です。

```
ln -s SUMMARY.md README.md
```

Gitはシンボリックリンクをそのまま扱え、GitHubはシンボリックリンクを考慮して表示するため、GitHub上でみた場合にも意図通りに (`README.md`を参照してシンボリックリンクの実態の`SUMMARY.md`を使用して) 表示されます。

## 存在しないファイルを作成する

`SUMMARY.md`に記述した**存在しないファイル**をビルド時に作成する機能があります。

```toml
[build]
create-missing = true
```

この機能はデフォルトで有効です。`SUMMARY.md`でアウトラインを作成し、そこから文章を書き始めることができます。
