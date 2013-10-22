Create a custom user for your database:

sudo -u postgres createuser --superuser "usc.admin" 
sudo -u postgres psql 
postgres=# \password "usc.admin" 
Enter new password: 
Enter it again: 
\q 
createdb usc.admin

Create main database:

createdb usc.website