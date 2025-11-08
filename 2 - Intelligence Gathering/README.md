# Intelligence Gathering

Este diretório contém as atividades relacionadas à **coleta de inteligência** durante os testes de segurança na aplicação crAPI, em um ambiente de laboratório local.

## 1. Objetivo

O objetivo desta fase do pentest é mapear, identificar e documentar informações relevantes sobre a aplicação para suportar etapas posteriores de análise de vulnerabilidades, ataques e exploração, respeitando que todo o teste ocorre em **ambiente controlado e local**.

## 2. Escopo

- Ambiente: **Rede Interna** (crAPI rodando localmente via Docker), no meu caso, utilizei o ip da máquina virtual com Ubuntu Server.
- Métodos: **reconhecimento ativo** da aplicação
- Ferramentas utilizadas: `curl`, `wget`, `DevTools`,`nikto`, entre outros.
- Não envolve endpoints públicos ou coleta externa

---

## 3. Atividades realizadas

### 3.1 Analise na documentação da crAPI para entender a lógica de negócio e endpoints esperados

### 3.1.1 A lógica da aplicação:

Após analisar o arquivo `crapi-openapi-spec.json`, foi possível identificar que a aplicação crAPI simula uma plataforma para gerenciamento de veículos. A lógica de negócio é dividida em módulos principais: 

- Identidade (autenticação e gerenciamento de usuários);
- Veículos;
- Comunidade (fórum e cupons); e
- Workshop (loja e mecânicos)

A seguir, o detalhamento das principais funcionalidades e seus respectivos endpoints.

---

## 4. Identificação dos Endpoints da documentação

### 4.1. Módulo de Identidade e Autenticação
Este módulo gerencia todo o ciclo de vida do usuário, desde o cadastro até a recuperação de senha.

Criação de Conta de Usuário
O usuário cria a conta no crAPI utilizando o endpoint `/identity/api/auth/signup`

**Objetos enviados:**

- email (tipo: string) 
- name (tipo: string) 
- number (tipo: string) 
- password (tipo: string) 

**Método:** POST 

Respostas possíveis:

- 200: "User successfully registered" 
- 403: Descrição não disponível 
- 500: Descrição não disponível 

--- 
**Login de Usuário**

Para se autenticar, o usuário utiliza o endpoint `/identity/api/auth/login`

**Objetos enviados:**
- email (tipo: string) 
- password (tipo: string) 

**Método:** POST 

Respostas possíveis:

- 200: Retorna um token JWT para ser usado em requisições autenticadas.
- 500: Descrição não disponível 
---
### 4.3. Módulo de Veículos
Após o login, o usuário pode gerenciar seus veículos.

**Adicionar um Novo Veículo**
O usuário adiciona um veículo à sua conta pelo endpoint `/identity/api/v2/vehicle/add_vehicle`

Objetos enviados:
- pincode (tipo: string) 
- vin (tipo: string) 

**Método:** POST 

Segurança: Requer autenticação via bearerAuth (token JWT).

**Respostas possíveis:**
- 200: Veículo adicionado com sucesso.
- 403: Acesso proibido/não autorizado.
---
**Obter Localização do Veículo**
É possível consultar a localização de um veículo específico via endpoint `/identity/api/v2/vehicle/{vehicleId}/location`

Parâmetro na URL:
- vehicleId (tipo: string, formato: uuid) 

**Método:** GET 

**Segurança:** Requer autenticação via bearerAuth (token JWT).

**Respostas possíveis:**
- 200: Retorna os dados de localização.
- 404: "Invalid vehicle_id for User" 
---
### 4.4. Módulo de Comunidade (Fórum)
A aplicação possui um fórum onde usuários autenticados podem interagir.

**Criar uma Nova Postagem**
Usuários criam posts no fórum através do endpoint `/community/api/v2/community/posts`

**Objetos enviados:**
- content (tipo: string) 
- title (tipo: string) 

**Método:** POST 

**Segurança:** Requer autenticação via bearerAuth (token JWT).

**Respostas possíveis:**
- 200: Retorna o post recém-criado com detalhes do autor.
---
### 4.5. Módulo de Workshop (Loja)
Usuários podem comprar produtos e gerenciar pedidos.

**Criar um Pedido**
Para comprar um produto, a aplicação utiliza o endpoint `/workshop/api/shop/orders`

**Objetos enviados:**
- product_id (tipo: integer) 
- quantity (tipo: integer) 

**Método:** POST 

**Segurança:** Requer autenticação via bearerAuth (token JWT).

