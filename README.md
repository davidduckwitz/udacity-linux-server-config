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
<p><strong>Please make sure your private key is the same directory. The default port for SSH is 22 but we'll change it later on in the documentation</strong>


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

