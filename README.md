### install dependencies

```
brew install nginx

npm i -g verdaccio
```

### start nginx; verdaccio

```
killall nginx; nginx -c $(pwd)/nginx.conf -e $(pwd)/access.log

verdaccio -l http://mynpmregistry.com:3001
```

### start container; run commands

```
docker run -it --add-host mynpmregistry.com:host-gateway --add-host mynodemirror.com:host-gateway  -v $(pwd):/home/ubuntu/renovate containerbase/base bash

export RENOVATE_TOKEN=<PAT>

echo "127.0.0.1 nodejs.org" >> /etc/hosts
echo "127.0.0.1 registry.npmjs.org" >> /etc/hosts

cd /home/ubuntu/renovate
install-tool node v18.17.1
corepack prepare
corepack enable

apt-get update && apt-get install python3 build-essential
pnpm i

LOG_LEVEL=debug pnpm start --dry-run  bienzaaron/renovate-test-repo > debug.log
```
