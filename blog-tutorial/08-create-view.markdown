blogチュートリアル(8) ビューの作成
==================================

このステップでは、レスポンスをHTMLに整形するためのビューを作成します。

このステップが終わると、ようやく投稿記事の一覧画面を表示できるようになります。


indexSuccess.phpファイルの編集
------------------------------

`apps/frontend/modules/templates/indexSuccess.php`ファイルを開き、以下のように編集して下さい。

	[php]
	<h1>Blog posts</h1>
	<table>
	  <tr>
	    <th>Id</th>
	    <th>Title</th>
	    <th>Actions</th>
	    <th>CreatedAt</th>
	  </tr>
	
	  <!-- ここから、$posts配列をループして、投稿記事の情報を表示 -->
	
	  <?php foreach ($posts as $post): ?>
	  <tr>
	    <td><?php echo $post->getId() ?></td>
	    <td>
	      <?php echo link_to($post->getTitle(), 'post/edit?id=' . $post->getId()) ?>
	    </td>
	    <td>
	      <?php echo link_to('編集', 'post/edit?id=' . $post->getId()) ?>
	      <?php echo link_to('削除', 'post/delete?id=' . $post->getId(),
	                         array('confirm'=>'id=' . $post->getId() . 'のデータを削除してもよろしいですか？')) ?>
	    </td>
	    <td><?php echo $post->getCreatedAt() ?></td>
	  </tr>
	  <?php endforeach; ?>
	
	</table>
	<?php echo link_to('新規追加', 'post/new') ?>
	<?php if ($flash = $sf_user->getFlash('info')): ?>
	<?php echo $flash ?>
	<?php endif ?>

**$posts**変数をループで処理している点はCakePHPと同じです。
しかし、**$posts**変数の中に格納されているのがレコードを表す**オブジェクト**になっている点が大きく異なります。したがって、レコードのIDやタイトルを取得するには以下のようにオブジェクトのメソッドを使用します。

- `id`フィールド: $post->getId()
- `title`フィールド: $post->getTitle()
- `created_at`フィールド: $post->getCreatedAt()

> **TIP**
> データベースのフィールド名と、アクセサメソッド名の対応はお分かりでしょうか。フィールド名は「小文字＋アンダースコア」で、対応するアクセサ名は、アンダースコアを削除し、各パートの先頭文字を大文字にしたものになっています。



link_toヘルパー
---------------

ビューでリンクを記述する場合、symfonyでは**link_toヘルパー**を使用します。
link_toヘルパーの詳細は、『[The Definitive Guide to symfony 1.2 第9章 リンクとルーティングシステム](http://symfony.sarabande.jp/book/1.2/09-Links-and-the-Routing-System.html#link.helpers)』を参照してください。


> **TIP**
> 編集や削除のリンクを作成するコードで、link_toヘルパーの2つめの引数に内部URLと合わせてidパラメーターを追加しています。



ブラウザで確認
--------------

ビューのファイルを保存したら、ブラウザで「`http://localhost/sf_sandbox/web/frontend_dev.php/post/index`」にアクセスしてみてください。
この時点では、最初にfixtureで登録した3件のレコードがリストに表示されればOKです。

> **CAUTION**
> アクセスするURLは、お使いの環境に合わせて適宜読み替えて下さい。

> **TIP**
> 表示された各行の編集や削除のリンクがどのようなURLになっているのかも確認してみてください。


