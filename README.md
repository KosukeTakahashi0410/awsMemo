## コマンドメモ

```
AWS 接続
ssh ec2-user@54.238.171.237 -i ~/.ssh/takahashikouske-key.pem
exit

ファイル送る
sftp -i ~/.ssh/takahashikouske-key.pem ec2-user@54.238.171.237
put <ファイル名>
quit

```

```
ビルド（プロダクション環境で）
yarn run build

（serveの追加）
yarn global add serve
もしかするとglobalが必要かも

（serveを使って起動）
serve -s build -p 3000
```

[無料で使えるAWSの初期トレーニングまとめ](https://techblog.nhn-techorus.com/archives/885)  
Adachiさんアドバイス -> 失敗から勉強していこう、そこから聞いたりなんだで勉強していこう！  

# awsMemo
端中さんアドバイス：あんまり一個一個に深入りしないでやっていった方がいいよ！  
ぽんぽんいこうや  

## AWSって何？
クラウドコンピューティングサービスのこと  
仮想の

- webサーバー
- ストレージ
- データベース

などを提供する

## EC2
**仮想サーバー**のこと  
**インスタンス**という単位で数えられる  
OSを乗っけてやる  
EC2とは・・・（ADACHI）  
サーバーでしかない、それ以上でもなければそれ以下でもない  
パソコン一台ごとでサーバーを立てると辛い  
PCを作る感じ  

#### EC2の取り扱い
インスタンス内に入るには

## VPC
virtual private cloudの略  
EC2同士で内部接続や、RDS（DB）とやりとりをするのでVPCを使う  
サブネットを置くことで実現する  
VPCとは・・・  
バーチャルのネットワーク周り  

## Subnet
VPCによって作られているCIDRブロックを分割したネットワーク郡  
直接外部ネットワークにつながっている**パブリックサブネット**  
直接外部ネットワークにつながっていない**プライベートサブネット**がある  
IPアドレスを割り当てることで、データ送信量をいじる  
* [サブネット (subnet)](https://wa3.i-3-i.info/word11973.html)
* [サブネットマスク (subnet mask)](https://wa3.i-3-i.info/word11975.html)
* [CIDR](https://wa3.i-3-i.info/word11989.html)


## CIDR
サイダーって読む  
IPアドレス（コンピュータ向けのネットワーク上の住所）  
IPアドレスは**どのネットワーク**と**どのコンピューター**というのが情報として分かれている  
**概念としてめっちゃむずい、後で確認！**\  

## SSHで接続するとき

```
chmod 600 ********.pem  
```

で鍵にアクセス制限をつけてあげないと動かせないので要注意（パーミッションエラー）  
chmodはぶっちゃけよくわからん  

## Nodeを入れよう
[AWS EC2でNodeを動作させる](https://qiita.com/oishihiroaki/items/bc663eb1282d87c46e97)
AWSでNodeを動作させるためにNodeをいれる  

## ルーティング

## S3とは
ファイル保存する（イメージでいうとファインダー）  
**静的ファイル(html,css,javascript)のみ**  
そこにホスティング(サーバー)機能がある  
EC2でホスティングをしなきゃいけないけど、それをいろいろ  
いろいろ設定がすっ飛ばせる  

## Spring bootでapplication.propertiesを環境に合わせるやつ
[Spring Bootでapplication.propertiesを環境ごとに切り替える方法](https://intellectual-curiosity.tokyo/2019/04/29/spring-boot%E3%81%A7application-properties%E3%82%92%E7%92%B0%E5%A2%83%E3%81%94%E3%81%A8%E3%81%AB%E5%88%87%E3%82%8A%E6%9B%BF%E3%81%88%E3%82%8B%E6%96%B9%E6%B3%95/)  
要は二つの環境のためにファイルを作ればいいってわけ  

## Spring bootをjarファイルにするやつ
[「Gradle」Spring Bootアプリケーションをビルドしてみる](http://a4dosanddos.hatenablog.com/entry/2018/12/01/115030)  

```
gradle bootjar
-> jarファイルを作る

java -jar ********.jar
-> jar起動
```

## apache使い方
[apacheの起動,停止,再起動に関するまとめ](https://qiita.com/rimoenic/items/81385e08cf772ae5cfe4)  
[AWSにApache入れて、ブラウザから「Public IP」にアクセスしたい。](https://qiita.com/mochizukikotaro/items/2fbaa492776840db05f8)  

```
sudo service httpd
```

の後にコマンドを入れてあげると動作するよ  

## linuxについて

```
sudo
-> 管理者権限で

yum
-> パッケージ管理ツール
```

* [【 sudo 】コマンド――スーパーユーザー（rootユーザー）の権限でコマンドを実行する](https://www.atmarkit.co.jp/ait/articles/1611/28/news036.html)
* [【yum入門】yumとは何か？Linuxにおけるyumとrpmの違い](https://uxmilk.jp/9715)

## create-react-appの環境変数を変える方法
[create-react-appで環境変数を設定したり切り替えたりする方法](https://sumii.io/posts/create-react-app-env-setup/)  
.env.productionと.env.developmentに分ける  

## react appをさっとデプロイする方法
[npmパッケージのserveで立てたローカルサーバーでReact Appを確認する方法](https://qiita.com/tktktktk/items/bd40409e84aaff1f43c5)  
[Amazon S3でSPAをサクッと公開する](https://qiita.com/kiyokiyo_kzsby/items/77bdb81a1ce1852b30ca)  
上のパケットポリシーまで  
わりとやることは単純

```
reactのビルド
yarn run build

ビルドしたファイル（/build以下）をS3に打ち込む
☆ここでS3直下にindex.htmlがないと404 Bad Requestになる

完成
```

* [VPCのネットワークまわりをもう一度（超優良記事、VPCがめっちゃわかりやすい）](https://qiita.com/ryosukes/items/9ad289e1d673899fc628)
* [AWSのVPCって何？メリットや使えるシーンなど徹底解説！](https://techplay.jp/column/541)
* [AWS のネットワーク設計入門](https://d1.awsstatic.com/events/jp/2017/summit/slide/D2T3-5.pdf)
* [[初心者向け]VPC作成からEC2インスタンス起動までを構成図見ながらやってみる（その1）](https://dev.classmethod.jp/articles/creation_vpc_ec2_for_beginner_1/)
* [[初心者向け]VPC作成からEC2インスタンス起動までを構成図見ながらやってみる（その２）](https://dev.classmethod.jp/articles/creation_vpc_ec2_for_beginner_2/)
* [0から始めるAWS入門①：VPC編](https://qiita.com/hiroshik1985/items/9de2dd02c9c2f6911f3b)
* [知識0から、AWSのEC2でウェブサーバーを構築するまで](https://qiita.com/shunsuke227ono/items/23dbf4f3bc663a2875f0)
* [AWS VPC環境構築](https://qiita.com/tanj/items/141311526d9ee19aa637)
* [AWS入門者向け 初心者が最初に理解すべきEC2とVPCの基本的な用語解説](https://avinton.com/academy/aws/)
* [AWS勉強 -VPC作成&サブネットに分割-https://qiita.com/KawamotoShuji/items/294768ae55fc9788b70a]()
* [【AWS】セキュリティグループを設定してみた（そして関連する用語を調べてみた）](https://qiita.com/noko_qii/items/d4c19ec5e891264af462)
* [サブネットの自動割り当て IP 設定 - EC2 VPC](https://qiita.com/leomaro7/items/924702bdb1e0701ec6db)
* [SSH鍵（秘密鍵）でログインした際のパーミッションエラーの解決方法](https://qiita.com/turmericN/items/9a1756e98c062bc81ef1)
* [AWS EC2作成からSSH接続](https://qiita.com/gurensouen/items/7382c2d14763436466d2#%E3%82%BF%E3%83%BC%E3%83%9F%E3%83%8A%E3%83%AB%E3%81%A7%E3%81%AE%E6%8E%A5%E7%B6%9A)
* [0から始めるAWS入門②：EC2編](https://qiita.com/hiroshik1985/items/f078a6a017d092a541cf#%E8%B5%B7%E5%8B%95%E3%81%AE%E5%89%8D%E3%81%AB%E5%85%AC%E9%96%8B%E9%8D%B5%E7%A7%98%E5%AF%86%E9%8D%B5%E3%81%AE%E8%A8%AD%E5%AE%9A)
* [EC2+RDS+Spring bootで簡単なAPIを作ってみる①](https://qiita.com/yseki_/items/81c84d78895b009c2aa6)
* [Amazon RDS for MySQLインスタンス作成手順](https://qiita.com/na0AaooQ/items/7c69a88c80f1efb4cad3)
* [AWSクラウド環境の構築からSpring Bootアプリのデプロイまで（初心者向け）](https://qiita.com/KevinFQ/items/119521ebd12bb7890761)
* [EC2+RDS+Spring bootで簡単なAPIを作ってみる①](https://qiita.com/yseki_/items/81c84d78895b009c2aa6)
* [AWSで基本的なサーバー環境を構築してみました。](https://qiita.com/President_Taka/items/a55c85996dd6a8a8bb4c)
* [見ながらやろう! AWSを始めよう -VPC構築編-](https://qiita.com/nago3/items/f5badeb4f7e5c32b0540)
* [Amazon RDS for MySQLインスタンス作成手順](https://qiita.com/na0AaooQ/items/7c69a88c80f1efb4cad3)
* [draw.ioでAWSのインフラ構成図を書く](https://qiita.com/nave-m/items/68425f476b254a1a47b0)
* []()
