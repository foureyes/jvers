---
layout: post
title: Python Web App Deployment With nginx, uwsgi and daemontools
---
### On Deploying Python Web Apps...###
Ok.  You've picked a Python web framework that fits your project or your personal style.  You've coded up the foundation of your application using your framework's built-in dev server.  Now what?  There's a bunch of combinations of web servers, application servers and protocols to choose from!  Just look at this [hacker news thread] (http://news.ycombinator.com/item?id=1824171). 

One of the stacks I've been looking at involves using:
* [nginx] (http://nginx.org/) as the web esrver
* [uwsgi] (http://projects.unbit.it/uwsgi/) as the application container uwsgi
* [daemontools] (http://cr.yp.to/daemontools.html) to daemonize 

But why use this particular combination of technologies?  I've had experience with Python deployed on lighttpd and fastcgi, and it works pretty well.  It's fairly solid, and it logs exceptions to lighttpd's own error log.  Unfortunately, if you're deploying more than one app on it, reloading lighttpd will "blip" all of those applications.  Also, occasionally, some fastcgi processes don't get killed if lighttpd shuts down uncleanly.  This leads to incredibly perplexing behavior once lighttpd comes up!

I've also taken a look at nginx and fastcgi managed by daemontools.  This also works ok, but I've had problems digging out stack traces when an app 500's.  I'm not entirely sure what's going on, but I suspect flup is swallowing the error somehow.

Of course, there are other reasons why you might consider this alternate setup.  Maybe Apache's mod_wsgi isn't an option because you've [tuned Apache to serve PHP] (http://blog.dscpl.com.au/2009/03/load-spikes-and-excessive-memory-usage.html).  Maybe you're unsure about [mod_wsgi on nginx] (http://blog.dscpl.com.au/2009/05/blocking-requests-and-nginx-version-of.html).  Whatever the case, uwsgi, seems to be a legitimate choice for deploying Python web apps.  Here's a quick tour on how to get started with this stack.  I'll be using a simple [flask] (http://flask.pocoo.org/) app to test things out.  I'll go over the following:

1. Installing the latest stable nginx
2. Installing uwsgi
3. Creating a Flask hello world
4. Running your Flask app with uwsgi
5. Hooking everything up with your nginx config
6. Managing your uwsgi server with daemontools



### Stable nginx Comes With uwsgi ###
The latest stable version of nginx comes with a module that allows it to communicate with a uwsgi applications server.  You can compile the latest stable version of nginx by source or by [creating a deb package] (http://ubuntuforums.org/showthread.php?p=6953724%3E).  However, I've found that the easiest way to install it is by using the [nginx personal package archive] (http://wiki.nginx.org/Install).  
{% highlight bash %}
# install python-software-properties to get add-apt-repository
sudo apt-get install python-software-properties

sudo add-apt-repository ppa:nginx/stable
sudo apt-get update 
sudo apt-get install nginx
{% endhighlight %}

### Installing uwsgi ###
As of writing this, the actual uwsgi binary (which is distinct from the module that allows nginx to communicate with a uwsgi server) doesn't seem to exist as a .deb package.  However, it can be installed by source easily. 
{% highlight bash %}
#you'll have to install a few dependencies first...
apt-get install build-essential psmisc python-dev libxml2 libxml2-dev python-setuptools

#download and install uwsgi
cd /opt/
wget http://projects.unbit.it/downloads/uwsgi-0.9.6.6.tar.gz
tar -zxvf uwsgi-0.9.6.6.tar.gz
ln -s uwsgi-0.9.6.6/ uwsgi/
cd uwsgi/
python setup.py install
{% endhighlight %}

### Flask ###
Installing flask is straightforward; just use pip or easy_install.  Put it in a virtualenv specific to your app if you want to isolate the libraries that your project uses. 
{% highlight bash %}
# make a virtualenv for your app
mkvirtualenv --no-site-packages uwsgi-flask-test
easy_install yolk flask

sudo mkdir /opt/uwsgi-flask-test/
sudo chown app:app /opt/uwsgi-flask-test/
vim /opt/uwsgi-flask-test/myapp.py
{% endhighlight %}

This is the hello world app that I used to test out the nginx/uwsgi stack.
{% highlight python %}
from flask import Flask
app = Flask(__name__)

@app.route('/uwsgi-flask-test/')
def hello_world():
	return "Hello World!"

if __name__ == '__main__':
	app.run()
{% endhighlight %}


### Running Your Flask App in uwsgi ###
To run the hello world app under wsgi, we have to start it using the uwgi binary.  You can set the virtualenv that you're using by specifying a value for the --home option.  Also note that the name of your module should be passed into the --module option and the name of your application's wsgi callable (in this case, app) should be passed into the --callable option.  Run this command to start up your uwsgi server.
{% highlight bash %}
uwsgi -s 127.0.0.1:3031 --module myapp --callable app --home /home/app/.virtualenvuwsgi-flask-test/
{% endhighlight %}

### Putting it All Together With nginx ###
Now that your Flask up is running with uwsgi, you'll have to configure nginx to connect to your uwsgi server.  Create a file called /etc/nginx/sites-available/uwsgi-flask-test.
{% highlight nginx %}
server {
	listen       7777;

	location /uwsgi-flask-test/ {
		include uwsgi_params;
		uwsgi_pass 127.0.0.1:3031;
	}
}
{% endhighlight %}

Enable your new configuration and restart.
{% highlight nginx %}
sudo ln -s /etc/nginx/sites-available/uwsgi-flask-test /etc/nginx/sites-enabled/uwsgi-flask-test
sudo /etc/init.d/nginx restart
{% endhighlight %}

You should be able to hit your webserver (in the example case, localhost:7777/uwsgi-flastk-test/) to see your app.  If there's an issue, you can check the output of your uwsgi server.  If there's no output, go over your nginx configuration and your uwsgi startup parameters.  Once you have everything setup, you can have daemontools manage your uwsgi server.  Just modify the run-script from above and put it in your urn script.  For example, /etc/service/uwsgi-flask-test/run should look like:
{% highlight bash %}
#!/bin/sh

exec su - app -c "uwsgi -s 127.0.0.1:3031 --module myapp --callable app --home /home/app/.virtualenvs/uwsgi-flask-test/ --pythonpath /opt/uwsgi-flask-test/ --logto /tmp/uwsgi.log"
{% endhighlight %}


### Troubleshooting ###
* 404 - where'd my page go?
   * Check uwsgi output.  If it's not showing a 404...
   * Inspect nginx configs.
   * Otherwise check you app's routes.
* 502 - bad, bad gateway
   * First make sure your uwsgi is running!
   * If it's running, does the port in your nginx config match the one specified in your uwsgi start script? 
   * If you're using sockets, check the perms.

### Someone's Definitely Done This Already ###
I've pieced together this tutorial with some help from the internet and a bit of trial and error.  Here are some more resources:
* Linode has an in-depth [article] ( http://library.linode.com/web-servers/nginx/python-uwsgi/ubuntu-10.10-maverick#create_uwsgi_init_script) on doing the whole nginx with uwsgi thing as well...
* So does [this blog] (http://timothyfletcher.com/blog/running-django-apps-on-nginx-and-uwsgi/)
* And [this blog] (http://www.jeremybowers.com/blog/post/5/django-nginx-and-uwsgi-production-serving-millions-page-views/)

example configs
http://projects.unbit.it/uwsgi/wiki/Example
