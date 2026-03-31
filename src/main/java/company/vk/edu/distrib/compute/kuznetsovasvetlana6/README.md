## Инструкция по сборке:
### 1. Для запуска сервера с хранением в файловой системе:
```
./gradlew run
```

### 2. Для запуска сервера с хранением в памяти:
В Server.java поменять MyKVServiceFactoryFile на MyKVServiceFactoryMemory.

Аналогично, ```./gradlew run```

### 3. Отправка запросов на сервер:
- HTTP GET /v0/status: ```curl -i -X GET "http://localhost:8080/v0/status"```
- HTTP GET /v0/entity?id=<ID>: ```curl -i -X GET "http://localhost:8080/v0/entity?id=1"```
- HTTP PUT /v0/entity?id=<ID>: ```curl -i -X PUT "http://localhost:8080/v0/entity?id=1" -d "my_data"```
- HTTP DELETE /v0/entity?id=<ID>:  ```curl -i -X DELETE "http://localhost:8080/v0/entity?id=1"```

### 4. Для запуска тестов:
1. ```
   docker pull haydenjeune/wrk2
   ```
2. Запустить в одном окне сервер
3. Во втором окне выполнить команду:
   
Для PUT:
```
docker run --rm -v "%cd%:/data" haydenjeune/wrk2 -t1 -c1 -R200 -d30s --latency -s /data/put.lua http://host.docker.internal:8080
```
Для GET:
```
docker run --rm -v "%cd%:/data" haydenjeune/wrk2 -t1 -c1 -R200 -d30s --latency -s /data/get.lua http://host.docker.internal:8080
```
