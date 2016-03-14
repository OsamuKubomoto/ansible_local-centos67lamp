# README

ansible_localを使ってプロビジョニングするplaybookを作りました。

## 開発環境

VirtualBox5.0.16
Vagrant1.8.1

### OSとミドルウェアのバージョン ※2016-02-04時点

 * centos 6.7
 * Apache 2.2.15
 * PHP 5.4.45
 * mysql 5.5.48
 * nodejs v0.10.42
 * npm 1.3.6
 * bower 1.7.7
 * Composer 1.0-dev


## 構築手順

ダウンロードする

    $ git clone https://github.com/OsamuKubomoto/ansible_local-centos67lamp.git test-ansible-local

/provision/group_vars/allを適宜修正してください。

仮想マシン起動＆プロビジョン

    $ cd test-ansible-local
    $ vagrant up

2回目以降のプロビジョン実行

    $ vagrant provision

※ windowsでプロビジョンを実行すると上記エラーが発生します（2016年3月14日時点）。面倒ですが今後のアップデートで修正されるまでは下記コマンドで実行しましょう。

    vagrant ssh -c "cd /vagrant && ansible-playbook -c local provision/site.yml"

