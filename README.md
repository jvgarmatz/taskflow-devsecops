# Relatório de Análise e Práticas de DevSecOps - TaskFlow

## 1. O que é "Shift-Left Security"?
O conceito de **Shift-Left Security** (ou "segurança à esquerda") significa trazer as preocupações, testes e boas práticas de segurança para as etapas mais iniciais do ciclo de desenvolvimento de software (planejamento, design e escrita do código), em vez de deixá-las apenas para a fase final de testes ou quando a aplicação já está em produção.

## 2. Vulnerabilidades identificadas no TaskFlow
Analisando o código do **TaskFlow**, uma das falhas mais evidentes é o **armazenamento de senhas em texto puro** no banco de dados SQLite (`admin123` e `senha123`), além da **chave de sessão (`SECRET_KEY`) exposta diretamente no código-fonte** (`app.py`). 

**Por que isso é um problema?**
* **Senhas em texto puro:** Caso alguém consiga acessar o arquivo do banco de dados, terá acesso imediato e legível a todas as senhas dos usuários, sem precisar quebrar nenhuma criptografia ou hash.
* **Segredo hardcoded:** Se o repositório for compartilhado ou vazado, qualquer pessoa pode usar essa chave para forjar sessões e se passar por outro usuário dentro do sistema.

## 3. Por que deixar a segurança para o final é arriscado?

* **Custo elevado:** Corrigir uma falha estrutural (como remodelar a autenticação ou o banco de dados) com o sistema já pronto custa muito mais tempo e dinheiro do que fazê-lo desde o início.
* **Atrasos no lançamento:** Identificar brechas críticas às vésperas da entrega pode paralisar o projeto ou forçar um lançamento inseguro sob pressão de prazos.
* **Exposição a incidentes:** Falhas que passam despercebidas para produção podem gerar vazamento de dados, danos à reputação da empresa e sanções legais.