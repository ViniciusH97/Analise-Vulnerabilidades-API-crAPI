# Reconhecimento da Aplicação

Este diretório contém as atividades relacionadas à **coleta de inteligência** durante os testes de segurança na aplicação crAPI, em um ambiente de laboratório local.

## Objetivo

O objetivo desta fase do pentest é mapear, identificar e documentar informações relevantes sobre a aplicação para suportar etapas posteriores de análise de vulnerabilidades, ataques e exploração, respeitando que todo o teste ocorre em **ambiente controlado e local**.

## Escopo

- Ambiente: **localhost** (crAPI rodando localmente via Docker)
- Métodos: **reconhecimento ativo** da aplicação
- Ferramentas utilizadas: `curl`, `Postman`, `DevTools`.
- Não envolve endpoints públicos ou coleta externa

## Atividades realizadas

1. **Mapeamento de rotas e endpoints da API**
   - Identificação de todos os recursos disponíveis no servidor local
   - Análise de métodos HTTP suportados (GET, POST, PUT, DELETE, etc.)
   - Documentação de parâmetros de entrada e formatos de resposta

2. **Análise de respostas HTTP e headers**
   - Investigação de headers de segurança (`Content-Security-Policy`, `X-Frame-Options`, etc.)
   - Identificação de informações potencialmente sensíveis em respostas

3. **Captura e inspeção de tráfego**
   - Utilização de Wireshark e Burp Suite para análise de pacotes
   - Observação de padrões de comunicação e dados trafegados

4. **Registro e documentação**
   - Todas as descobertas foram registradas para servir de base para análise de vulnerabilidades
   - Organização dos dados por recurso e tipo de informação

## Referência MITRE ATT&CK

Mesmo em ambiente local, este trabalho pode ser mapeado conceitualmente para técnicas de **Reconnaissance** e **Discovery** da matriz MITRE ATT&CK, como:

- **T1595 – Active Scanning:** exploração de rotas e endpoints internos disponíveis
- **T1087 – Account Discovery:** levantamento de informações de usuários e dados visíveis via API
- **T1609 – Container and Resource Discovery:** análise do ambiente local e recursos da aplicação

> O mapeamento MITRE é conceitual, para ilustrar como atividades de reconhecimento interno se relacionam com técnicas utilizadas em ataques reais.
