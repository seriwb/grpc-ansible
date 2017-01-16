# grpc-sample

CentOS 7の仮想OS上に、gRPCを利用した開発環境を構築するプロジェクトです。  
本プロジェクトは以下を利用します。

- Vagrant
- Ansible


## 動作説明

Provisioningで以下のAnsible Playbookが実行されます。  
※ホストOSにAnsibleは不要です。  

    grpc-sample/ansible/local.yml

開発用のリポジトリは、以下のディレクトリに配置することを想定しています。

    grpc-sample/repositories


## 実行要件

ホストOSには40GB以上のディスク領域が必要です。
- https://atlas.hashicorp.com/centos/boxes/7

以下のソフトウェアとVagrantのプラグインをホストOSにインストールしてください。

### ソフトウェア

- Vagrant 1.8.7
- VirtualBox 5.0.X

### Vagrantプラグイン

- vagrant-vbguest
- vagrant-reload

Vagrantプラグインのインストール手順は以下になります。

```
$ vagrant plugin install <プラグイン名>
```


## 実行手順

ホストOSのコンソールで、以下のコマンドを実行してください。  

    $ vagrant up

rsyncの自動同期を行う場合は、ゲストOS起動後に以下のコマンドをホストOSで実行してください。

    $ vagrant rsync-auto


### 実行時間

すべてのタスクが完了するまで、約1時間ほどかかります。  


# Ansible Playbook

本プロジェクトで利用するAnsibleのPlaybookです。

    grpc-sample/ansible


## 実行要求

Vagrant以外から実行する場合は、実行環境にAnsible 2.2.0+ をインストールしてください。


## 開発環境構築の手動実行方法

開発環境のサーバに```grpc-sample/ansible```をコピーし、当該ディレクトリ上で以下のコマンドを実行してください。

    ansible-playbook -i local local.yml

※SSHのagent forwardingを使ってgit cloneしているので、GitHubの秘密鍵がssh-addで登録されている必要があります。
vagrant sshしてからansible-playbookコマンドを叩く場合も、ホストOS側で事前にssh-addの実行をお願いします。


## 環境の説明

Playbookの実行により、以下がCentOS 7上に構築されます。

### ミドルウェア

- git 2.11.0
- gRPC(protocol-buffer)
- go 1.7.4
- ruby 2.4.0
- node.js 7.4.0
- php 7.0.14
- phalcon 3.0.3


### nginx

#### SSLの秘密鍵、証明書について

Ansibleは、本番環境で利用するSSLの秘密鍵、証明書を作成・配置を行いません。
必要に応じて`{{ nginx_conf_dir }}/ssl`ディレクトリ配下にファイルを配置してください。

開発環境構築用のPlaybookを利用した場合は、
以下の手順で作成された秘密鍵、証明書が上記ディレクトリに配置されます。

```
$ openssl genrsa 2048 > server.key
$ openssl req -new -key server.key > server.csr
（問い合わせに対しては全てEnterのみ）
$ openssl x509 -days 3650 -req -signkey server.key < server.csr > server.crt
```