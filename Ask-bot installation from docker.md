---


---

<h1 id="askbot-installation-from-docker--email-configration">AskBot Installation From Docker &amp; email configration</h1>
<h2 id="askbot-installation">askbot installation</h2>
<ul>
<li>Pull docker from <a href="https://hub.docker.com/r/berdon/docker-askbot">Here</a><br>
<code>docker pull berdon/docker-askbot</code></li>
<li>Create a container<br>
<code>docker create --name=askbot -p 3000:80 -v /askbot:/data/ berdon/docker-askbot:latest</code>
<blockquote>
<p><code>create</code> for creating container<br>
<code>--name</code> Container name<br>
<code>-p</code> Port, Host:Gust<br>
<code>-v</code> for link direntry from Container to host,    Directry on host : directry on gust<br>
<code>berdon/docker-askbot:latest</code> Image name</p>
</blockquote>
</li>
<li>run container<br>
<code>docker start askbot</code></li>
</ul>
<h2 id="configure-email-smtp-server">configure email Smtp server</h2>
<ul>
<li>
<p>get in to docker askbot shell<br>
<code>docker exec -it askbot bash</code></p>
</li>
<li>
<p>go to app directry<br>
<code>cd /app/</code></p>
</li>
<li>
<p>add “SMTP” configrations on “<a href="http://settings.py">settings.py</a>”<br>
<code>nano settings.py</code></p>
<blockquote>
<p>in most cases there is no editor avilable inside docker so you need to install one<br>
<code>apt install nano</code><br>
this will install nano editor</p>
</blockquote>
</li>
<li>
<p>go to “#outgoing mail server settings” add your configration<br>
<code>#outgoing mail server settings</code><br>
<code>SERVER_EMAIL = ''</code><br>
<code>DEFAULT_FROM_EMAIL = ''</code><br>
<code>EMAIL_HOST_USER = 'UserName'</code><br>
<code>EMAIL_HOST_PASSWORD = 'Password'</code><br>
<code>EMAIL_SUBJECT_PREFIX = ''</code><br>
<code>EMAIL_HOST='smtp server '</code><br>
<code>EMAIL_PORT=Port No</code><br>
<code>EMAIL_USE_TLS=True</code><br>
<code>EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'</code></p>
</li>
<li>
<p>exit from Docker shell<br>
<code>exit</code></p>
</li>
<li>
<p>restart askbot</p>
<ul>
<li><code>docker restart askbot</code></li>
</ul>
</li>
</ul>
<h2 id="enable-email-verification-in-askbot">enable email verification in askbot</h2>
<ul>
<li>goto your askbot website
<blockquote>
<p>http:// your site address/settings/QA_SITE_SETTINGS/<br>
“Base URL for your Q&amp;A forum, must start with http or https” give your Site Url<br>
http:// your site address/settings/ACCESS_CONTROL/<br>
“Require valid email for” = Account registration<br>
Hit Save</p>
</blockquote>
</li>
</ul>
<h2 id="debugging">Debugging</h2>
<ul>
<li>for cheking email smtp config is working or not
<blockquote>
<p>goto gocker terminal <code>docker exec -it askbot bash</code><br>
goto python shell <code>python manage.py shell</code><br>
<code>&gt;&gt;&gt; from django.core.mail import EmailMessage</code><br>
<code>&gt;&gt;&gt; email = EmailMessage('email Testing', 'This is a test for that Strange user', to=['Thatuser@Hisdomain.com'])</code><br>
<code>&gt;&gt;&gt; email.send()</code><br>
This should return with the status 1, which means it worked.`</p>
</blockquote>
</li>
<li>Some times you need to use “sudo with docker”</li>
</ul>

