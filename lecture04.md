# 第4回授業課題

## 【課題】
- VPC作成
- EC2とRDSの構築
- EC2からRDSへの接続

<br>

### コスト管理
***
![01](/images-lecture04/budget.png)
  - VPC作成前に、コストを管理する為に閾値の設定を行った
    - 通知が来るように設定を行っている

<br>

### VPC作成
***
![02](/images-lecture04/VPC.png)

<br>

### EC2
***
![03](/images-lecture04/EC2-1.png)

![04](/images-lecture04/EC2-2.png)

<br>

### RDS
***
![05](/images-lecture04/RDS.png)

<br>

### セキュリティーグループ
***
#### EC2
![06](/images-lecture04/EC2-sg.png)
#### RDS
![07](/images-lecture04/RDS-sg-1.png)

![08](/images-lecture04/RDS-sg-2.png)

<br>

### EC2へのSSH接続
***
![09](/images-lecture04/EC2-access.png)
  - TeraTermを使用してアクセス

<br>

### EC2からRDSへの接続
***
- `sudo yum install mysql`コマンドにてMySQLをインストール

![10](/images-lecture04/RDS-access-1.png)


![11](/images-lecture04/RDS-access-2.png)
  - 下記を入力
  ```
  mysql -u ユーザー名 -p -h データベースのエンドポイント
  ```
  - 続けてパスワードを入力すると接続できる

<br>

## 【所感】
ES2にMySQLがインストールできず、解決するのに4時間ほどかかってしまった。

![12](/images-lecture04/EC2-miss.png)

EC2作成時に誤ってLinux 2023を選択してしまっており、SSH接続時の画面で気づくべきだった。再度Linux 2でインスタンスを作成し直すとすんなり接続することが出来て拍子抜けしてしまったが、「Linux 2023だから接続が出来ないのではないか？」という仮説が証明されたことは嬉しい（他に変更点はない為、恐らく合っている）。現在は無料利用枠を使用しているが、無料利用枠の中にも有料のサービスがあり、理解を深めることがコスト管理にも繋がると感じた。今後もサービスに関する学習を続けていきたい。