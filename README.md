# MiniWebSocket

MiniWebSocket é uma biblioteca JavaScript minimalista para criar **conexões WebSocket** em tempo real, tanto no servidor quanto no cliente.  
Com ela, você consegue criar chats, notificações e sistemas que precisam de comunicação instantânea de forma fácil e rápida.

---

## 💡 Funcionalidades

- Criação de **servidor WebSocket** simples
- Conexão de múltiplos **clientes**
- Envio e recebimento de mensagens em tempo real
- Broadcast de mensagens para todos os clientes conectados
- Fácil de instalar e usar

---

## ⚡ Instalação

Se você estiver usando **Node.js**, basta instalar via npm:

```bash
npm install @arthurdevfrontend/miniwebsocket

```

ou, se usar _Yarn_

```bash
yarn add @arthurdevfrontend/miniwebsocket
``` 

Prontinho! Agora a blibioteca está instalada 🎉

# Uso Básico🧩

1️⃣ Criar o servidor

Crie um arquivo chamado `server.js` e escreva assim:

```javascript

const { WebSocketServer } = require("arthurdevfrontend/miniwebsocket)

// Criar o servidor na porta 8080
const server = new WebSocketServer({ port: 8080});

// Quando alguém se conectar
server.on("connection", (socket) => {
    console.log("Alguém se conectou!")

    // Receber mensagem de um cliente
    socket.on("message", (msg) => {
        console.log("Mensagem Recebida")


        // Mandar a mensagem para todo mundo
        server.broadcast(`Alguem disse: ${msg}`);

    });



    socket.send("Bem vindo ao MiniWebSocket")
});
```

# 2️⃣ Criar o Cliente (Node.js)

Crie um arquivo chamado `Client.js`

```javascript
const { WebSocket } = require("@arthurdevfrontend/miniwebsocket")

// Conectar ao servidor
const socket = new WebSocket("ws://localhost:8080",{
  reconnectInterval: 3000,
  maxReconnectAttempts: 10
});

// Quando receber mensagem
socket.on("message", (msg) => {
  console.log("Servidor diz:", msg);
});

// Mandar mensagem para o servidor
socket.send("Oi, servidor!");
```



# 3️⃣ Rodar
No terminal primeiro rode o servidor:
```bash
node server.js

```
Depois em outro terminal rode o cliente
```bash
node client.js
```

# 4️Testando recursos extras do MiniWebSocket
- *Broadcast:* envia para todos os clientes:

```javascript
server.broadcast("Mensagem global pra todos!")
```
- Salas(Rooms):
```javascript

socket.joinRoom("sala1")
socket.sendToRoom("sala1", "Mensagem só pra essa sala");
```
- *Ping:* testar se o cliente está online
```javascript
socket.ping();
```
- Reconexão automática: se o cliente perder a conexão ele tentar reconectar sozinho,
conforme você definiu no `reconnectInterval` e `maxReconnectAttempts`.
Você vera mensagem rodando em tempo real!🥳

🎯Dicas fáceis para começar
- Pense Que Cada Cliente e um amiguinho para conversar
- `send()` manda mensagem
- `on("message", ...)` escuta quando alguém manda mensagem
- `broadcast()`manda mensagem para todos tudo de uma vez.
Com isso voce consuege criar um chat divertido ou avisos em tempo real🐱‍👤 


💡 Dica final: Pense nos WebSockets como um telefone mágico, onde todo mundo pode falar e ouvir ao mesmo tempo, sem presisar desligar e ligar o telefone. 📞 
