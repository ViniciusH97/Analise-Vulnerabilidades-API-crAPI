# TCC - Análise de Vulnerabilidades em Autenticação e Autorização em APIs RESTful (crAPI)

Este repositório documenta o projeto de Trabalho de Conclusão de Curso (TCC) com foco na identificação e exploração de vulnerabilidades críticas em APIs RESTful, utilizando a aplicação vulnerável chamada crAPI desenvolvida pela OWASP. Está aplicação foi criada de forma vulnerável propositalmente.

## Objetivo

Demonstrar de forma prática, como vulnerabilidades como **Broken Object Level Authorization (BOLA)** e **Broken Authentication**, podem ser exploradas por atacantes, e apresentar boas práticas de mitigação baseadas no OWASP Top 10.

---

## Metodologia Utilizadas

A metodologia se seguirá pelos preceitos do PTES (Penetration Testing Execution Standard), que auxiliará em uma análise mais técnica e eficiente dos testes. O metódo de teste seguirá com testes manuais com uso de ferramentas e scripts com o conhecimento parcial da aplicação crAPI (gray-box).

Sessões da norma PTES:

- [Pre-engagement Interactions](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/1%20-%20Pre-engagement%20interections)
- [Intelligence Gathering](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/2%20-%20Intelligence%20Gathering)
- [Threat Modeling](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/3%20-%20Threat%20Modeling)
- [Vulnerability Analysis](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/4%20-%20Vulnerability%20Analysis)
- [Exploitation](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/4%20-%20Vulnerability%20Analysis)
- [Post Exploitation](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main/6%20-%20Post%20Exploitation)
- [Reporting](https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI/tree/main)

## Tecnologias Utilizadas

- Docker e Docker Compose
- Ferramentas de Pentest: Burp Suite, Nmap, Hydra, Postman, Nikto, wget entre outros.
- PostgreSQL/MySQL (no backend da crAPI)

---

## Referências
- [PTES (Penetration Testing Execution Standard)](http://www.pentest-standard.org/index.php/Main_Page)
- [OWASP Top 10 - API Security](https://owasp.org/www-project-api-security/)
- [crAPI - Completely Ridiculous API](https://github.com/OWASP/crAPI)
- [Meu Fork do Projeto do crAPI ajustado para o trabalho](https://github.com/ViniciusH97/crAPI.git)
- [Introdução ao Pentest 2º Edição - Daniel Moreno](https://www.novatec.com.br/livros/introducao-pentest-2ed/)
- [Engenharia de Software - Pressman e Maxim](https://books.google.com.br/books/about/Engenharia_de_software_9_ed.html?id=FSE3EAAAQBAJ&redir_esc=y)
- [Hacking APis - Corey Ball](https://www.oreilly.com/library/view/hacking-apis/9781098130244/)

---

## Aviso 

Este projeto foi desenvolvido para fins de pesquisa e para o trabalho de conclusão do curso, voltado em análise de segurança aos mecanismos de autenticação e autorização em APIs RESTful. Nenhuma técnica aqui documentada deve ser usada em ambientes reais sem autorização.

## Licenças

<a href="https://github.com/ViniciusH97/Analise-Vulnerabilidades-API-crAPI">Analise-Vulnerabilidades-API-crAPI</a> © 2025 by <a href="https://github.com/ViniciusH97">ViniciusH97</a> is licensed under <a href="https://creativecommons.org/licenses/by-nc/4.0/">CC BY-NC 4.0

[![CC BY-NC 4.0][cc-by-nc-image]][cc-by-nc]

[cc-by-nc]: https://creativecommons.org/licenses/by-nc/4.0/
[cc-by-nc-image]: https://licensebuttons.net/l/by-nc/4.0/88x31.png
[cc-by-nc-shield]: https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg

**Trechos do OWASP API Security Top 10**: © OWASP Foundation, CC BY-SA 4.0 ([docs/OWASP-API-Top10.md](docs/OWASP-API-Top10.md))
