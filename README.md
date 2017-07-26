# udacity-linux-server-config

SSH IP : 52.58.237.3 (Static IP) <br>
SSH Port: 2200 (Changed from 22)<br>
URL to App: http://52.58.237.3 <br>
Your Keyfile for SSH -->: https://github.com/davidduckwitz/udacity-linux-server-config/blob/master/key.pem<br>
Created Putty-Key-File->: https://github.com/davidduckwitz/udacity-linux-server-config/blob/master/putty-key.ppk<br>

# Use Amazon Lightsail Server to serve Catalog Script
You can use a "Amazon Lightsail Server" to serve your APP. It's easy and realy cheap (First Month FREE / then 5$ / Month)<br>
1. Create Account / Login to: https://lightsail.aws.amazon.com/ls/webapp/home <br>
2. Create a new Instance<br>
--> Choose location of your Amazon-Server (In my case 'Frankfurt / Europe')<br>
--> Name your instance (e.g. My Catalog-App-Server)<br>
--> Download your SSH-Keyfile to login with SSH from Accountpage: https://lightsail.aws.amazon.com/ls/webapp/account <br>
--> Once you are in the accounts page, there is an option to download the default private key.

<p>To see if you can login into instance. Two things need to be done:</p>
<ol>
<li>
<p>You need to change permission of the downloaded lightsail private key.
<code>chmod 400 LightsailDefaultPrivateKey.pem</code> or <code>chmod 600 LightsailDefaultPrivateKey.pem</code></p>
</li>
<li>
<p>To login:
<code>ssh user@PublicIP -i LightsailDefaultPrivateKey</code></p>
</li>
</ol>
<p><strong>Please make sure your private key is the same directory. The default port for SSH is 22 (We will change that later to 2200)</strong>
4. Connect to your Instance with the big Orange Button (Connect using SSH)<br>
5. Update System & create a new user named 'grader'<br>
<p>Once you are able to access the instance, lets update our system and then create our new user.</p>
<h2><a id="user-content-updating-the-server" class="anchor" href="#updating-the-server" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Updating the server</h2>
<p>Since you are running ubuntu, its only two commands:</p>
<pre><code>sudo apt-get update
sudo apt-get upgrade
</code></pre>
<h2><a id="user-content-creating-the-new-user-with-sudo-permissions" class="anchor" href="#creating-the-new-user-with-sudo-permissions" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Creating the New user with sudo permissions</h2>
<p>You are login into the instance. Lets create a new user called grader:</p>
<pre><code>sudo adduser grader
</code></pre>
<p>It will prompt for a password. Add any password to that field.
After the user gets created, run this command to give the grader sudo priviledges:</p>
<pre><code>sudo visudo
</code></pre>
<p>Once your in the visudo file, go to the section user privilege specification</p>
<pre><code>root    ALL=(ALL:ALL) ALL
</code></pre>
<p>You've noticed the root user in the file. You need add the grader user to same section.  It should look like this:</p>
<pre><code>grader  ALL=(ALL:ALL) ALL
</code></pre>
<p>If you want to login into the account, check to see if works: <code>sudo login grader</code>.
We've created our new user, lets configure our ssh to non-default port</p>
<h2><a id="user-content-configuring-ssh-to-a-non-default-port" class="anchor" href="#configuring-ssh-to-a-non-default-port" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configuring SSH to a non-default port</h2>
<p>SSH default port is 22. We want to configure it to non default port.  Since we are using LightSail, we need to open the non default port through the web interface. If you don't do this step, you'll be locked out of the instance. Go to the networking tab on the management console. Then, the firewall option</p>
<img src="https://github.com/davidduckwitz/udacity-linux-server-config/blob/master/lightsailfirewall.png"><br>
Go into your sshd config file: <code>sudo nano /etc/ssh/sshd_config</code>
Change the following options. # means commented out</p>
<pre><code># What ports, IPs and protocols we listen for
# Port 22
Port 2200

