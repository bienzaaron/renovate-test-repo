### install dependencies

```
brew install nginx

npm i -g verdaccio
```

### start nginx; verdaccio

Nginx / verdaccio are used to proxy requests from locally running renovate to nodejs.org / registry.npmjs.org.

```
killall nginx; nginx -c $(pwd)/nginx.conf -e $(pwd)/access.log

verdaccio -l http://mynpmregistry.com:3001
```

### start container; run commands

```
# start containerbase image and ensure mynpmregistry.com and mynodemirror.com are pointed to the container host
docker run -it --add-host mynpmregistry.com:host-gateway --add-host mynodemirror.com:host-gateway  -v $(pwd):/home/ubuntu/renovate containerbase/base bash


cd /home/ubuntu/renovate
install-tool node v18.17.1
corepack prepare
corepack enable

# install dependencies
apt-get update && apt-get install python3 build-essential
pnpm i

# make sure container can't talk directly to registries
echo "127.0.0.1 nodejs.org" >> /etc/hosts
echo "127.0.0.1 registry.npmjs.org" >> /etc/hosts

# set PAT, start local version of renovate
export RENOVATE_TOKEN=<PAT>
LOG_LEVEL=debug pnpm start --dry-run  bienzaaron/renovate-test-repo > debug.log
```
