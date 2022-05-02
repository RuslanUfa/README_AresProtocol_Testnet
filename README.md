# Ares Protocol
## Перенос ноды 


### 1 Команды на текущем сервере

#### 1.1 Остановите свой валидатор в JS.aresprotocol.io

#### 1.2 Остановить docker
```
docker stop ares_gladios && docker cp ares_gladios:/root/.local/share/gladios-node ./ares-chain-data
```

#### 1.3 Удалить docker
```
docker rm ares_gladios && docker rmi aresprotocollab/ares_gladios:latest
```


### 2 Команды на новом сервере

#### 2.1 Установить обновления
```
sudo apt update && sudo apt -y upgrade
```

#### 2.2 Установить Docker
```
apt install docker.io
```

#### 2.3 Вытащить последний образ программы
```
docker pull aresprotocollab/ares_gladios:latest
```

#### 2.4 Установка ноды по методу Docker (можно выбрать альтернативные методы, см. официальный гайд, ссылка ниже)
```
docker run -d --name ares_gladios -p 9944:9944 -v `pwd`/ares-chain-data:/data aresprotocollab/ares_gladios:latest gladios-node --name your-name --chain gladios --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --warehouse http://api.aresprotocol.io  --validator
```

#### (Пример установки)
```
docker run -d --name ares_gladios -p 9944:9944 -v `pwd`/ares-chain-data:/data aresprotocollab/ares_gladios:latest gladios-node --name ares_СryptoHelp_0x982293a6ABA77E8dD4B18E35FA7eE022BD0c2ce9 --chain gladios --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --warehouse http://api.aresprotocol.io  --validator
```

#### 2.5 Настройка сеансовых ключей
```
docker exec -it ares_gladios bash -c "apt update && apt install -y curl && curl -X POST http://localhost:9933 -H 'Content-Type: application/json' -d '{\"id\":1, \"jsonrpc\":\"2.0\", \"method\": \"author_rotateKeys\"}'"
```

#### (Пример вывода)
```
{"jsonrpc":"2.0","result":"0x96d1de2174990fbce9fe989a0e0e48c505b2206412dbe62fae12d4c3be8adb55fe7b2a6b0c65ea6037c805d421b80e4717643f7c2b6c5bdd6d6098dc0d53512f743edda90453481b4d3d603d2a9a68097233c83bcc7a3b10c862f30151c7da12","id":1}
```

#### Сохраните полученный ключ в JS.aresprotocol.io (пример)
```
0x96d1de2174990fbce9fe989a0e0e48c505b2206412dbe62fae12d4c3be8adb55fe7b2a6b0c65ea6037c805d421b80e4717643f7c2b6c5bdd6d6098dc0d53512f743edda90453481b4d3d603d2a9a68097233c83bcc7a3b10c862f30151c7da12
```

### Посмотреть логи
```
docker logs -f ares_gladios  -n 1000
```

### Официальный гайд по установке новой ноды (часть 3/3)
```
[[Medium.com/streamrblog](https://medium.com/streamrblog/how-to-join-the-brubeck-testnet-c8b823c847f8)](https://aresprotocollab.medium.com/public-deployment-of-gladios-testnet-nodes-second-ohase-third-part-807a1e098423)
```

### Официальный гайд на обновление
```
https://aresprotocollab.medium.com/gladios-upgraded-node-commands-and-added-online-identification-penalty-mechanisms-for-validators-4650793d8ad0
```
