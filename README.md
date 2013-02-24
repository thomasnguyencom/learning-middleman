Learning to Deploy a Static Site from Middleman

Development Environment
MacBook Pro
Mac OS X
10.7.5

Server Environment
Using Linode.com
Ubuntu
12.04 LTS 32-bit

Start Here:
http://middlemanapp.com/getting-started/

Locally create, build, and deploy
1. ~ gem install middleman
2. Navigate to new site folder
3. ~ middleman init my_project
4. ~ cd my_project
5. ~ middleman server
6. Open browser to http://localhost:4567 # yup, that easy

Make it easy to login from the local machine
On the remote machine:
1. ~ mkdir .ssh

On the local development machine:
1. ~ cat ~/.ssh/id_dsa.pub | ssh <root>@<server> "cat - >> ~/.ssh/authorized_keys"
2. ~ addgroup developers
3. ~ adduser -ingroup developers <username>

Prepare the remote machine
1. ~ apt-get update
2. ~ apt-get upgrade -y
3. ~ apt-get install nginx

Now, build locally and copy to the remote nginx server
1. ~ cd my_project
2. ~ bundle exec middleman build
3. ~ scp -r build <root>@<server>:/usr/share/nginx/

Configure/Start up the nginx server
1. ~ cd /etc/nginx/sites-available (/etc/nginx/sites-enabled)
2. By default, nginx will use the "default" file which points to the /usr/share/nginx/www folder. Change the reference to /usr/share/nginx/build
3. ~ service nginx start
4. Open browser to http://<server> # yup, that easy