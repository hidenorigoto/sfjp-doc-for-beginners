blogチュートリアル(4) 追加の設定
================================

CSRFシークレットの変更
----------------------

symfonyではデフォルトでCSRF対策が有効になっています（symfony 1.3より。それ以前はオプション）。
サンドボックスパッケージをダウンロードした場合は、このCSRF保護に使われるシークレット文字列を必ず変更してください。
`apps/frontend/config/settings.yml`ファイルを開き、**csrf_secret**の値を適当な半角英数文字列に書き換えてください。

<pre>
all:
  .settings:
    # Form security secret (CSRF protection)
    csrf_secret:            fweefawkpkfwea230912jfasmknfa923 # 適当な文字列
</pre>


ディレクトリのパーミッション
----------------------------

Linux環境の場合は、いくつかのディレクトリのパーミッションをウェブサーバーのプロセスから書き込めるように設定する必要があります。
これを行うには、以下のようにsymfonyコマンドを実行してください。

<pre>
php symfony project:permissions
</pre>

> **TIP**
> 具体的には、`cache`および`log`ディレクトリを書き込み可能なパーミッションに設定します。
