# uwsgi
http://projects.unbit.it/uwsgi/

# mod_wsgi daemonize mode
http://countergram.com/pylons-lighttpd-flup

# lots of different ways to deploy python
http://news.ycombinator.com/item?id=1824171

# maybe mod_wsgi doesn't look appealing (blocking) on your web server (nginx)
http://blog.dscpl.com.au/2009/05/blocking-requests-and-nginx-version-of.html

# maybe you're watching your python web app gobble up memory because your apache was tuned for php, not mod_wsgi or mod_python
http://blog.dscpl.com.au/2009/03/load-spikes-and-excessive-memory-usage.html

# compile everythin, linode
http://library.linode.com/web-servers/nginx/python-uwsgi/ubuntu-10.10-maverick#create_uwsgi_init_script


# example configs
http://projects.unbit.it/uwsgi/wiki/Example

# packaging nginx
# http://ubuntuforums.org/showthread.php?p=6953724%3E

# add-apt-repository isn't installed by default. You have to install the python-software-properties package first.
# https://launchpad.net/ubuntu/+ppas
sudo apt-get install python-software-properties

# stable version of nginx since 8.4 comes w/ uwsgi module included
# http://wiki.nginx.org/Install
# install from the personal package
sudo add-apt-repository ppa:nginx/stable
sudo apt-get update 
sudo apt-get install nginx

# uwsgi
apt-get update
apt-get upgrade
apt-get install build-essential psmisc python-dev libxml2 libxml2-dev python-setuptools

cd /opt/
wget http://projects.unbit.it/downloads/uwsgi-0.9.6.6.tar.gz
tar -zxvf uwsgi-0.9.6.6.tar.gz
ln -s uwsgi-0.9.6.6/ uwsgi/
cd uwsgi/
python setup.py install

adduser --system --no-create-home --disabled-login --disabled-password --group uwsgi
chown -R uwsgi:uwsgi /opt/uwsgi
touch /var/log/uwsgi.log
chown uwsgi /var/log/uwsgi.log

# virtualenv
mkvirtualenv --no-site-packages uwsgi-flask-test
easy_install yolk flask


# sample app
sudo mkdir /opt/uwsgi-flask-test/
sudo chown app:app /opt/uwsgi-flask-test/
vim /opt/uwsgi-flask-test/myapp.py

from flask import Flask
app = Flask(__name__)

@app.route('/uwsgi-flask-test/')
def hello_world():
	return "Hello World!"

if __name__ == '__main__':
	app.run()


# uwsgi command
uwsgi -s 127.0.0.1:3031 --module myapp --callable app --home /home/app/.virtualenvuwsgi-flask-test/

# nginx config
sudo vim /etc/nginx/sites-available/uwsgi-flask-test

server {
	listen       7777;

	location /uwsgi-flask-test/ {
		include uwsgi_params;
		uwsgi_pass 127.0.0.1:3031;
	}
}

sudo ln -s /etc/nginx/sites-available/uwsgi-flask-test /etc/nginx/sites-enabled/uwsgi-flask-test
sudo /etc/init.d/nginx restart


# trouble shooting
#404
## check uwsgi output - no 404.... indpect nginx configs, otherwise check you app's route's
#502
## uwsgi not running
## ports don't match
## perms on socket?


