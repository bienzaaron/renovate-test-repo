127.0.0.1 mynodemirror.com
127.0.0.1 mynpmregistry.com

killall nginx; nginx -c $(pwd)/nginx.conf -e $(pwd)/access.log