# Authentication:
LoginGraceTime 120
#PermitRootLogin prohibit-password
PermitRootLogin no
StrictModes yes

# Change to no to disable tunnelled clear text passwords
PasswordAuthentication No
</code></pre>
<p>Once these changes are made, restart ssh: <code>sudo service restart ssh</code>
Any user can login into the machine using a specify port: <code>sudo user@PublicIP -p 2200</code></p>
<h3><a id="user-content-creating-the-ssh-keys" class="anchor" href="#creating-the-ssh-keys" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Creating the ssh keys</h3>
<pre><code>LOCAL MACHINE:~$ ssh-keygen
</code></pre>
<p>Two things will happen:</p>
<ol>
<li>You can name the file whatever you want.  Keep in mind when you name the file it will give you a private key and public key</li>
<li>It will prompt you for a pass phrase. You can enter one or leave it blank</li>
</ol>
<p>Once the keys are generated, you'll need to login to the user account aka grader here:
You'll make a directory for ssh and store the public key in an authorized_keys files</p>
<pre><code>mkdir .ssh
cd .ssh
</code></pre>
<p>When you are in the directory, create an authorized_keys file. This where you paste the public key that you generated on your local machine.</p>
<pre><code>sudo nano authorized_keys
</code></pre>
<p>Please double check your path by pwd. You should be in your <code>/home/grader/.ssh/</code> when creating the file. You should be login with grader account using the private key from local machine into the server: <code>ssh user@PublicIP -i ~/.ssh/whateverfile_id_rsa</code></p>
<h2><a id="user-content-configuring-firewall-rules-using-ufw" class="anchor" href="#configuring-firewall-rules-using-ufw" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configuring Firewall rules using UFW</h2>
<p>We need to configure firewall rules using UFW. Check to see if ufw is active: <code>sudo ufw status</code>. If not active, lets add some rules</p>
<pre><code>sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2200/tcp
sudo ufw allow 80/tcp or sudo ufw allow www (either one of these commands will work)
sudo ufw allow 123/udp
</code></pre>
<p>Now, you enable the rules: <code>sudo ufw enable</code> and re check the status to see what rules are activity</p>
<h2><a id="user-content-configure-timezone-for-server" class="anchor" href="#configure-timezone-for-server" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configure timezone for server</h2>
<pre><code>sudo dpkg-reconfigure tzdata
</code></pre>
<p>Choose none of the above and choose UTC.  The server by default is on UTC.</p>
<h2><a id="user-content-install-apache-git-and-flask" class="anchor" href="#install-apache-git-and-flask" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Install Apache, Git, and flask</h2>
<h3><a id="user-content-apache" class="anchor" href="#apache" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Apache</h3>
<p>We will be installing apache on our server. To do that:</p>
<pre><code>sudo apt-get install apache2
</code></pre>
<p>If apache was setup correctly, a welcome page will come up when you use the PublicIP. We are going to install mod wsgi, python setup tools, and python-dev</p>
<pre><code>sudo apt-get install libapache2-mod-wsgi python-dev
</code></pre>
<p>We need to enable mod wsgi if it isn't enabled: <code>sudo a2enmod wsgi</code></p>
<p>Let's setup wsgi file and sites-available conf file for our application.
Create the WSGI file in <code>/var/www/catalog/</code> with the following content:</p>
<pre><code>

import sys
import logging

logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, '/var/www/catalog')

