# 第3回授業課題

## 【課題】
- サンプルアプリケーションのデプロイ
- APサーバーについて調べる
- DBサーバーについて調べる

<br>

## 【課題詳細】
### -  サンプルアプリケーションのデプロイ  -
![01](/images-lecture03/2023-12-04_234104.png)

![02](/images-lecture03/2023-12-04_234132.png)

ブラウザでのアクセスに成功。

<br>

***
#### 実際に行った手順＆学んだこと
***
- `ruby -v`でRubyのバージョン確認を行う
- コマンドの一覧は`ruby -h`（より詳細は`ruby --help`）で確認が出来る
   - `rvm install -v`では**Ruby Version Manager**のバージョン確認が可能
   - **RVM**（Ruby Version Manager）とは
     - 同じデバイスに複数インストールされたRubyを管理するよう設計されたオペレーティングシステム
    
- 指定されたRubyのバージョンを`rvm install 3.1.2`にてインストール
- `rvm use 3.1.2`で使用したいバージョンへの切替が出来る
   - `rvm list`でも、インストールされているRubyの確認と、どのバージョンが適用されているかを確認することが出来る
   
   ![03](/images-lecture03/2023-12-04_161620.png)
   - **ruby-3.1.2**が適用されていることがわかる
   
- `docker system prune -a`を入力し、未使用データの削除を行う **《容量の確保》**
   - **Are you sure you want to continue? [y/n]** の横に`y（yesの意）`を入力
   - **Docker**とは
     - ひとつのOSに対して多数のアプリケーション実行環境（開発環境）を構築可能
     - AWSではDockerのオープンソリューションと商用ソリューションの両方がサポートされている
   
- 下記コマンドにてMariaDBを削除して**MySQL8.0**をインストールする
  ``` 
  curl -fsSL https://raw.githubusercontent.com/MasatoshiMizumoto/raisetech_documents/main/aws/scripts/mysql_amazon_linux_2.sh | sh
  ```
   - **Curlコマンド**とは
     - 様々なオプションを指定することで、データ取得時の条件や、取得する情報を変えることが出来る
   - **MySQL**とは
     - Webアプリケーション開発でよく使われるデータベースシステム
    
- 下記コマンドにてMySQLの初期パスワードを確認する
  ```
  sudo cat /var/log/mysqld.log | grep "temporary password" | awk '{print $13}'
  ```
   - **sudoコマンド**とは
     - 一般ユーザーがソフトをインストールしたり、ソフトを実行したりする場合、Linuxではsudoを一番始めに宣言して使用する
     - 宣言することで管理者権限で実行することが可能となる

- `mysql -u root -p`を入力し、Enter passwordに初期パスワードを入力してログインする
- 下記で初期パスワードの変更を行う
  ```
  ALTER USER 'root'@'localhost' IDENTIFIED BY '設定するパスワード';
  ```
   - 「設定するパスワード」の文字を消し、任意のパスワードを新しく入力する
   - 実行したら`FLUSH PRIVILEGES;`を入力することで、変更が有効になる
   - ログアウトする場合は`exit`を入力する
   - MySQLのコマンドキャンセルは`\c`で可能
   - もう一度`mysql -u root -p`でログインを行い、パスワードが変更されていることを確認しログアウトする

- `cd raisetech-live8-sample-app`でディレクトリの移動を行う
- 「database.yml.sample」ファイルのコピーを下記コマンドで行う
   ```
   cp config/database.yml.sample config/database.yml
   ```
   - 「config」フォルダ内の「database.yml.sample」ファイルが、「config」フォルダ内に「**database.yml**」というファイル名でコピーされる
   - **YML**とは
     - YAML Ain’t Markup Languageの略称
     - XMLやJSONのような人間が読めるデータシリアライズ言語のひとつ
     - 他の言語と比較しても軽量で比較的わかりやすいため、読みやすいとされている
   
- コピーしたファイル内にある「password」欄に設定した新しいパスワードを入力する
- MySQLの設定
  - `my.cnf`というファイルに対して行う
  - `/etc/my.cnf`はグローバルオプションファイル
  - `cat /etc/my.cnf`で上記のファイル内容が表示される
  - **catコマンド**とは
    - 「連結する」を意味するconcatenateが名前の由来
    - ファイルの内容を連結して標準出力に出力するコマンド
    - 単一のファイル内容を表示するために使用されることが多い
- `socket=/var/lib/mysql/mysql.sock`のスラッシュ以下をコピー
  - 「database.yml」ファイル内にある「socket」の内容を書き換える（2箇所）
  - **socket**とは
    - プログラムとネットワークをつなげる接続口のこと
    
- `bin/setup`で**環境構築**を行う
  - バージョン`2.3.14`の**Bundler**がインストールされていることが確認できる
  - **Bundler**とは
    - gemのバージョン管理やgemの依存関係を管理してくれるgemのこと
  - **gem**とは
    - gem形式にパッケージングされたRuby言語用の外部ライブラリ
  - **ライブラリ**とは
    - 汎用性の高い機能を他のプログラムで呼び出して使えるように部品化して集めたファイルのこと
    
