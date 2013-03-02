Learning to Deploy a Static Site from Middleman

Development Environment
MacBook Pro
Mac OS X
10.7.5

Server Environment
Using Linode.com
Ubuntu
12.04 LTS 32-bit

Locally create, build, and deploy (http://middlemanapp.com/getting-started/)
1. $ gem install middleman
2. Navigate to new site folder
3. $ middleman init my_project
4. $ cd my_project
5. $ middleman server
6. Open browser to http://localhost:4567 # yup, that easy

Make it easy to login from the local machine
On the remote machine:
1. $ mkdir .ssh

On the local development machine:
1. $ cat ~/.ssh/id_dsa.pub | ssh <root>@<server> "cat - >> ~/.ssh/authorized_keys"
2. $ addgroup <developers.group>
3. $ adduser -ingroup <developers.group> <username>

Prepare the remote machine with nginx and vsftpd (https://help.ubuntu.com/10.04/serverguide/ftp-server.html)
1. $ sudo apt-get update
2. $ sudo apt-get upgrade -y
3. $ sudo apt-get install nginx
4. $ sudo apt-get install vsftpd # During installation, a user (ftp) is created with a home directory of /home/ftp (default FTP directory)
5. To change the location to /srv/ftp (for example)
   $ sudo mkdir /srv/ftp
   $ sudo usermode -d /srv/ftp ftp
   $ sudo /etc/init.d/vsftpd restart
6. To configure vsftpd to authenticate system users for upload, edit the /etc/vsftpd.conf file:
   -local_enable=YES
   -write_enable=YES
   $ sudo /etc/init.d/vsftpd restart
7. Build or Deploy! (https://github.com/tvaughan/middleman-deploy/)
$ middleman build [--clean]
$ middleman deploy [--clean]