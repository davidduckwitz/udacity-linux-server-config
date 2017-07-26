# udacity-linux-server-config

SSH IP : 52.58.237.3 (Static IP) <br>
SSH Port: 2200 (Changed from 22)<br>
URL to App: http://52.58.237.3 <br>
Your Keyfile for SSH (I recommend 'putty') --> Download: <here><br>

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


# What i've done
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
Locate the SSH key you created for the grader user.<br>

