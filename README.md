127.0.0.1 mynodemirror.com
127.0.0.1 mynpmregistry.com

127.0.0.1 nodejs.org
127.0.0.1 registry.npmjs.org

killall nginx; nginx -c $(pwd)/nginx.conf -e $(pwd)/access.log

verdaccio -l http://mynpmregistry.com:3001
