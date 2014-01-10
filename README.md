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
sources/
current -> releases/2014-01-10-19-24-48
.deployrc
```

```
mkdir releases
git clone --mirror git@github.com/you/yourproject sources
echo GIT_REPO=sources >.deployrc
```

You can now deploy with
```
deploy
```

## Hooks

### .deploy.extract.after
This hook is executed after the extraction of your project sources in a new release subdirectory. You get the name of that subdirectory in `$1`. Here is an example to install composer dependencies.
```
cd releases/$1

curl -sS https://getcomposer.org/installer | php
php composer.phar install
```
