sudo docker run \
--name zabbix-server \
--network zabbix-net \
-v /var/lib/zabbix/alertscripts:/usr/lib/zabbix/alertscripts \
-v /var/lib/zabbix/timezone:/etc/timezone \
-v /var/lib/zabbix/localtime:/etc/localtime \
-p 10051:10051 -e DB_SERVER_HOST="zabbix-postgres" \
-e POSTGRES_USER="zabbix" \
-e POSTGRES_PASSWORD="zabbix" \
-d yurashupik/zabbix:2
