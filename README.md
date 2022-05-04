# Ares Protocol
## Перенос ноды 

#### Для начала остановите свой валидатор в JS.aresprotocol.io

### 1 Команды на текущем сервере

#### 1.1 Остановить docker
```
docker stop ares_gladios && docker cp ares_gladios:/root/.local/share/gladios-node ./ares-chain-data
```

#### 1.2 Удалить docker
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

#### 2.4 Запуск ноды по методу Docker (можно выбрать альтернативные методы, см. официальный гайд, ссылка ниже)
```
docker run -d --name ares_gladios -p 9944:9944 -v `pwd`/ares-chain-data:/data aresprotocollab/ares_gladios:latest gladios-node --name your-name --chain gladios --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --warehouse http://api.aresprotocol.io  --validator
```

#### (Пример установки) вместо "your-name" вводите свои данные "ares_username_BSC address"
```
docker run -d --name ares_gladios -p 9944:9944 -v `pwd`/ares-chain-data:/data aresprotocollab/ares_gladios:latest gladios-node --name ares_СryptoHelp2_0x782293a6ABA77E8dD4B18E35FA7eE022BD0c2cf8 --chain gladios --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --warehouse http://api.aresprotocol.io  --validator
```

#### Посмотреть логи
```
docker logs -f ares_gladios  -n 1000
```

#### 2.5 Проверить статус развертывания
[Log in Polkadot Telemetry](https://telemetry.polkadot.io/#list/0xcc07acbee59e89a8bc99d87a24364b514d6ae657551338547b713444583eaac2)

#### 2.6 Установка ключей сеанса
```
docker exec -it ares_gladios bash -c "apt update && apt install -y curl && curl -X POST http://localhost:9933 -H 'Content-Type: application/json' -d '{\"id\":1, \"jsonrpc\":\"2.0\", \"method\": \"author_rotateKeys\"}'"
```

#### (Пример вывода)
```
{"jsonrpc":"2.0","result":"0x96d1de2174990fbce9fe989a0e0e48c505b2206412dbe62fae12d4c3be8adb55fe7b2a6b0c65ea6037c805d421b80e4717643f7c2b6c5bdd6d6098dc0d53512f743edda90453481b4d3d603d2a9a68097233c83bcc7a3b10c862f30151c7da12","id":1}
```

#### 2.7 Перейдите в JS.aresprotocol.io и сохраните полученный ключ в вашей учетной записи (пример)
```
0x96d1de2174990fbce9fe989a0e0e48c505b2206412dbe62fae12d4c3be8adb55fe7b2a6b0c65ea6037c805d421b80e4717643f7c2b6c5bdd6d6098dc0d53512f743edda90453481b4d3d603d2a9a68097233c83bcc7a3b10c862f30151c7da12
```

#### 2.8 Станьте валидатором
```
Войдите на страницу ставок и перейдите на вкладку «Действия с учетной записью», Выберите учетную запись, которой вы хотите управлять, нажмите «Подтвердить» и на всплывающей странице установите процент комиссии вознаграждения
```

#### 2.9 Ваша нода появитя в списке во вкладке «Ожидание», осталось только подождать


### Официальный гайд по установке новой ноды (часть 3/3)
[Medium.com/Second phase/third part](https://aresprotocollab.medium.com/public-deployment-of-gladios-testnet-nodes-second-ohase-third-part-807a1e098423)

### Официальный гайд на обновление
[Medium.com/Upgraded Node](https://aresprotocollab.medium.com/gladios-upgraded-node-commands-and-added-online-identification-penalty-mechanisms-for-validators-4650793d8ad0)
