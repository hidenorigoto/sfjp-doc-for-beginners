blogチュートリアル(2) データベースの設定
========================================

MySQLにblogsymfonyデータベースを作成
------------------------------------

このチュートリアルで使用するデータベースの名前を「**blogsymfony**」とします。
まずはphpMyAdmin（またはコマンドラインなど、お好きなツール）を使って、MySQLに**blogsymfony**という名前のデータベースを作成してください。

> **NOTE**
> データベースの照合順序は「utf8_general_ci」または「utf8_bin」に設定してください。


データベースへの接続設定
------------------------

MySQLデータベースへ接続するユーザー名、パスワード、およびデータベース名をsymfonyに設定します。
この設定は、config/databases.ymlファイルに記述します。
エディタでこのファイルを開き、以下のように編集してください。
(USERNAMEやPASSWORDは、それぞれお使いの環境のユーザー名とパスワードに置き換えてください。)

<pre>
all:
  doctrine:
    class: sfDoctrineDatabase
    param:
      dsn: 'mysql:host=localhost;dbname=blogsymfony'
      username: USERNAME
      password: PASSWORD
      attributes:
        default_table_charset: utf8
        default_table_collate: utf8_unicode_ci
</pre>

> **NOTE**
> symfonyの設定ファイルは、拡張子からも分かるように[YAML](http://ja.wikipedia.org/wiki/YAML)形式で記述します。
> YAMLでは、インデントにタブは使用してはいけません。かならず空白でインデントします。
> symfonyで使えるYAMLの詳細については、『[The symfony Reference Book YAMLフォーマット](http://www.symfony-project.org/reference/1_4/ja/02-YAML)』を参照してください。
