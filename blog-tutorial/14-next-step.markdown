blogチュートリアル(14) まとめと応用
===================================

このチュートリアルをマスターできたら、次はどうしますか？


チュートリアルのプログラムを改良してみる
----------------------------------------

このチュートリアルのアプリケーションは非常にシンプルなので、いろいろと不足しています。
必要だと思う機能を追加してみてください。
例えば、以下のような機能が考えられます。

- 各投稿データにカテゴリを追加
- 投稿の削除画面や編集画面のURLで無効なIDが指定された場合のエラー処理
- 投稿の一覧画面に検索機能を追加
- 投稿の一覧画面にページング機能を追加
- ：


次のチュートリアルへ進んでみる
------------------------------

symfonyには、もう少し複雑で規模の大きなアプリケーションを扱うJobeetチュートリアルがあります。

- [Practical Symfony](http://www.symfony-project.org/jobeet/1_4/Doctrine/ja/)

Jobeetチュートリアルでは、symfonyのほぼすべての機能について学ぶことができます。


Symfonyについて、詳しく学んでみる
---------------------------------

Symfonyについて学ぶには、上記Jobeetチュートリアルと合わせて、以下のドキュメントを読んでおくとよいでしょう。

- [Symfony完全ガイド 1.2(The Definitive Guide to symfony 1.2)](http://cloud.github.com/downloads/masakielastic/masakielastic.github.com/sf-book-1.2-ja.pdf)<br />
  Symfony 1.2時点でのドキュメントですが、Symfony 1.4でも根本の部分は共通していますので、十分に役立ちます。
  Symfonyの基本をしっかり学ぶ事ができます。
  入門者から中級者まで、一読をおすすめします。


チュートリアルをさらに理解するための補足
----------------------------------------

symfonyの理解を深めるために、本文では触れなかったsymfonyの機能についていくつか解説します。


### symfonyのオートロード

symfonyでは、PHPのオートロード機能を利用して、ライブラリ内のクラスや自動生成されるモデルクラス、フォームクラスなどを、明示的にincludeやrequireすることなく利用できます。

この「オートロード対象」となるクラスの設定は、`autoload.yml`という設定ファイルで設定でき、symfonyのデフォルトのオートロード設定は以下のファイルに記述されています。

<pre>
(symfony)/lib/config/config/autoload.yml
</pre>

このファイルの中身は以下のようになっています。

<pre>
autoload:
  # project
  project:
    name:           project
    path:           %SF_LIB_DIR%
    recursive:      true
    exclude:        [model, symfony, vendor]

  project_model:
    name:           project model
    path:           %SF_LIB_DIR%/model
    recursive:      true

  # application
  application:
    name:           application
    path:           %SF_APP_LIB_DIR%
    recursive:      true

  modules:
    name:           module
    path:           %SF_APP_DIR%/modules/*/lib
    prefix:         1
    recursive:      true
</pre>

つまり、以下のパスにあるクラスファイルは自動的にオートロード対象になります。

- (プロジェクトルート）/lib ディレクトリ以下で、model、symfony、vendorという名前以外のディレクトリ内のファイル
- (プロジェクトルート）/lib/model ディレクトリ以下のファイル
- (プロジェクトルート）/apps/（アプリケーション）/lib ディレクトリ以下のファイル
- (プロジェクトルート）/apps/（アプリケーション）/modules/*/lib ディレクトリ以下のファイル

上記以外のディレクトリをオートロード対象に追加したい場合は、プロジェクトやアプリケーションのconfigディレクトリにautoload.ymlファイルを作成し、追加したい設定を記述します。


