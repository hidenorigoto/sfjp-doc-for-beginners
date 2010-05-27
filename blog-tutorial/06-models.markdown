blogチュートリアル(6) モデルの作成
==================================

このステップは、symfonyでは特に作業はありません。

なぜなら、**php symfony doctrine:build --all**コマンドを実行したときに、自動的にモデルファイルが生成されているからです。


モデルファイルの構成
--------------------

では、生成されたモデルファイルを見てみましょう。

<pre>
sf_sandbox/
  lib/
    model/
      doctrine/
        Post.class.php
        PostTable.class.php
        base/
          BasePost.class.php
</pre>

- **BasePost.class.php：** `sfDoctrineRecord`の派生クラスで、Postモデルの基本的な情報が書き込まれています。このファイルは編集してはいけません。
- **Post.class.php：** `BasePost`の派生クラスです。`post`テーブルの1つのレコードを表すクラスです。レコードインスタンスに対するカスタムメソッドなどを定義できます。
- **PostTable.class.php：** `Doctrine_Table`の派生クラスで、`post`テーブルを表すクラスです。テーブルに対する操作（特定の条件でレコードを取得するメソッドなど）を定義できます。

このように、1つのモデルに対して複数のファイルが生成されます。PostとPostTableに分かれているところがCakePHPとはやや異なります。
