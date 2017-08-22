# blockchain #
Hyperledger Sawtooth Case Implementation

## Infraestrutura ##

### Iniciar o ambiente ###
```
docker-compose up -d
```

### Parar o ambiente ###
```
docker-compose up -d
```

### Logar no container cliente ###
```
docker exec -it sawtooth-client-default bash
```

### Confirmar conectividade ###
```
curl http://rest-api:8080/blocks
```

### Testar conectividade do HOST do Docker ###
```
curl http://localhost:8080/blocks
```

### Submeter transações de teste ###
```
intkey create_batch --count 10 --key-count 5
intkey load -f batches.intkey -U http://rest-api:8080
sawtooth batch submit -f batches.intkey --url http://rest-api:8080
```

### Ver a lista de blocos ###
```
sawtooth block list --url http://rest-api:8080
```

### Ver um bloco em particular ###
```
sawtooth block show --url http://rest-api:8080 {BLOCK ID}
```

### Ver a lista de nodes ###
```
sawtooth state list --url http://rest-api:8080
```

### Ver os dados em um endereço (node) ###
```
sawtooth state show --url http://rest-api:8080 {STATE ADDRESS}
```


## Conexão com a API REST ##

### No container cliente ###
```
curl http://rest-api:8080/blocks
```

### No computador HOST do Docker ###
```
curl http://localhost:8080/blocks
```

## Rodando o contrato de teste XO (Jogo da Velha)

### Iniciar os usuários jack e jill ###
```
xo init --username jack --url http://rest-api:8080
xo init --username jill --url http://rest-api:8080
```

### Mudar usuário para jack e criar o jogo ###
```
xo init --username jack
xo create game1
xo list
```

### Primeira jogada do Jack ###
```
xo take game1 4
```

### Primeira jogada do Jill ###
```
xo init --username jill
xo take game1 3
```

### Situação parcial do jogo ###
```
xo show game1
```

### Continuando o jogo... ###
```
# Jack
xo init --username jack
xo take game1 5
xo show game1

# Jill
xo init --username jill
xo take game1 6
xo show game1

# Jack
xo init --username jack
xo take game1 7
xo show game1

# Jill
xo init --username jill
xo take game1 1
xo show game1

# Jack
xo init --username jack
xo take game1 2
xo show game1

# Jill
xo init --username jill
xo take game1 9
xo show game1
```

O Jill ganhou :D