from application import app as application
application.secret_key='super_secret_key'
</code></pre>
<p>Please note application.py is my python file. Wherever you housed your application logic.</p>
<p>To setup a virtual host file: <code>cd /etc/apache2/sites-available/catalog.conf</code>:</p>
<pre><code>Virtual Host file
&lt;VirtualHost *:80&gt;
     ServerName  <strong> YOUR SERVER PublicIP</strong>
     ServerAdmin <strong> YOUR EMAIL</strong>
     #Location of the items-catalog WSGI file
     WSGIScriptAlias / /var/www/catalog/catalog.wsgi
     #Allow Apache to serve the WSGI app from our catalog directory
     &lt;Directory /var/www/catalog&gt;
          Order allow,deny
          Allow from all
     &lt;/Directory&gt;
     #Allow Apache to deploy static content
     &lt;Directory /var/www/catalog/static&gt;
        Order allow,deny
        Allow from all
     &lt;/Directory&gt;
      ErrorLog ${APACHE_LOG_DIR}/error.log
      LogLevel warn
      CustomLog ${APACHE_LOG_DIR}/access.log combined
&lt;/VirtualHost&gt;

</code></pre>
<h3><a id="user-content-git" class="anchor" href="#git" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Git</h3>
<p><code>sudo apt-get install git</code></p>
<p>Clone repository into the apache directory. In the <code>cd /var/www</code></p>
<pre><code>mkdir itemsCatalog
cd /var/www/itemsCatalog

sudo git clone https://github.com/harushimo/fullstack-nanodegree-vm.git  itemsCatalog
</code></pre>
<h3><a id="user-content-flask" class="anchor" href="#flask" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Installing Python / Flask and Modules</h3>

# What i've installed
__installed python and some Modules__
- ```sudo apt-get install python``` Python 2.7 CORE<br>
- ```sudo apt-get install python-pip```Script to install the following python modules<br>
- ```pip install sqlalchemy```<br>
- ```pip install requests```<br>
- ```pip install flask```<br>
- ```pip install oauth2client```<br>
- ```pip install Flask-WTF```<br>
- ```pip install functools```<br>
<br>
Change some pathes in Files to run<br>
<p>Update some pathes in the application.py.</p>
1. Find <code>CLIENT_ID = json.loads(open('client_secrets.json', 'r').read())['web']['client_id']</code><br>
--> Change it to <code>CLIENT_ID = json.loads(open('/var/www/catalog/client_secrets.json', 'r').read())['web']['client_id']</code>
2. Find <code>engine = create_engine('sqlite:///categories.db')</code><br>
--> Change it to <code>engine = create_engine('sqlite:///var/www/catalog/categories.db?check_same_thread=False')</code><br>
3. Find <code>oauth_flow = flow_from_clientsecrets('client_secrets.json', scope='')</code><br>
--> Change it to <code>oauth_flow = flow_from_clientsecrets('/var/www/catalog/client_secrets.json', scope='')</code><br>
4. Find <code>app_id = json.loads(open('fb_client_secrets.json', 'r').read())['web']['app_id']</code><br>
--> Change it to <code>app_id = json.loads(open('/var/www/catalog/fb_client_secrets.json', 'r').read())['web']['app_id']</code><br>
5. Find <code>app_secret = json.loads(open('fb_client_secrets.json', 'r').read())['web']['app_secret']</code><br>
--> Change it to <code>app_secret = json.loads(open('/var/www/catalog/fb_client_secrets.json', 'r').read())['web']['app_secret']</code><br>
<p>Update some pathes in the database_setup.py.</p>
1. Find <code>engine = create_engine(
	'sqlite:///categories.db')</code>
   Change it to: <code>engine = create_engine(
	'sqlite:///var/www/catalog/categories.db?check_same_thread=False')</code>
# Run Application
1. Restart apache <code>sudo service apache2 restart</code>
2. Open the PUBLIC IP of your Amazon Server in Browser<br>
<strong> HAVE FUN :) </strong>
<br>
# Troubleshooting
<code>ERROR 500 (Internal Server Error)</code>
--> To get the Error-Message you mus open apache logfile: <code>sudo nano /var/log/apache2/error.log</code>
--> Find the error in the last 1 - 20 Lines<br>
--> If you Google for that error, you will find a lot Solutions for all errors you can see.<br>
<strong>If you can't find a solution for your error, contact me at 'davidduckwitz@googlemail.com' or your Udacity Mentor</strong>

