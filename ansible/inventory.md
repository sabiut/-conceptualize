# Working with Ansible Inventories


## Introduction

Your company decided that their backup software license was frivolous and unnecessary. Because of this, the license was not renewed. As a stop-gap measure, your supervisor has created a simple script and an Ansible playbook to create an archive of select files, depending on pre-defined Ansible host groups. You will create the inventory file to complete the backup strategy.

## Solution

1.  Log in to the server using the provided lab credentials:
    
    `ssh ansible@<PUBLIC_IP_ADDRESS>`
    
2.  If you are logged in as `cloud_user`, switch to `ansible` using the same password provided for `cloud_user`:
    
    `su - ansible`
    

### Configure the `media` Host Group to Contain `media1` and `media2`

1.  Create the `inventory` file:
    
    `touch /home/ansible/inventory`
    
2.  Edit the `inventory` file:
    
    `vim /home/ansible/inventory`
    
3.  Paste in the following:
    
    `[media] media1 media2`
    
4.  To save and exit the file, press **ESC**, type `:wq`, and press **Enter**.
    

### Define Variables for `media` with Their Accompanying Values

1.  Create a `group_vars` directory:
    
    `mkdir group_vars`
    
2.  Move into the `group_vars` directory:
    
    `cd group_vars/`
    
3.  Create a `media` file:
    
    `touch media`
    
4.  Edit the `media` file:
    
    `vim media`
    
5.  Paste in the following:
    
    `media_content: /tmp/var/media/content/ media_index: /tmp/opt/media/mediaIndex`
    
6.  To save and exit the file, press **ESC**, type `:wq`, and press **Enter**.
    

### Configure the `webservers` Host Group to Contain the Hosts `web1` and `web2`

1.  Move into the home directory:
    
    `cd ~`
    
2.  Edit the `inventory` file:
    
    `vim inventory`
    
3.  Beneath `media2`, paste in the following:
    
    `[webservers] web1 web2`
    
4.  To save and exit the file, press **ESC**, type `:wq`, and press **Enter**.
    

### Define Variables for `webservers` with Their Accompanying Values

1.  Move into the `group_vars` directory:
    
    `cd group_vars/`
    
2.  Create a `webservers` file:
    
    `touch webservers`
    
3.  Edit the file:
    
    `vim webservers`
    
4.  Paste in the following:
    
    `httpd_webroot: /var/www/ httpd_config: /etc/httpd/`
    
5.  To save and exit the file, press **ESC**, type `:wq`, and press **Enter**.
    

### Define the `script_files` Variable for `web1` and Set Its Value to `/usr/local/scripts`

1.  Move into the home directory:
    
    `cd ~`
    
2.  Create a `host_vars` directory:
    
    `mkdir host_vars`
    
3.  Move into the `host_vars` directory:
    
    `cd host_vars/`
    
4.  Create a `web1` file:
    
    `touch web1`
    
5.  Edit the file:
    
    `vim web1`
    
6.  Paste in the following:
    
    `script_files: /tmp/usr/local/scripts`
    
7.  To save and exit the file, press **ESC**, type `:wq`, and press **Enter**.
    

## Testing

1.  Return to the home directory:
    
    `cd ~`
    
2.  Run the backup script:
    
    `/home/ansible/scripts/backup.sh`
    
    If you have correctly configured the inventory, it should not erro