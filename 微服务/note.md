docker快速安装rabbitmq  ： https://www.cnblogs.com/angelyan/p/11218260.html

... https://www.cnblogs.com/alangur/p/12916416.html




kong  (https://www.jianshu.com/p/a2e0bc8f4bfb)

docker network create kong-net

docker run -d --name kong-database --network=kong-net  -p 5432:5432  -e "POSTGRES_USER=kong" -e "POSTGRES_DB=kong"  -e "POSTGRES_PASSWORD=123456"  postgres

docker run --rm --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database"  -e "KONG_PG_PASSWORD=123456" kong:latest kong migrations bootstrap

docker run -d --name kong --network=kong-net -e "KONG_DATABASE=postgres"  -e "KONG_PG_HOST=kong-database"  -e "KONG_PG_PASSWORD=123456"   -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout"  -e "KONG_PROXY_ERROR_LOG=/dev/stderr"  -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" -p 8000:8000 -p 8443:8443 -p 8001:8001 -p 8444:8444 kong:latest


docker安装Konga

https://www.cnblogs.com/alangur/p/13071324.html

docker run --network=kong-net --rm pantsel/konga:latest -c prepare -a postgres -u postgresql://kong:qwe123QWE@kong-database:5432/konga
docker run -p 1337:1337 --network kong-net --name konga -e "NODE_ENV=production"  -e "DB_ADAPTER=postgres" -e "DB_URI=postgresql://kong:qwe123QWE@kong-database:5432/konga" pantsel/konga