**Respostas possíveis:**
- 200: "Order sent successfully." 
- 400: "Insufficient Balance. Please apply coupons to get more balance!" 
---
### 4.6. Módulo Administrativo **(Ponto de Atenção)**
Existem endpoints que deveriam ser restritos a administradores.

**Deletar Vídeo de Perfil (Admin)**
Um endpoint específico para deletar vídeos de usuários é o `/identity/api/v2/admin/videos/{video_id}`

**Descrição:** "_Delete profile video of other users by video_id as admin_".

Parâmetro na URL:
- video_id (tipo: integer) 

**Método**: DELETE 

**Segurança:** Requer autenticação via bearerAuth (token JWT).

**Respostas possíveis:**
- 200: OK 
- 403: "Forbidden" 
- 404: "Video not found"
---

### 4.7. Realizar o mapeamento de rede do servidor da API
   - Identificar portas
   - Identificar serviçoes expostos

**Ferramenta utilizada:** `nmap`

<img width="760" height="599" alt="Captura de tela 2025-09-14 162206" src="https://github.com/user-attachments/assets/cc08fee4-076f-49ff-b623-606935e42dc7" />
/>

Após o mapeamento com o uso do `nmap`, foi possível identificar as portas abertas 22 (SSH), 8080, 8087, 8443 e 8888 (interface web principal). O reconhecimento da rede foi concluído e a superfície de ataque inicial foi mapeada com sucesso.

---

**Mapeamento de rotas e endpoints da API**
   - Identificação de todos os recursos disponíveis no servidor local
   - Análise de métodos HTTP suportados (GET, POST, PUT, DELETE, etc.)
   - Documentação de parâmetros de entrada e formatos de resposta.

### 5. Reconhecimento de Endpoints DevTools

<img width="1358" height="730" alt="image" src="https://github.com/user-attachments/assets/bc4bd09b-a8e3-4419-a9cb-885e19e92acd" />

---

Identificação de método POST em login, endpoint `/identify/api/auth/login/`:

<img width="1173" height="554" alt="image" src="https://github.com/user-attachments/assets/7982803f-be75-43b4-8508-92840e3528fd" />

--- 

Neste teste foi utilizado um e-mail e senha não cadastrado para mapear o endpoint, resultando no _Response_:

<img width="833" height="374" alt="image" src="https://github.com/user-attachments/assets/19c58a0f-664a-410f-b2e9-8b968d4fc4d7" />

_Request_ em estrutura JSON:

```json
{
   "email": "usuarioteste@gmail.com",
   "password": "12345678"
}
```

---

_Request_ com usuário e senha cadastrados:

<img width="1026" height="521" alt="image" src="https://github.com/user-attachments/assets/3682cb94-a971-4526-ae37-8ccec398bf0e" />

---

_Response_ do endpoint de login:

<img width="979" height="542" alt="image" src="https://github.com/user-attachments/assets/1247e8e7-ec97-452a-a9d8-0a42f979793c" />

Ao realizar o login, a aplicação retorna um token JWT sem assinatura digital

---

Identificação de endpoints com o método GET `/dashboard`:

<img width="969" height="533" alt="image" src="https://github.com/user-attachments/assets/5dc1017f-5f33-405d-b81d-a4d28267478f" />

---

Identificação do endpoint método GET `/vehicles`:

<img width="950" height="443" alt="image" src="https://github.com/user-attachments/assets/62493fe1-ea35-4cae-b4ce-73e2f0c8176d" />

---

## Reconhecimento com o Postman

Após o mapeamento dos endpoints da aplicação, foi utilizado o Potman para tentar as requisições e estudar o comportamento das rotas, analisando o corpo no request e response.

<img width="1359" height="595" alt="teste com o Postman" src="https://github.com/user-attachments/assets/a7069a67-3081-43cf-9116-b78f0f42c0f2" />

## Reconhecimento com o BurpSuite

Identificação do endpoint POST identity/api/auth/siqnup:

<img width="1157" height="616" alt="Captura de tela 2025-09-14 203447" src="https://github.com/user-attachments/assets/1e1af21a-264e-46ff-9859-9ca94b283cfd" />

Identificação do endpoint /workshop/api/mechanic/

<img width="1366" height="729" alt="Captura de tela 2025-09-14 213800" src="https://github.com/user-attachments/assets/55cfb467-75f0-49fe-9bd9-c78ece74fbe1" />

### 6. Endpoints encontrados:

Utilizando a ferramenta Burp Suite como proxy, foi realizada a navegação completa na aplicação crAPI. Todas as funcionalidades foram executadas, incluindo criação de contas, login, adição de veículos, interação com a loja e com a comunidade. O tráfego HTTP/S foi capturado e analisado para validar a documentação e buscar por endpoints não documentados.

