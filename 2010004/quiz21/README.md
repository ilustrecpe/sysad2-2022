### HOW TO CREATE AN ANSIBLE CONFIGURATION ###

1. Before creating an ansible configuration ensure that you have python, ansible, nano/vim, and
pip installed. To install pip you need to do apk add curl first then pass the command
curl https: //bootstrap.pypa.io/get-pip.py -o get-pip.py followed by python3 get-pip.py
--user

   This can be done by passing in the command apk add python3, apk add ansible.If Alpine
Linux returned an error you should edit using vim or nano the repositories which is usually located
in /root/etc/apk, from /root/etc/apk uncomment the community repo, save and then run
the aforementioned commands again. For further inquiries check the ansibile documentation
of how to install ansible.

2. Check if you have python and ansible installed, to check if ansible is properly installed
type ansible --version, for python its python3 --version, also install nano or vim.

3. To create an ansible configuration create a fresh configuration file first by
passing the command touch config.cfg, after creation pass in the command nano
config.cfg or vim config.cfg, initially this file is empty
before we proceed with passing changes type [defaults] first in the first line.
next we should populate it with parameters that we wish to set, in my case since my managed nodes have
unique IP address i passed in an inventory file in my local directory to an inventory
parameter, i did this by passing the command inventory=[inventory file name], and then
host_key_checking as false since I used ssh for my inventory, i did this by passing
the command HOST_KEY_CHECKING = False. To view the list of parameters that can be
edited in the configuration file check the ansible configuration settings in the
ansible documentation.

4. Save your work, in nano you nood to do the keyboard combination control+x save
then press enter. In vim press esc then type :wq. 

### HOW TO CREATE AN ANSIBLE INVENTORY ###

1. If you are using a virtualbox to create your control node and managed nodes
I would suggest changing the network settings to 
a NatNetwork and pass in your custom network address, this can be done by navigating
to your virtual machine > tools> preferences > network, select NatNetwork,
input your desired network address, mac address, and network name. After doing so,
we need to change the network settings of our control node and managed nodes, again
navigate to your virtualbox manager select your control node and managed nodes
respectively, settings > network, under attached to select NAT NETWORK and then select
the NatNetwork that you created.

2. Launch your control node and managed node, pass in the command ifconfig -a
under eth0 it should be in the same format as the network address we configured in
the virtualbox.

3. To create an Ansible inventory ensure that you have ansible, python, pip, nano/vim,
installed, refer to the post above if you haven't configured this yet.

4. pass in the command touch inventory and use nano to edit.

5. Initially this inventory file is empty, an inventory file accoridng to the ansible
documentation contains the IP address of your managed hosts, to do this we need to
pass in the name of our first managed hosts followed by the IP address of that
managed host, this can be any name. this can be done
by first typping [hostname] then on the next line followed by their IP address.

6. Next we need to pass in variables that ansible will use as credentials when
accessing that managed node, on the next line type [hostname: vars] (hostname is the
name of the managed host) then on the next line followed by ansible_ssh_user=
[managed host username when entering vm] lastly on the next line ansible_ssh_pass=
[managed host password when entring vm]

7. If done correctly this should update ansible of the list of managed hosts.

### HOW TO CREATE AN AD-HOC ANSIBLE COMMAND WITH SETUP AND SHELL MODULE ###

1. AD-HOC commands are commands that can be typed manually by first invoking the name
ansible followed by the target host, -m, then the module we would like to use
followed by module options which are arguments inside the module.

2. To use AD-hoc commands using the ansible builtin setup it is suggested that you
create a playbook yaml file for this, inside the playbook pass in the name, hosts, and then
most importantly pass in the command ansible.builtin.setup to use the setup module, then
followed by the ad-hoc command we would like to perform.

3. Same with step#3 the only difference is that instead of ansible.builtin.setup we
pass the command ansible.builtin.shell
