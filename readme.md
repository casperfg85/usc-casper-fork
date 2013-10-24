# USC Website

## Installation

### Dependencies

First, install all required dependencies:
```
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install python-pip python-dev python-setuptools python-imaging build-essential python-virtualenv virtualenvwrapper postgresql postgresql-client libpq-dev nodejs 
```

Then, create our virtual environment:
```
mkvirtualenv usc --no-site-packages --distribute
workon usc
cdvirtualenv
```
Note: Restart might be needed before the command mkvirtualenv be available

Your prompt should now look similar to this:
```
(usc)neegool@bulalo ~ $
```

Next, from within the virtual environment, we install the following:
```
pip install -U mezzanine
pip install -U yolk
pip install psycopg2
```

### Database

Once the dependencies have been installed, we now setup the database.

Next, create a custom user for your database:
```
sudo -u postgres createuser --superuser $USER
sudo -u postgres psql
```

Once you have entered the PostgreSQL REPL, setup the password (use "password" as our password)
```
postgres=# \password [enter your username here]
```

Exit the REPL using by typing ```\q``` .

Let us now create our database:
```
createdb $USER
createdb usc.website
```

### Project

Clone our repository, and switch to that directory (make sure you've been added to the repo as a collaborator. Otherwise, kindly inform me so that I can add you)
```
git clone https://github.com/neegool/usc-website.git
cd usc-website
```

Customize the local_settings.py to be compatible for your system. Change the USER part.
```
gedit local_settings.py
```

It should now look something similar to this:
```
#Not used with sqlite3.
"USER": "neil"
```
We can now try running our project. First set up our database:
```
python manage.py createdb
```

Leave the username to be the default. Make sure that the domain and the port is also default ```(127.0.0.1:8000)```, and then say Yes to the rest. Afterwards we can now run the server by typing:
```
python manage.py runserver
```

Point your browser to ```127.0.0.1:8000```. If you can see the website, you have successfully completed our setup!

### Tools

We also need to install Ruby and RubyGems, which are needed by some of the tools that we'll be using. 

First, make sure that you are outside our virtual environment by typing:
```
deactivate
```

Then, install Ruby by issuing the following commands:

```
curl -L https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm requirements
rvm install ruby
rvm use ruby --default
rvm rubygems current
```

Next, install Coffeescript, Jade and Less:
```
sudo npm install -g coffee-script
sudo npm install -g less
sudo npm install jade
```

Then, install Bundler (needed by Guard) by typing:
```
gem install bundler
```

Next, go back to our virtual environment:
```
workon usc
cdvirtualenv
```

Finally, setup Guard:
```
bundle
bundle exec guard
```
--END--