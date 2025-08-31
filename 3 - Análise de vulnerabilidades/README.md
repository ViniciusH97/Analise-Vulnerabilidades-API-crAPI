# Análise de Vulnerabilidades

Este diretório contém as atividades relacionadas à **análise de vulnerabilidades** na aplicação crAPI, em ambiente de laboratório local.

## Objetivo
Registrar, documentar e analisar vulnerabilidades na aplicação, com foco em autenticação, autorização, validação de entrada e segurança de configuração.

## Escopo
- Ambiente: localhost (crAPI rodando via Docker)  
- Testes focados em endpoints internos da aplicação  
- Ferramentas utilizadas: `Burp Suite`, `Postman`, `Nikto`, `Nmap`, `curl`, `DevTools`, entre outras

## Atividades realizadas

### 1. Teste de Autenticação
- Objetivo: verificar falhas na validação de tokens ou senhas
- Atividades:
  - Teste de brute-force em endpoints de login
  - Verificação de bypass de autenticação
- Ferramentas: `Burp Suite`, `Postman`
- Evidências:
  - ![print]()
  - Logs de erros relevantes: `path/para/log.txt`

### 2. Teste de Autorização
- Objetivo: identificar escalonamento de privilégios ou acesso não autorizado
- Atividades:
  - Acesso a endpoints restritos sem permissão
  - Teste de roles e privilégios
- Ferramentas: `Burp Suite`, `Postman`
- Evidências:
  - ![print]()
  - Snippet de request/response:  
  ```http
  GET /admin HTTP/1.1
  Host: localhost
  Authorization: Bearer <token_test>
  ``` 
