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

�_�E�����[�h����

    $ git clone https://github.com/OsamuKubomoto/ansible_local-centos67lamp.git test-ansible-local

/provision/group_vars/all��K�X�C�����Ă��������B

���z�}�V���N�����v���r�W����

    $ cd test-ansible-local
    $ vagrant up

2��ڈȍ~�̃v���r�W�������s

    $ vagrant provision

�� windows�Ńv���r�W���������s����Ə�L�G���[���������܂��i2016�N3��14�����_�j�B�ʓ|�ł�������̃A�b�v�f�[�g�ŏC�������܂ł͉��L�R�}���h�Ŏ��s���܂��傤�B

    vagrant ssh -c "cd /vagrant && ansible-playbook -c local provision/site.yml"