- `node -v`でNodeのバージョン確認をする
- 指定のバージョンを`nvm install 17.9.1`でインストールする
  - **NVM**（Node Version Manager）とは
    - Node.jsのバージョン管理を行うためのソフトウェアツール
  - **Node.js**とは
    - JavaScriptをサーバー側で動作させるプラットフォーム
    
- `nvm use 17.9.1`で使用するバージョンを切り替える
- `npm install -g yarn`でyarnをインストールする
  - **NPM**（Node Package Manager）とは
    - 主にJavaScriptで開発されたプラグラム部品（モジュール）を管理するためのパッケージ管理システムの一つ
  - **Yarn**とは
    - JavaScriptをサーバーサイドで動かすための実行エンジンである「Node.js」上で動作するパッケージマネージャーの一つ
    - npmより高速で、並列インストールをサポートし、パッケージのインストール速度を向上させる
  - 「npm install -g yarn」の「**-g**」
    - インストール先がグローバル。デフォルトはローカル
    - rootが所有する{prefix}/lib/node_modules/にパッケージがインストールされる
   
- `yarn -v`でバージョンの確認をし、問題がなければもう一度`bin/setup`を行う
- `bin/cloud9_dev`でアプリケーションの起動をする
    
    **⇒ アクセスの権限がない（実行ができない）ため拒否される**
- `ls -la bin`でbinディレクトリ内すべてのファイルやディレクトリを詳細な情報と共に表示し、隠しファイルも含めて表示する
  - パーミッション情報を確認する
  - cloud9_devは`-rw-rw-r--`となっており、アクセス権限がないことがわかる
  - パーミッション情報は、1桁目がファイル情報で、「d」であればディレクトリ、「-」であればファイルを意味する
  - 1桁目以降は、3文字1セットで、左から「所有者」「グループ」「その他のユーザー」を表す
  - パーミッションの有効無効は0～7の数値で表す  
    
     | アクセス権 | 数値| 説明 |
     |:---|:---|:---|
     | --- | 0 | 読み込み書き込み不可 |
     | --x | 1 | 実行のみ |
     | -w- | 2 | 書き込みのみ |
     | -wx | 3 | 書き込み実行のみ |
     | r-- | 4 | 読み込みのみ |
     | r-x | 5 | 読み込み実行のみ |
     | rw- | 6 | 読み込み書き込みのみ |
     | rwx | 7 | 読み込み書き込み実行ができる |


- `sudo chmod 775 bin/cloud9_dev`でcloud9_devのアクセス権限を変更する
   - 上図の数値を元に変更
   - `ls -la bin`で権限が変更されているかを確認する
   - `-rwxr-xr-x`となっていた為、「755」で変更が適用されていることがわかる
- `bin/cloud9_dev`で再度アプリケーションの起動をする
- **Block host**と表示された為、`Ctrl＋C`でアプリケーションを停止する
- 「config」フォルダ ⇒「environments」フォルダ内にある「**development.rb**」ファイルを開く
-  Block hostの画面に表示されている下記を「development.rb」ファイルの一番下にペーストする
   - config.hosts << "9946160ad4a34eef9979c3602ca44997.vfs.cloud9.ap-northeast-1.amazonaws.com"
　

   ![04](/images-lecture03/2023-12-04_234356.png)
   - `config.hosts <<`も入力しなければ起動しない
   - `end`がきちんと反映されていないと起動しない ⇒ `syntax error`が表示された
    
- `bin/cloud9_dev`で再度アプリケーションの起動をする
   - 起動に成功
   - 動作確認も完了

<br>

### -  APサーバーについて調べる  -

 - Railsを動かすためのサーバー（Railsのバージョンは**7.0.4**）
 - **Puma version 5.6.5**を使用
   
   ![05](/images-lecture03/2023-12-04_235002.png)
 - サーバーを`Ctrl＋C`で停止させた後、引き続きアクセスは出来ない
   
   ![06](images-lecture03/2023-12-04_235116.png)
 - `rails s`でアプリケーションサーバーを再起動すると再びアクセスが可能

<br>

### -  DBサーバーについて調べる  -

 - **MySQL version 8.0.35**を使用
 - バージョンの確認はMySQLログイン時、またはログインしてからのコマンドで確認が出来る
 
   ![07](/images-lecture03/2023-12-05_004744.png)

   ![08](/images-lecture03/2023-12-05_004942.png)
   
 - サーバーを終了させた後、`rails s`を入力しても引き続きアクセスは出来ない
 
   ![09](/images-lecture03/2023-12-05_001344.png)

   ![10](/images-lecture03/2023-12-05_000638.png)
 
 - 再起動をすると`active（running）`になりアクセスが可能になる
 
   ![11](/images-lecture03/2023-12-05_000853.png)

   ![12](/images-lecture03/2023-12-05_001249.png)

<br>

## 【所感】
工程が上手く理解できず、課題を進めるのに非常に時間が掛かった。

それぞれが互いにどのように作用しているか等、一度実践しただけではわからなかった。

今回こうして作業内容を整理し直すことで、それでもまだ不十分であるとは思うが、理解に繋がったように思う。

「簡単なアプリケーション」と聞いていたが、起動時の動作が単純なアプリケーションでも初学者の自分には複雑だった。

実際の業務となると、もっと難解な作業になるのだろうがまったく想像がつかない。

これからも根気よく理解を深めていきたい。