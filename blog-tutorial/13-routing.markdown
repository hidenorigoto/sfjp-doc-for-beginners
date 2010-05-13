blogチュートリアル(13) ルーティング
===================================

最後にsymfonyのルーティング機能について少しだけ触れておきましょう。

まずは、apps/frontend/config/routing.ymlファイルをエディタで開いてください。
以下のような設定になっているはずです。


<pre>
# You can find more information about this file on the symfony website:
# http://www.symfony-project.org/reference/1_4/en/10-Routing

# default rules
homepage:
  url:   /
  param: { module: default, action: index }

# generic rules
# please, remove them by adding more specific rules
default_index:
  url:   /:module
  param: { action: index }

default:
  url:   /:module/:action/*
</pre>


これが初期状態でのルーティング設定で、3つのルーティング設定があります。

1. **homepage:** ルートディレクトリにアクセスした時に実行されるモジュールとアクションを指定しています
2. **default_index:** ルートディレクトリ + モジュール名という形式のURLにアクセスした場合に、モジュール名に対応するモジュールのindexアクションが実行される設定です
3. **default:** ルートディレクトリ + モジュール名/アクション名という形式のURLにアクセスした場合に、対応するアクションが実行される設定です。通常、1と2以外のすべてのURLがこのルートにマッチします。


投稿一覧をホームページに
------------------------

では、投稿一覧をホームページに設定してみましょう。
routing.ymlのhomepageの部分を、以下のように変更します。

<pre>
homepage:
  url:   /
  param: { module: post, action: index }
</pre>

これで、postモジュールのindexアクションが、ホームページに設定されました。
ブラウザでホームページ（今回は、http://～～/frontend_dev.php）にアクセスして、投稿一覧画面が表示されることを確認してみてください。


> **NOTE**
> 投稿の追加や編集画面では、データの保存後に「post/index」へリダイレクトしていますが、このリダイレクト先が自動的に変更されていることにお気づきでしょうか。
> また、追加画面、編集画面にある「一覧に戻る」というリンクのリンク先も自動的に変更されています。
