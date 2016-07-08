# FreeNAS 9.10 Vagrant Box
Source files to build a FreeNAS 9.10 Vagrant box

This box is distributed to Atlas, please use vagrant directly to install it:
    vagrant init drajen/freenas9 && vagrant up

If you want to build your own custom box for the vagrant virtualbox provider, please follow these instructions:

Download an .iso from http://download.freenas.org/
git clone this repo:

    git clone https://github.com/drajen/freenas-vagrant

Untar'gz the template:

    tar xzvf freenas-template.tar.gz

Register the vbox and attach the .iso via the UI:

    vboxmanage registervm $(pwd)/freenas-template/freenas-template.vbox

Answer all the prompts and set the root password to 'root'
Power the machine off and unregister the VM: (before this step it could be useful to snapshot the machine to get back to this known state quickly)

    vboxmanage controlvm $(pwd)/freenas-template/freenas-template.vbox
    vboxmanage unregistervm $(pwd)/freenas-template/freenas-template.vbox

Use Ansible to prep the box:

    ansible-playbook -i inventory.ini prep.yml

There should now be a file called 'package.box' in `pwd` after the playbook finishes

# Known issues
All quirks are documented on Atlas in the release notes of [drajen/freenas9](https://atlas.hashicorp.com/drajen/boxes/freenas9).
