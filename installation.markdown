Symfonyのインストール方法（入門者・評価向け）
============================================

> **TIP**
> この文書は、Symfony 1系を対象としています。

Symfonyには、以下の5種類のインストール方法があります。

1. pearによるインストール
2. Symfonyパッケージをダウンロードしてインストール
3. Symfony Sandboxパッケージをダウンロードしてインストール
4. subversionリポジトリからチェックアウトしてインストール
5. gitリポジトリ（github）からcloneしてインストール

これらのインストール方法については、公式サイトのいくつかのドキュメントで説明されています。

- [The symfony framework Installation (英語)](http://www.symfony-project.org/installation/1_4)
- [Getting Started with symfony symfonyのインストール](http://www.symfony-project.org/getting-started/1_4/ja/03-Symfony-Installation)
- [Practical Symfony 1日目：プロジェクトを始める](http://www.symfony-project.org/jobeet/1_4/Doctrine/ja/01)

> **CAUTION**
> 古いドキュメントでは、pearを使ったインストール方法で解説されているものが多くありますが、現在ではpearを使ったインストールは推奨されていません。


このページでは、Symfony入門者向けに一番手軽なSandboxパッケージを使ったインストール方法について説明します。



SymfonyのSandboxパッケージをダウンロード
-------------------

まずは、Symfony 1.4の最新版パッケージをダウンロードしましょう。

Symfony 1.4の最新版パッケージのダウンロードは、公式サイトの[こちらのページ](http://www.symfony-project.org/installation)から行います。

![ダウンロードページ](images/installation.png)


**Download**という行にtgz形式、またはzip形式でダウンロードできるリンクが表示されています。
また、**Sourceパッケージ**と**Sandboxパッケージ**があります。

- **Sourceパッケージ：** Symfony本体のソースのみ
- **Sandboxパッケージ:** Symfony本体のソースと、sf_sandboxプロジェクト、frontendアプリケーションが初期化されたファイル群が付属

今回は、Symfony 1.4の**Sandboxパッケージ**をダウンロードして下さい（Symfony 1.4の列、Sandboxのtgzまたはzipリンクから）。

ウェブサーバーのDocumentRoot配下のディレクトリ、またはユーザーのpublic_html配下のディレクトリにて、ダウンロードしたファイルを展開してください。
以下のようなディレクトリ、ファイルがあります（ファイルは一部のみ記載しています）。

<pre class="command-line">
sf_sandbox/
    apps/
        frontend/
    cache/
    config/
    data/
    lib/
        form/
        vendor/
            symfony/
    log/
    plugins/
    test/
    web/
        css/
        images/
        js/
        sfDoctrinePlugin/
        uploads/
        .htaccess
        frontend_dev.php
        index.php
        robots.txt
    LICENSE
    README
    symfony
    symfony.bat
</pre>

Symfonyのディレクトリ構造について詳しく知りたい方は、『[The Definitive Guide to symfony(日本語訳) 2.2.2 ファイルのツリー構造](http://symfony.sarabande.jp/book/1.2/02-Exploring-Symfony-s-Code.html#file.tree.structure)』を参照してください。



symfonyの最初の動作確認
-----------------------

展開したSandboxパッケージのSymfonyがお使いの環境で動作するかどうか調べてみましょう。
コマンドラインでパッケージを展開したディレクトリ(sf_sandboxディレクトリ)へ移動し、以下のコマンドを実行してみてください。

<pre class="command-line">
php symfony -V
</pre>

以下のようにSymfonyのバージョン情報が表示されれば、動作確認はOKです。

<pre class="command-line">
symfony version 1.4.4 (パス)
</pre>



sfディレクトリの準備
--------------------

Symfonyには組み込みのエラー画面やデバッグツールバーがありますが、これら組み込み機能用のデザインファイルはプロジェクトのデザインファイルとは分離されています。
以下の操作を行って、組み込みのデザインが適用されるように準備してください。

### Linux環境
<pre class="command-line">
# sf_sandboxディレクトリにて
ln -s lib/vendor/symfony/data/web/sf web/
</pre>

### Windows環境
<pre class="command-line">
# sf_sandboxディレクトリにて
xcopy /E /F /Y lib\vendor\symfony\data\web\sf web\sf\

# エクスプローラでsfディレクトリをwebディレクトリへコピーしても構いません
</pre>



パーミッションの設定
--------------------

Linux環境の場合、`cache`ディレクトリと`log`ディレクトリにウェブサーバーのプロセスから書き込みができるように設定しておく必要があります。
Symfonyにはこれらのディレクトリのパーミッションを設定するタスクが用意されています。
コマンドプロンプトでプロジェクトのルートディレクトリへ移動し、以下のコマンドを実行してください。

<pre class="command-line">
php symfony project:permissions
</pre>



ブラウザから表示の確認
----------------------

さて、ここまで準備ができたらウェブブラウザからSymfonyのディレクトリにアクセスして、初期表示を確認しましょう。
sf_sandboxをローカル環境のドキュメントルート直下で展開した場合は、アクセスするURLは次のとおりです。

<pre class="command-line">
http://localhost/sf_sandbox/web/frontend_dev.php
</pre>

「Symfony Project Created」というような画面が表示されたでしょうか？このメッセージが表示されれば、まずはSymfonyを動作させる最低限の設定の完了です。

> **NOTE**
> お使いの環境の設定やサンドボックスパッケージを展開したディレクトリによっては上記のURLとは異なる場合があります。
> 重要な点は、`（プロジェクトルート）/web/frontend_dev.php`に対応するURLにアクセスするということです。



You are not allowed to access this file. Check frontend_dev.php for more information.
------------

Symfonyを設置した開発サーバーとは別のコンピュータからアクセスした場合、このような表示になります。
これは、公開サーバーで誤って開発用フロントコントローラーが閲覧可能になってしまうのを防ぐためのコードです。
もしこのようなメッセージが表示された場合は、`web/frontend_dev.php`ファイルを開き、以下の行をコメントアウトして下さい。

    [php]
    if (!in_array(@$_SERVER[''REMOTE_ADDR''], array(''127.0.0.1'', ''::1'')))
    {
        die(''You are not allowed to access this file. Check ''.basename(__FILE__).'' for more information.'');
    }
    



画面が真っ白になる
------------

この段階で画面が真っ白になって何も表示されない場合、`cache`ディレクトリ、または`log`ディレクトリのパーミッションが正しく設定されていない可能性があります。
ウェブサーバーのエラーログを確認してキャッシュに書き込めないというエラーが出ている場合は、パーミッションを設定し直して下さい。
