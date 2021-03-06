################################
2.0.2から2.0.3へのアップグレード
################################

アップグレードの前には index.php
を静的ページと置き換えてサイトを停止してください。



ステップ 1: CodeIgniter ファイルの更新
======================================

"system" フォルダ内のすべてのファイルとディレクトリを置き換え、さらに
index.php ファイルを置き換えます。もし index.php
に変更を加えている場合、新しい index.php
に再度変更を加える必要があります。

.. note:: もし、これらのフォルダの中のファイルを更新している場合は、必ず最初にコピーを残しておいてください。



ステップ 2: メインの index.php ファイルの更新
=============================================

手を加えずに index.php を使用している場合は、古いバージョンのファイル
を新しいものに置き換えるだけです。

もし index.php ファイルに変更を加えている場合、新しいファイルに再度変
更を加える必要があります。



ステップ 3: config/user_agents.php の更新
=========================================

この設定ファイルに、たくさんのユーザエージェントクラスが追加されていま
すので、このファイルを application/config/user_agents.php
にコピーしてください。



ステップ 4: EXT 定数を ".php" に置換
====================================

.. note:: EXT 定数は廃止予定とされましたが、まだアプリケーションからは削除されていません。すぐに変更することを推奨します。



ステップ 5: autoload.php から APPPATH.'third_party' を削除
==========================================================

application/config/autoload.php を開いて、以下を探してください:


::

	$autoload['packages'] = array(APPPATH.'third_party');


もし何らかの追加パッケージを使用していなければ、その行は次のように変更
できます:

::

	$autoload['packages'] = array();


パッケージを自動読み込みしていない場合、これによりわずかに性能が向上し
ます。



セッション用のデータベーステーブルの更新
========================================

セッションクラスでデータベースを使用している場合、データベースの
ci_sessions テーブルを以下のように更新してください:


::

	
		CREATE INDEX last_activity_idx ON ci_sessions(last_activity);
		ALTER TABLE ci_sessions MODIFY user_agent VARCHAR(120);


