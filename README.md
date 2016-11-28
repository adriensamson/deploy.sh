# deploy.sh

deploy.sh in a simple shell script to deploy your projects.

## Installation

Clone it.
```
git clone https://github.com/adriensamson/deploy.sh
```
Add a link to `lib/deploy` in your path.
```
ln -s /path/to/deploy.sh/lib/deploy ~/bin/
```

## Setup

You'll end up with this directory structure:

```
releases/
shared/
sources/
current -> releases/2014-01-10-19-24-48
.deployrc
```

```
deploy -i git@github.com/you/yourproject
```

You can now deploy with
```
deploy
```

## Auto links

You can add a list of symbolic links to recreate at each release in `.deploy.links`. For instance, with

```
config.json
nested/conf.yml
key.pem ssl/key.pem
```

it will create the following links :

```
releases/$RELEASE/config.json -> shared/config.json
releases/$RELEASE/nested/conf.yml -> shared/nested/conf.yml
releases/$RELEASE/ssl/key.pem -> shared/key.pem
```

## Hooks

### .deploy.extract.after
This hook is executed after the extraction of your project sources in a new release subdirectory. You get the name of that subdirectory in `$1`. Here is an example to install composer dependencies.
```
cd releases/$1

curl -sS https://getcomposer.org/installer | php
php composer.phar install
```
