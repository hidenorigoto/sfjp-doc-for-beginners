blogチュートリアル(3) スキーマの定義とテーブルの生成
====================================================

スキーマの定義
---------------

symfonyでは、データベースのスキーマをsymfony内の設定ファイル（schema.yml）に記述し、この設定から、データベース内にテーブルを生成します。
`config/doctrine/schema.yml`ファイルをエディタで開き、以下のように編集してください。

<pre>
Post:
  actAs:
    Timestampable:
  columns:
    id:
      primary: true
      unsigned: true
      type: integer
      autoincrement: true
    title:
      type: string(50)
    body:
      type: string
</pre>

> **NOTE**
> CakePHPの場合はテーブル名に複数形（ブログチュートリアルでは「posts」）を使用するのに対し、symfonyでは単数形を使用することに注意してください。
> また、スキーマの定義では、モデル名にはキャメルケース、カラム名には小文字とアンダースコアを使って命名することに注意が必要です。


テーブルの生成
--------------

定義したスキーマに基づいてデータベースにテーブルを生成しましょう。コマンドラインでプロジェクトディレクトリ（sf_sandbox）へ移動し、以下のコマンドを実行します。

<pre>
php symfony doctrine:build --all
</pre>

確認プロンプトが表示されますので、「y」を入力してコマンドの実行を継続します。
メッセージの最後に以下のような行があれば、テーブルの生成が完了しています。

<pre>
>> doctrine  created tables successfully
</pre>

phpMyAdminで、postテーブルが生成されているかどうか確認してみてください。


fixtureを使ったテストデータの投入
---------------------------------

このチュートリアルで使用するテストデータもここで投入しておきましょう。
symfonyにはRuby on Rails由来のfixture機能があり、YAML形式で記述したテストデータを簡単にデータベースに投入できます。
`data/fixtures/fixtures.yml`ファイルを開き、次のように編集してください。

<pre>
Post:
  post1:
    title: タ&lt;b&gt;イ&lt;/b&gt;トル
    body:  これは、&lt;br /&gt;記事の本文です。

  post2:
    title: またタイトル
    body:  そこに本文が続きます。

  post3:
    title: タイトルの逆襲
    body:  こりゃ本当に面白そう！うそ。
</pre>

ファイルを保存したら、プロジェクトのルートディレクトリで以下のコマンドを実行してください。

<pre>
php symfony doctrine:data-load
</pre>

このコマンドを実行すると、fixtureファイルに定義したデータがデータベースに投入されます。
phpMyAdminでpostテーブルにレコードが追加されているかどうか確認してください。


> **NOTE**
> CakePHPの場合、先にCREATE TABLE文などにより手作業で直接データベースにテーブルを作成し、この情報をCakePHPが読み取って動作します。
> symfonyの場合は、schema.ymlの設定を元に動作し、データベースのテーブルもスキーマファイルから生成されますので、CakePHPとは順序が逆になります。
> ただし、データベースの既存のテーブル情報からschema.ymlを生成することも可能です。
> 『[The symfony Reference Book タスク](http://www.symfony-project.org/reference/1_4/ja/16-Tasks#chapter_16_sub_doctrine_build_schema)』を参照してください。

