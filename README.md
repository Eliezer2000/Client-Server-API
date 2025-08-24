# Desafio Go: Client & Server com Context, HTTP e SQLite 💻
![Go](https://img.shields.io/badge/Go-1.22-blue)
![SQLite](https://img.shields.io/badge/SQLite-3-lightgrey)
![HTTP](https://img.shields.io/badge/Protocol-HTTP%2F1.1-green)
## 📌 Sobre o desafio
Este desafio tem como objetivo aplicar conceitos fundamentais do desenvolvimento backend com **Golang**, incluindo:
- Servidor HTTP
- Uso de **contextos com timeout**
- Integração com API externa
- Persistência de dados em **SQLite**
- Manipulação de arquivos
O sistema é composto por **dois programas em Go**:
- `server.go`: responsável por consumir a API de câmbio e registrar as cotações no banco.
- `client.go`: responsável por requisitar o valor da cotação ao servidor e salvar em um arquivo de texto.
---
## 📋 Requisitos do desafio
### Servidor (`server.go`)
- Disponibilizar o endpoint `/cotacao` na porta `8080`
- Consumir a API [AwesomeAPI](https://economia.awesomeapi.com.br/json/last/USD-BRL)
- Usar **timeout de 200ms** para a chamada da API externa
- Usar **timeout de 10ms** para salvar os dados no banco SQLite
- Persistir cada cotação recebida no banco `cotacao.db`
- Retornar ao cliente apenas o valor da cotação (`bid`) em JSON
### Cliente (`client.go`)
- Requisitar `GET http://localhost:8080/cotacao` ao servidor
- Usar **timeout de 300ms** para a requisição
- Salvar a resposta em um arquivo `cotacao.txt` no formato:
  ```
  Dólar: {valor}
  ```
### Tratamento de Erros
- Todos os contextos devem logar erro caso o tempo seja insuficiente
---
## 📂 Estrutura do projeto
```
desafio_client_server_api/
├── client/
│   └── client.go
├── server/
│   └── server.go
├── cotacao.db          # Gerado automaticamente pelo server
├── cotacao.txt         # Gerado automaticamente pelo client
└── README.md
```
---
## ▶️ Como executar
### 1. Rodar o servidor
No diretório `server/`:
```bash
go run server.go
```
O servidor será iniciado em:
```
http://localhost:8080/cotacao
```
### 2. Rodar o cliente
Em outro terminal, no diretório `client/`:
```bash
go run client.go
```
Isso vai gerar o arquivo `cotacao.txt` contendo a cotação atual do dólar.
---
## 📖 Exemplo de fluxo
### Requisição do client
```
GET http://localhost:8080/cotacao
```
### Resposta do server (JSON)
```json
{
  "bid": "5.4321"
}
```
### Arquivo gerado pelo client (`cotacao.txt`)
```
Dólar: 5.4321
```
---
## 🛠 Tecnologias utilizadas
- **Go** 1.22
- **SQLite3**
- **AwesomeAPI** - USD/BRL
- **Context API do Go** (context)
---
## 📌 Observações
- Caso os timeouts sejam atingidos, mensagens de erro serão exibidas no log
- O banco `cotacao.db` será criado automaticamente na primeira execução do servidor
---
## 👨‍💻 Autor
Desenvolvido por Eliézer Alves 🚀
