blogチュートリアル(6) モデルの作成
==================================

このステップは、symfonyでは特に作業はありません。

なぜなら、**php symfony doctrine:build --all**コマンドを実行したときにモデルファイルが生成されているからです。


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

- **BasePost.class.php：** sfDoctrineRecordの派生クラスで、Postモデルの基本的な情報が書き込まれています。このファイルは編集してはいけません。
- **Post.class.php：** BasePostの派生クラスです。postテーブルの1つのレコードを表すクラスです。レコードインスタンスに対するカスタムメソッドなどを定義できます。
- **PostTable.class.php：** Doctrine_Tableの派生クラスで、postテーブルを表すクラスです。テーブルに対する操作（特定の条件でレコードを取得するメソッドなど）を定義できます。

このように、1つのモデルに対して複数のファイルが生成されます。PostとPostTableと分かれているところがCakePHPとはやや異なります。
