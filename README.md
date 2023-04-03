Canvas LMS
======

Canvas is a modern, open-source [LMS](https://en.wikipedia.org/wiki/Learning_management_system)
developed and maintained by [Instructure Inc.](https://www.instructure.com/) It is released under the
AGPLv3 license for use by anyone interested in learning more about or using
learning management systems.

[Please see our main wiki page for more information](http://github.com/instructure/canvas-lms/wiki)

Installation
=======

Detailed instructions for installation and configuration of Canvas are provided
on our wiki.

 * [Quick Start](http://github.com/instructure/canvas-lms/wiki/Quick-Start)
 * [Production Start](http://github.com/instructure/canvas-lms/wiki/Production-Start)


sudo apt-get update
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get -y update
udo apt-get -y install postgresql-14
sudo apt-get -y install zlib1g-dev libldap2-dev libidn11-dev libxml2-dev libsqlite3-dev libpq-dev libxmlsec1-dev curl build-essential

rvm install "ruby-2.7.0"
rvm use 2.7.0
gem install bundle
gem install bundler:2.3.26
gem install nokogumbo scrypt sanitize ruby-debug-ide
sudo chown -R codespace:codespace /workspaces/canvas-lms/
sudo chown -R codespace:codespace /usr/local/rvm/rubies/ruby-2.7.0/lib/ruby/gems/2.7.0
bundle _2.3.26_ install
**STOPPED HERE**
yarn install --pure-lockfile
for config in amazon_s3 delayed_jobs domain file_store outgoing_mail security external_migration dynamic_settings database; \
          do cp -v config/$config.yml.example config/$config.yml; done
sudo chown -R codespace:codespace /usr/local/rvm/rubies/ruby-2.7.0/lib/ruby/gems/2.7.0
bundle _2.3.26_ update
sudo chown -R codespace:codespace /var/run/postgresql/
export PGHOST=localhost
/usr/lib/postgresql/14/bin/initdb ~/postgresql-data/ -E utf8
/usr/lib/postgresql/14/bin/pg_ctl -D ~/postgresql-data/ -l ~/postgresql-data/server.log start
/usr/lib/postgresql/14/bin/createdb canvas_development
bundle exec rails canvas:compile_assets
bundle exec rails db:initial_setup



THINGS THAT I WILL BE USING REGULARLY
stopping DB safely (hoping to prevent corruption)

export PGHOST=localhost
/usr/lib/postgresql/12/bin/pg_ctl stop -D ~/postgresql-data/
after this, go to command palette and select Codespaces: Stop Current Codespace
starting the db and launching the Canvas server (providing access to Canvas UI)

export PGHOST=localhost
/usr/lib/postgresql/12/bin/pg_ctl start -D ~/postgresql-data/
bundle install
bundle exec rails server