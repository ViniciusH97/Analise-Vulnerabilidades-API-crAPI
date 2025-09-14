# Reconhecimento da Aplicação

Este diretório contém as atividades relacionadas à **coleta de inteligência** durante os testes de segurança na aplicação crAPI, em um ambiente de laboratório local.

## 1. Objetivo

O objetivo desta fase do pentest é mapear, identificar e documentar informações relevantes sobre a aplicação para suportar etapas posteriores de análise de vulnerabilidades, ataques e exploração, respeitando que todo o teste ocorre em **ambiente controlado e local**.

## 2. Escopo

- Ambiente: **localhost** (crAPI rodando localmente via Docker), no meu caso, utilizei o ip da máquina virtual com Ubuntu Server.
- Métodos: **reconhecimento ativo** da aplicação
- Ferramentas utilizadas: `curl`, `wget`, `DevTools`,`nikto`, entre outros.
- Não envolve endpoints públicos ou coleta externa

---

## 3. Atividades realizadas

### 3.1 Realizar o mapeamento de rede do servidor da API
   - Identificar portas
   - Identificar serviçoes expostos

**Ferramenta utilizada:** `nmap`

<img/>

Após o mapeamento com o uso do `nmap`, foi possível identificar as portas abertas 22 (SSH), 8080, 8087, 8443 e 8888 (interface web principal). O reconhecimento da rede foi concluído e a superfície de ataque inicial foi mapeada com sucesso.

---

**Mapeamento de rotas e endpoints da API**
   - Identificação de todos os recursos disponíveis no servidor local
   - Análise de métodos HTTP suportados (GET, POST, PUT, DELETE, etc.)
   - Documentação de parâmetros de entrada e formatos de resposta.

### 3.2 Tela de Login - Aplicação crAPI:

**Ferramenta utilizada:** `DevTools`

<img width="1358" height="730" alt="image" src="https://github.com/user-attachments/assets/bc4bd09b-a8e3-4419-a9cb-885e19e92acd" />

---

Identificação de método POST em login, endpoint `/identify/api/auth/login/`:

<img width="1173" height="554" alt="image" src="https://github.com/user-attachments/assets/7982803f-be75-43b4-8508-92840e3528fd" />

--- 

Neste teste foi utilizado um e-mail e senha não cadastrado para mapear o endpoint, resultando no _Response_:

<img width="833" height="374" alt="image" src="https://github.com/user-attachments/assets/19c58a0f-664a-410f-b2e9-8b968d4fc4d7" />

**Acrescentar**(Testar os casos de e-mail valido com senha inválida)

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

### 3.2.1 Endpoints encontrados:

1. `/identify/api/auth/login/`
2. `/identity/api/v2/user/dashboard`
3. `/identity/api/v2/vehicle/vehicles`

---

### 3.3. Análise de respostas HTTP e headers
   - Investigação de headers de segurança (`Content-Security-Policy`, `X-Frame-Options`, etc.)
   - Identificação de informações potencialmente sensíveis em respostas

**Ferramenta utilizada:** `curl`

### 1. Coleta dos headers:

```bash
curl -I http:/192.168.0.110:8888
```

<img width="708" height="417" alt="image" src="https://github.com/user-attachments/assets/3d52c29f-6610-4f40-a449-ba2ec6b5a273" />

---

**Ferramenta utilizada:** `wget`

<img width="683" height="491" alt="image" src="https://github.com/user-attachments/assets/ce692ea9-69aa-4ba0-8453-10d3507f1f19" />

--- 

**Ferramenta utilizada:** `nikto`

<img width="793" height="529" alt="image" src="https://github.com/user-attachments/assets/bbadd93d-76c7-461e-98f7-b3ab818b02ef" />

**Acrescentar** [Descrição da análise com nikto]

### 2. Análise dos Headers

- `Server: openresty/1.25.3.1` → expõe tecnologia e versão do servidor (**fingerprinting**).
- Ausência de `Content-Security-Policy` → aplicação vulnerável a **XSS**.
- Ausência de `X-Frame-Options` → risco de **clickjacking**.
- Ausência de `Strict-Transport-Security (HSTS)` → risco de downgrade de HTTPS → HTTP.
- Ausência de `X-Content-Type-Options` → pode permitir **MIME sniffing**.
- Presença de `Cache-Control: no-store, no-cache, must-revalidate` → **ponto positivo**, evita cache de conteúdo sensível.

---

Todas as descobertas foram registradas para servir de base para análise de vulnerabilidades e a organização dos dados por recurso e tipo de informação

## Referência MITRE ATT&CK

Mesmo em ambiente local, este trabalho pode ser mapeado conceitualmente para técnicas de **Reconnaissance** e **Discovery** da matriz MITRE ATT&CK, como:

- **T1595 – Active Scanning:** exploração de rotas e endpoints internos disponíveis
- **T1087 – Account Discovery:** levantamento de informações de usuários e dados visíveis via API
- **T1609 – Container and Resource Discovery:** análise do ambiente local e recursos da aplicação

> O mapeamento MITRE é conceitual, para ilustrar como as atividades de reconhecimento interno podem se relacionar com técnicas utilizadas em ataques reais.
