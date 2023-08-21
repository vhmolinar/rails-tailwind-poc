# Rails + Tailwind POC

## Creating the application

Install PostgreSQL GEM
```sh
sudo apt install libpq-dev
gem install pg -v '1.5.3' --source 'https://rubygems.org'
```

Create our rails project having tailwind as the css library and postgresql as the database
```sh
rails new rails-tailwind-poc --css tailwind --database postgresql
```

## Configuring the local environment

Create a postgres container, MUST run at root folder of this project because we are mapping out the unix socket file
```sh
docker run --name rails-tailwind-poc -p 5432:5432 -v $(pwd)/db/postgresql:/run/postgresql -e POSTGRES_HOST_AUTH_METHOD=trust -e POSTGRES_DB=postgres -e POSTGRES_USER=$(whoami) -e POSTGRES_PASSWORD -d postgres:15.4
```

Setup a symlink between the mapped volume folder and the standard /var/run/postgresql dir for database socket files.
```sh
ln -s $(pwd)/db/postgresql /var/run/postgresql
```

Setup database
```sh
bin/rails db:setup
bin/rails db:migrate
```

Install foreman to run local server
```sh
gem install foreman
```