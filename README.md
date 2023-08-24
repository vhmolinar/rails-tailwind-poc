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

Install foreman to run local server
```sh
gem install foreman
```

## Configuring the local environment

Create a postgres container. The command MUST be run at root folder of this project because we are mapping out the unix socket file
```sh
docker run --name rails-tailwind-poc -p 5432:5432 -v $(pwd)/db/postgresql:/run/postgresql -e POSTGRES_HOST_AUTH_METHOD=trust -e POSTGRES_DB=postgres -e POSTGRES_USER=$(whoami) -e POSTGRES_PASSWORD -d postgres:15.4
```

Setup database
```sh
bin/rails db:setup
bin/rails db:migrate
```
