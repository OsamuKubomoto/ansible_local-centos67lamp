# README

ansible_local���g���ăv���r�W���j���O����playbook�����܂����B

## �J����

VirtualBox5.0.16
Vagrant1.8.1

### OS�ƃ~�h���E�F�A�̃o�[�W���� ��2016-02-04���_

 * centos 6.7
 * Apache 2.2.15
 * PHP 5.4.45
 * mysql 5.5.48
 * nodejs v0.10.42
 * npm 1.3.6
 * bower 1.7.7
 * Composer 1.0-dev


## �\�z�菇

�v���W�F�N�g�f�B���N�g�����쐬���ړ�

    $ mkdir example-project && cd example-project

Vagrantfile���쐬

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

git clone���Ă���

    $ git clone https://github.com/OsamuKubomoto/centos67-lamp.git provision

/provision/group_vars/all��K�X�C�����Ă��������B

���z�}�V���N��

    $ vagrant up

2��ڈȍ~�̃v���r�W�������s

    $ vagrant provision

## Windows���ł̃v���r�W�������s���̃G���[�ɂ���

    There are errors in the configuration of this machine. Please fix
    the following errors and try again:
    
    ansible local provisioner:
    * `playbook` does not exist on the guest: C:/vagrant/provision/site.yml

windows�Ńv���r�W���������s����Ə�L�G���[���������܂��B�i2016�N3��14�����_�j
�����vagrant provision���s����playbook�̎w��p�X���Ԉ���Ă���̂������ł��B

�~ C:/vagrant/provision/site.yml
�� /vagrant/provision/site.yml

�ʓ|�ł�������̃A�b�v�f�[�g�ŏC�������܂ł͉��L�R�}���h�Ŏ��s���܂��傤�B

    vagrant ssh -c "cd /vagrant && ansible-playbook -c local provision/site.yml"