### 7. Tabela de Endpoints Descobertos

A tabela a seguir consolida todos os endpoints identificados durante o mapeamento ativo. A análise confirmou que a implementação atual da API está alinhada com sua documentação oficial.

| Módulo | Endpoint e Método | Funcionalidade Descrita | Requer Autenticação? |
| :--- | :--- | :--- | :--- |
| **Identidade** | `POST /identity/api/auth/signup` | Cria uma nova conta de usuário. | Não |
| **Identidade** | `POST /identity/api/auth/login` | Autentica um usuário e retorna um token JWT. | Não |
| **Identidade** | `GET /identity/api/v2/user/dashboard` | Retorna os detalhes do perfil do usuário logado. | Sim (JWT) |
| **Identidade** | `POST /identity/api/v2/user/change-email` | Inicia o processo de alteração de e-mail do usuário. | Sim (JWT) |
| **Identidade** | `POST /identity/api/v2/user/verify-email-token` | Confirma a alteração de e-mail com um token. | Sim (JWT) |
| **Identidade** | `POST /identity/api/v2/user/reset-password`| Reseta a senha do usuário logado. | Sim (JWT) |
| **Veículos** | `GET /identity/api/v2/vehicle/vehicles` | Lista os veículos associados ao usuário logado. | Sim (JWT) |
| **Comunidade**| `POST /community/api/v2/community/posts` | Cria uma nova postagem no fórum. | Sim (JWT) |
| **Comunidade**| `GET /community/api/v2/community/posts/recent`| Lista as postagens recentes do fórum. | Sim (JWT) |
| **Workshop** | `GET /workshop/api/mechanic/` | Lista os mecânicos disponíveis. | Sim (JWT) |
| **Workshop** | `POST /workshop/api/shop/orders` | Realiza a compra de um item da loja. | Sim (JWT) |
| **Workshop** | `POST /workshop/api/shop/orders/return_order`| Inicia a devolução de um item comprado. | Sim (JWT) |

---

### 8. Análise de respostas HTTP e headers
   - Investigação de headers de segurança (`Content-Security-Policy`, `X-Frame-Options`, etc.)
   - Identificação de informações potencialmente sensíveis em respostas

**Ferramenta utilizada:** `curl`

###$ 8.1. Coleta dos headers:

```bash
curl -I http:/192.168.1.19:8888
```

**Ferramenta utilizada:** `wget`

```bash
wget --server-response --spider http://192.168.1.10:8888
```

<img width="846" height="689" alt="image" src="https://github.com/user-attachments/assets/3a2c2223-1f69-45c6-8edc-3721f6ac401b" />

--- 

**Ferramenta utilizada:** `nikto`

<img width="838" height="589" alt="image" src="https://github.com/user-attachments/assets/0535de43-dd2a-46be-a25c-d1c7822976ce" />

<img width="793" height="529" alt="image" src="https://github.com/user-attachments/assets/bbadd93d-76c7-461e-98f7-b3ab818b02ef" />

| Recurso / Cabeçalho     | Descrição             | Relevância / Impacto             |
| --------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| `Server: openresty/1.25.3.1`    | Versão do servidor identificada     | Possível exploração de vulnerabilidades conhecidas dessa versão |
| Cabeçalhos de segurança ausentes (`X-Frame-Options`, `X-Content-Type-Options`)    | Configurações de proteção contra clickjacking e MIME sniffing não configuradas | Indica falta de proteção e potenciais vetores de ataque         | Arquivos de backup/certificados expostos (`.tar`, `.cer`, `.pem`, `.jks`, `.war`, `.alz`) | Arquivos encontrados acessíveis via HTTP                                       | Podem conter credenciais, chaves privadas ou dados sensíveis    |
| Arquivo `.env`        | Arquivo de configuração contendo possíveis credenciais    | Alta pois expõe segredos da aplicação  | IP interno exposto (`172.18.0.9`)    | IP revelado em header `Location`    | Permite mapear arquitetura interna da rede        |
| Scripts antigos ou padrão (`/cgi/cgiproc?`, `/isapi/count.pl?`)   | Scripts que podem ser explorados para DoS ou execução remota       | Possível vetor de ataque em testes posteriores                  |

---

Todas as descobertas foram registradas para servir de base para análise de vulnerabilidades e a organização dos dados por recurso e tipo de informação

### 9. Conclusão da Fase de Reconhecimento

A fase de *Intelligence Gathering* foi concluída com sucesso. A superfície de ataque da API foi completamente mapeada e documentada. Com este conhecimento detalhado, o projeto avança para a próxima fase: **Threat Modeling**, onde estes endpoints serão analisados em nível de criticidade.
