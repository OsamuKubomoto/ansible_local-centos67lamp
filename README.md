# README

ansible_localを使ってプロビジョニングするplaybookを作りました。

## 開発環境

VirtualBox5.0.22
Vagrant1.8.4

### OSとミドルウェアのバージョン ※2016-11-14時点

 * centos 6.7
 * Apache 2.2.15
 * PHP 5.6.28
 * mysql 5.5.53
 * nodejs v0.10.46
 * npm 1.3.6
 * bower 1.8.0
 * Composer 1.2.2


## 構築手順

ダウンロードする

    $ git clone https://github.com/OsamuKubomoto/ansible_local-centos67lamp.git test-ansible-local

/Vagrantfileと/provision/group_vars/allを適宜修正してください。


ゲストOSを起動

    $ cd test-ansible-local
    $ vagrant up

初回起動時、下記のように共有フォルダのマウントでエラーが起きる場合は、以下の手順で進めます。

    ==> default: Mounting shared folders...
        default: /vagrant => path/to/test-ansible-local
    
    Failed to mount folders in Linux guest. This is usually because
    the "vboxsf" file system is not available. Please verify that
    the guest additions are properly installed in the guest and
    can work properly. The command attempted was:
    
    mount -t vboxsf -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3`,dmode=777,fmode=777 vagrant /vagrant
    mount -t vboxsf -o uid=`id -u vagrant`,gid=`id -g vagrant`,dmode=777,fmode=777 vagrant /vagrant
    
    The error output from the last command was:
    
    /sbin/mount.vboxsf: mounting failed with the error: No such device

ゲストOSのカーネルをアップデートします。

    $ vagrant ssh -c "sudo yum update -y kernel"

ゲストOSを再起動

    $ vagrant reload

たまに回線の状態によってはyumリポジトリのダウンロードに失敗して処理が中断されることがあるので、その場合は手動でプロビジョニングを再実行する。

    $ vagrant provision

