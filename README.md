# README

ansible_localを使ってプロビジョニングするplaybookを作りました。

[2016-05-05追記]
vagrant1.8.1でansible_localを利用するとエラーが発生します。
v1.8.2で修正されるまでは手動でプロビジョン実行する前提とします。


## 開発環境

VirtualBox5.0.20
Vagrant1.8.1

### OSとミドルウェアのバージョン ※2016-05-05時点

 * centos 6.7 (bento/centos-6.7 2.2.6)
 * Apache 2.2.15
 * PHP 5.6.21
 * mysql 5.5.49
 * nodejs v0.10.42
 * npm 1.3.6
 * bower 1.7.9
 * Composer 1.0.3


## 構築手順

ダウンロードする

    $ git clone https://github.com/OsamuKubomoto/ansible_local-centos67lamp.git test-ansible-local

/provision/group_vars/allを適宜修正してください。

仮想マシン起動＆プロビジョン

    $ cd test-ansible-local
    $ vagrant up
    $ vagrant ssh -c "cd /vagrant && ansible-playbook -c local provision/site.yml"

