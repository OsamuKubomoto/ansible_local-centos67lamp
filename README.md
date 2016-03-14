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

プロジェクトディレクトリを作成＆移動

    $ mkdir example-project && cd example-project

Vagrantfileを作成

    $ vi Vagrantfile
    
    Vagrant.configure(2) do |config|
      config.vm.box = "bento/centos-6.7"
    
      if Vagrant.has_plugin?("vagrant-cachier")
        config.cache.scope = :box 
      end
    
      # config.vm.network "forwarded_port", guest: 80, host: 8080
      # config.vm.network "private_network", ip: "192.168.33.10"
      # config.vm.network "public_network"
    
      config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", mount_options: ['dmode=777','fmode=644']
    
      config.vm.provider "virtualbox" do |v|
        v.customize ['modifyvm', :id, '--paravirtprovider', 'kvm']
        v.linked_clone = true
      end
    
      config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "provision/site.yml"
      end
    
    end

git cloneしておく

    $ git clone https://github.com/OsamuKubomoto/centos67-lamp.git provision

/provision/group_vars/allを適宜修正してください。

仮想マシン起動

    $ vagrant up

2回目以降のプロビジョン実行

    $ vagrant provision

## Windows環境でのプロビジョン実行時のエラーについて

    There are errors in the configuration of this machine. Please fix
    the following errors and try again:
    
    ansible local provisioner:
    * `playbook` does not exist on the guest: C:/vagrant/provision/site.yml

windowsでプロビジョンを実行すると上記エラーが発生します。（2016年3月14日時点）
これはvagrant provision実行時のplaybookの指定パスが間違っているのが原因です。

× C:/vagrant/provision/site.yml
○ /vagrant/provision/site.yml

面倒ですが今後のアップデートで修正されるまでは下記コマンドで実行しましょう。

    vagrant ssh -c "cd /vagrant && ansible-playbook -c local provision/site.yml"

