blogチュートリアル(11) 投稿記事の削除
=====================================

次は、ユーザーが既存の記事を削除できるようにしてみましょう。

これは、postモジュールのdeleteアクションとして実装します。
`apps/frontend/modules/post/actions/actions.class.php`ファイルをエディタで開き、以下のコードをクラス内の末尾に**追加**してください。

	[php]
	public function executeDelete(sfWebrequest $request)
	{
	  $id = $request->getParameter('id');
	  $this->forward404Unless($id);
	  Doctrine_Query::create()
	    ->delete()
	    ->from('Post p')
	    ->where('p.id = ?', $id)
	    ->execute();
	  $this->getUser()->setFlash('info', 'データを削除しました。');
	  $this->redirect('post/index');
	}

このコードでは、主に以下の3つのことを行っています。

1. パラメータから削除対象のIDを取得する。
2. 指定されたIDに対応するレコードを削除するDoctrineのDQLを作成し実行する。
3. 削除完了メッセージをflashにセットして、一覧画面へリダイレクトする。

> **TIP**
> URLパラメーターは、`$request->getParameter()`で取得します。
> もし`id`パラメーターが渡されていない場合は、404ページへ転送しています。



DQL
---

symfonyは、デフォルトでDoctrineというORMを使用しています。
DQLはDoctrine独自の機能で、SQLに似た構文でクエリを組み立てます。
詳細は『[The symfony and Doctrine book 6章 データを扱う](http://www.symfony-project.org/doctrine/1_2/ja/06-Working-With-Data)』などを参照してください。


削除の確認
----------

アクションの追加ができたら、ブラウザで一覧画面にアクセスして各行の「削除」をクリックしてみてください。
「削除」をクリックすると、JavaScriptの確認ダイアログが表示されます。
このダイアログで「OK」をクリックすると、先ほど追加したdeleteアクションが実行されます。
その後一覧画面にリダイレクトされ、flashメッセージが表示されます。

このように、リンクをクリックしたときにJavaScriptの確認ダイアログを表示するには、link_toヘルパーのconfirmオプションを使います。
