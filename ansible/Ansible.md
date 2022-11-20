## Install Ansible on the Control Host

Log in to the Control Host server using `ssh`, `cloud_user`, and the provided Public IP address and password:

`ssh cloud_user@<PUBLIC IP>`

Install `epel-release` and enter `y` when prompted:

`sudo yum install epel-release`

Install Ansible and enter `y` when prompted:

`sudo yum install ansible`

## Create an `ansible` User

Now, we need to create the `ansible` user on both the control host and workstation host.

On the control node:

`sudo useradd ansible`

Connect to the workstation node using the provided password:

`ssh workstation`

Add the `ansible` user to the workstation and set a password for the `ansible` user. We need to make sure it is something we will remember:

`sudo useradd ansible sudo passwd ansible logout`

## Configure a Pre-Shared Key for Ansible

With our user created, we need to create a pre-shared key that allows the user to log in from `control` to `workstation` without a password.

Change to the `ansible` user:

`sudo su - ansible`

Generate a new SSH key, accepting the default settings when prompted:

`ssh-keygen`

Copy the SSH key to `workstation`, providing the password we created earlier:

`ssh-copy-id workstation`

Test that we no longer need a password to log in to the `workstation`:

`ssh workstation`

Once we succeed at logging in, log out of `workstation`:

`logout`

## Configure the Ansible User on the Workstation Host

Our next job is to configure the `ansible` user on the workstation host so that that they may `sudo` without a password.

Log in to the workstation host as `cloud_user` using the password provided by the lab:

`ssh cloud_user@workstation`

Edit the `sudoers` file:

`sudo visudo`

Add this line at the end of the file:

`ansible ALL=(ALL) NOPASSWD: ALL`

Save the file:

`:wq`

Log out of `workstation`:

`logout`

## Create a Simple Inventory

Next, we need to create a simple inventory, `/home/ansible/inventory`, consisting of only the `workstation` host.

On the `control` host, as the `ansible` user, run the following commands:

`vim /home/ansible/inventory`

Add the text "workstation" to the file and save using `:wq` in `vim`.

## Write an Ansible Playbook

We need to write an Ansible playbook into `/home/ansible/git-setup.yml` on the control node that installs `git` on `workstation`, then executes the playbook.

On the control host, as the `ansible` user, create an Ansible playbook:

`vim /home/ansible/git-setup.yml`

Add the following text to the file:

`--- # install git on target host - hosts: workstation become: yes tasks: - name: install git yum: name: git state: latest`

Save and exit the file (`:wq` in vim).

Run the playbook:

`ansible-playbook -i /home/ansible/inventory /home/ansible/git-setup.yml`

Verify that the playbook ran successfully:

`ssh workstation which git`

# Lab2

## Install Ansible on the Control Node

Log in to the control node using `ssh`, `cloud_user`, and the provided public IP address and password:

`ssh cloud_user@<PUBLIC IP>`

To install Ansible on the control node:

`sudo yum install ansible`

## Configure the `ansible` User on the Control Node

Next, we'll configure the `ansible` user on the control node for ssh shared key access to managed nodes.

**Note:** Do not use a passphrase for the key pair.

Create a key pair for the `ansible` user on the control host, accepting the defaults when prompted:

`sudo su - ansible ssh-keygen`

Copy the public key to both `node1` and `node2`:

`ssh-copy-id node1 ssh-copy-id node2`

## Create a Simple Ansible Inventory

Next, we'll create a simple Ansible inventory on the control node in `/home/ansible/inventory` containing `node1` and `node2`.

On the control host:

`sudo su - ansible touch /home/ansible/inventory echo "node1" >> /home/ansible/inventory echo "node2" >> /home/ansible/inventory`

## Configure `sudo` Access for Ansible

Now, we'll configure sudo access for Ansible on `node1` and `node2` such that Ansible may use sudo for any command with no password prompt.

Log in to `node1` as `cloud_user` and edit the `sudoers` file to contain appropriate access for the `ansible` user:

`ssh cloud_user@node1 sudo visudo`

Add the following line to the file and save:

`ansible ALL=(ALL) NOPASSWD: ALL`

Enter:

`logout`

Repeat these steps for `node2`, and then back out to the control node.

## Verify Each Managed Node Is Accessible

Finally, we'll verify each managed node is able to be accessed by Ansible from the control node using the `ping` module.

Redirect the output of a successful command to `/home/ansible/output`.

To verify each node, run the following as the `ansible` user from the control host:

`ansible -i /home/ansible/inventory node1 -m ping ansible -i /home/ansible/inventory node2 -m ping`

To redirect output of a successful command to `/home/ansible/output`:

`ansible -i /home/ansible/inventory node1 -m ping > /home/ansible/output`