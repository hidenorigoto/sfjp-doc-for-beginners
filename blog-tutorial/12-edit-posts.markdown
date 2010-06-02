blogチュートリアル(12) 投稿記事の編集
=====================================

最後に既存の記事を編集できるようにしてみましょう。
ここまで学習された方は、どのような手順で編集機能を実装するか、少し自分で考えてみましょう。


記事の編集は、記事の追加と記事の削除の処理を組み合わせた内容になります。つまり、

1. GETメソッドでのアクセス時は、指定されたIDに対応するレコードを読み込んで、フォームの初期値として表示する。
2. PUTメソッドでのアクセス時は、送信されたデータでデータベースに保存する。

データの追加の時もそうでしたが、2についてはほとんどsymfonyが自動的に行ってくれます。（フォームにモデルが関連付けられているため）


editアクションの追加
--------------------

まずはアクションの実装から始めましょう。
`apps/frontend/modules/post/actions/actions.class.php`ファイルをエディタで開き、以下のコードをクラス内の末尾に**追加**してください。

	[php]
	public function executeEdit(sfWebrequest $request)
	{
	  $id = $request->getParameter('id');
	  $this->forward404Unless($id);
	  $this->form = new PostForm(
	    Doctrine_Core::getTable('Post')->findOneById($id)
	    );
	  if ($request->isMethod(sfRequest::PUT))
	  {
	    $this->form->bind($request->getParameter($this->form->getName()));
	    if ($this->form->isValid())
	    {
	      $this->form->save();
	      $this->getUser()->setFlash('info', 'データを更新しました。');
	      $this->redirect('post/index');
	    }
	  }
	}

パラメーターで渡された`id`を使って、`post`テーブルからレコードを読み込んでいます。
さらに、読み込んだレコードオブジェクトを使ってフォームを初期化しています。
こうすることで、レコードの値がフォームのウィジェットの初期値にセットされます。
フォームを初期化した後の処理は、newアクションの場合とほぼ同じです。

> **CAUTION**
> 既存データを編集するフォームの場合は、フォームの送信はPUTメソッドとなることに注意してください。


editSuccessビューの作成
-----------------------

次にビューを実装します。
`apps/frontend/modules/post/templates/editSuccess.php`ファイルを作成してエディタで開き、以下のコードを入力してください。
ビューのコードも、addの場合とほとんど同じです。

	[php]
	<?php echo $form->renderFormTag(url_for('post/edit?id=' . $form->getObject()->getId())) ?>
	<table>
	<?php echo $form ?>
	</table>
	<input type="submit" name="edit" value="edit" />
	</form>

> **CAUTION**
> newの場合と同様にフォームクラスの`renderFormTag`メソッドを使ってFORMタグを生成しています。
> 既存レコードの編集画面の場合は、symfonyにより自動的にPUTメソッドをエミュレートするタグが生成されます。
> これは、出力されたHTMLソースを見ると分かりますが、FORMタグのアクション自体はPOSTで、HIDDEN要素として`sf_method`にPUTという値が指定されます。この部分をsymfonyが解釈して、PUTメソッドとして処理します。


編集動作の確認
-------------

アクションとビューの実装が完了したら、ブラウザからテストしてみましょう。
一覧画面で各投稿の「編集」リンクをクリックして投稿の編集フォームを表示し、内容を変更してみてください。
変更した内容が反映されるでしょうか？

> **NOTE**
> 編集画面で使うフォーム`PostForm`クラスは、新規追加画面で使用したクラスと同じです。一般的なケースでは、このように新規追加と編集とで同じフォームクラスを再利用できます。

