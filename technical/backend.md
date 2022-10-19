# Edubadges installation instructions: Backend
## How to get started on your local development environment.
Prerequisites:

* git
* python 3.7.6
* virtualenv
* mysql
* [cairo](https://www.cairographics.org/download/) (SVG utility)

#### Optional extras:

* memcached

#### System-specific requirements:
* OS X: [XCode Command line tools](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/)
* Ubuntu 12.04 (install packages with apt-get): git, git-core, python-virtualenv, gcc, python-pip, python-devel, libjpeg-turbo, libjpeg-turbo-devel, zlib-devel, mariadb-devel, openldap-devel, cyrus-sasl-devel, swig, libxslt-devel, automake, autoconf, libtool, libffi-devel
* CentOS 7.x (install packages with yum): git, git-core, python-virtualenv, gcc, python-pip, python-devel, libjpeg-turbo, libjpeg-turbo-devel, zlib-devel, mariadb-devel, openldap-devel, cyrus-sasl-devel, swig, libxslt-devel, automake, autoconf, libtool, libffi-devel

Note: some of these packages would introduce additional security considerations if left installed on a server used in production.

### Create project directory and environment

* `mkdir edubadges && cd edubadges`
* `virtualenv .venv`
* `source .venv/bin/activate` *Activate the environment (each time you start a session working with the code)*

*Obtain source code and clone into code directory*

* `git clone https://github.com/edubadges/edubadges-server.git`
* `cd edubadges-server`
* `git submodule update --init`

### Create database
```
DROP DATABASE IF EXISTS badgr;
CREATE DATABASE badgr CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
```

### Install timezones
```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root mysql
```

### Install requirements
*from within edubadges-server directory*

* `pip install -r requirements.txt`

if on a mac mysqlclient does not build, try:
```
LDFLAGS=-L/usr/local/opt/openssl/lib pip install mysqlclient
```
### Run / debug IDE
You'll need to add the environment variables from env_vars.sh.example to a run configuration

### Generate a TOTP for first login with super user
If you login to http://localhost:8000/staff/superuser then you'll have to provide a TOTP token. Generate one with:
```
./manage.py addstatictoken superuser
```

### Customize local settings to your environment
* `cp env_vars.sh.example env_vars.sh`
* Edit the env_vars.sh file and insert local credentials for DATABASES and email, then run the following from within the `edubadges-server` directory after sourcing the env_vars.sh:

### Migrate databases, build front-end components
* `./manage.py migrate` - set up database tables
* `./manage.py dist` - generate docs swagger file(s)

### Seed database
* `./manage.py seed -c` - truncate tables and refill with seed data
* `./manage.py seed` - fill tables with seed data if objects don't exist yet

### Run a server locally for development
* `./manage.py runserver`

### See all url's
* `./manage.py show_urls`

### Staff dashboard
* `/staff/superlogin`
    * You can log in on the [staff dashboard](http://localhost:8000/staff/superlogin) with your superuser credentials (if you ran the seeds these will be username: superuser, password: secret).
* `/docs`
    * [API documentation](http://localhost:8000/docs)

### Additional configuration options
Set these values in your settings_local.py file to configure the application to your specific needs. Required options are listed in bold.
* `HELP_EMAIL` (Required)
  - An email address for your support staff.
* `GOOGLE_ANALYTICS_ID`
  - Google Analytics code will be inserted into your pages if this is set to your account tracking code, e.g. 'UA-3929083373-2'. See https://support.google.com/analytics/answer/1008080
* `PINGDOM_MONITORING_ID`
  - If you use Pingdom to monitor site performance, including this setting will embed Pingdom tracking script into the header.
* `OPEN_FOR_SIGNUP = True`
  - This defaults to True, but allows you to turn off signup if you would like to use Badgr for only single-account use or to manually create all users in `/staff`.
* `PAGINATION_SECRET_KEY`
  - Key used for symmetrical encryption of pagination cursors.  If not defined, encryption is disabled.  Must be 32 byte, base64-encoded random string.  For example: python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key())"
