blogチュートリアル(7) postモジュールの作成
==========================================

postモジュールの作成
--------------------

symfonyでは、モデルとコントローラ（モジュール、アクション）間に規約による関連づけはありません。
Postモデルの一覧を表示し、追加、編集、削除を行うためのモジュールの名前は何でも構いませんが、ここでは分かりやすいように「**post**」モジュールとします。
以下のコマンドをsf_sandboxディレクトリで実行して、postモジュールを作成しましょう。

<pre>
php symfony generate:module frontend post
</pre>

> **TIP**
> サンドボックスパッケージには、デフォルトでfrontendという名前のアプリケーションが含まれています。上のコマンドでは、アプリケーション名としてこのfrontendを指定しています。

モジュールを作成すると、apps/ディレクトリ配下に次のようなファイルが生成されます。

<pre>
sf_sandbox/
  apps/
    frontend/
      modules/
        post/
          actions/
            actions.class.php
          templates/
            indexSuccess.php
</pre>

- **actions.class.php：** postモジュールのアクションを記述するファイルです。
- **indexSuccess.php：** postモジュールのindexアクションを実行した場合に、レスポンスのレンダリングに使用されるテンプレートファイルです。PHP形式であることに注意してください。


indexアクションの編集
---------------------

それでは早速アクションを編集しましょう。actions.class.phpファイルをエディタで開きます。このファイルは、デフォルトで以下のような内容になっています。

	[php]
	/**
	 * test actions.
	 *
	 * @package    sf_sandbox
	 * @subpackage post
	 * @author     Your name here
	 * @version    SVN: $Id: actions.class.php 23810 2009-11-12 11:07:44Z Kris.Wallsmith $
	 */
	class postActions extends sfActions
	{
	 /**
	  * Executes index action
	  *
	  * @param sfRequest $request A request object
	  */
	  public function executeIndex(sfWebRequest $request)
	  {
	    $this->forward(''default'', ''module'');
	  }
	}

executeIndexメソッドの中身を次のように編集してください。

	[php]
	public function executeIndex(sfWebRequest $request)
	{
	  $this->posts = Doctrine_Core::getTable(''Post'')->findAll();
	}

このコードは次の2つのことを行っています。

- ORMであるDoctrineを使って、Postモデルのテーブルメソッド**findAll()**を呼び出し、postテーブルのすべてのレコードを取得しています。
- 上記で取得したレコードを、ビューで「$posts」という変数経由で使用できるように設定しています。
