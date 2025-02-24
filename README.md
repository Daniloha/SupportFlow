___
# SupportFlow

Sistema de gestão de chamados com painel de controle, padronização de tratativas, acompanhamento de status e integração com ferramentas externas como **Calc** e **Kanbanize**.

## 📄 Sobre o Projeto

O **SupportFlow** é uma solução completa para o **gerenciamento de chamados**, focada em otimizar o atendimento, monitorar o fluxo de trabalho e facilitar a comunicação entre equipes. Com uma interface intuitiva e recursos voltados para eficiência, o sistema permite:

- **Criação, acompanhamento e encerramento de chamados** em tempo real.  
- **Geração de relatórios** para análise de desempenho e tomada de decisões.  
- **Integração com ferramentas externas**, como **Calc** para exportação de dados e **Kanbanize** para gerenciamento visual dos chamados.

Desenvolvido com **ASP.NET Core**, o projeto prioriza **escalabilidade**, **segurança** e **flexibilidade**, sendo ideal para equipes que buscam um controle eficiente dos processos de atendimento.

___

## 📂 Estrutura do Projeto

```
SupportFlow.sln
│── /SupportFlow.Api             -> API e Configuração
│── /SupportFlow.Application     -> Casos de Uso, Handlers, Perfis do AutoMapper, Serviços e DTOs
│── /SupportFlow.Domain          -> Entidades, VOs, Repositórios (somente interfaces) e Regras de Negócio
│── /SupportFlow.Infrastructure  -> Contexto, Implementação dos Repositórios e Configuração do EF Core
│── /SupportFlow.Shared          -> Enums, Requests, Responses, Paginação, etc.
│── /tests
│   │── /SupportFlow.Api.Test             -> Testes da API
│   │── /SupportFlow.Application.Test     -> Testes de Casos de Uso e Serviços
│   │── /SupportFlow.Domain.Test          -> Testes de Domínio (Entidades e VOs)
│   │── /SupportFlow.Infrastructure.Test  -> Testes do Repositório e Banco de Dados
```

___

## ✅ Checklist de Desenvolvimento

### 1️⃣ - Criar a Solução e Projetos
1. 🔲 **Criar a solução no .NET**
2. 🔲 **Adicionar os projetos à solução**
3. 🔲 **Configurar referências entre os projetos**

### 2️⃣ - Definir o Domínio (SupportFlow.Domain)
1. 🔲 **Criar Entidades**  
   - Chamado  
   - Analista  
   - GuiaPadronizacao  
   - Escalonamento  
   - Status  
2. 🔲 **Criar Value Objects (VOs) se necessário**
3. 🔲 **Criar Interfaces de Repositórios**
4. 🔲 **Criar Exceções de Domínio (DomainException)**
5. 🔲 **Criar Regras de Negócio dentro das entidades**

### 3️⃣ - Criar Casos de Uso (SupportFlow.Application)
1. 🔲 **Criar DTOs**  
2. 🔲 **Criar Interfaces de Serviços**
3. 🔲 **Criar Implementação de Serviços**
4. 🔲 **Criar Handlers (se usar CQRS)**
5. 🔲 **Configurar AutoMapper para converter Entidades <-> DTOs**

### 4️⃣ - Implementar a Infraestrutura (SupportFlow.Infrastructure)
1. 🔲 **Criar o DbContext com Entity Framework Core**
2. 🔲 **Configurar Entidades com Fluent API**
3. 🔲 **Implementar os Repositórios**
4. 🔲 **Criar Migrations e Atualizar o Banco**

### 5️⃣ - Criar a API e Configurar Dependências (SupportFlow.Api)
1. 🔲 **Criar o Program.cs com Minimal API**
2. 🔲 **Configurar Injeção de Dependência (DI)**
3. 🔲 **Adicionar Swagger**
4. 🔲 **Criar Endpoints:**  
   - Registro de chamados  
   - Consultas e atualizações  
   - Gestão de escalonamentos  
   - Padrões de tratativas  
5. 🔲 **Criar Middlewares (tratamento de erro, logs, autenticação, etc.)**
6. 🔲 **Adicionar Autenticação e Autorização**
7. 🔲 **Implementar Integração com Calc e Kanbanize**

### 6️⃣ - Criar Testes
#### 🟠 Testes de Unidade
1. 🔲 **Testes para Entidades e Regras de Negócio (SupportFlow.Domain.Test)**
2. 🔲 **Testes para Serviços e Casos de Uso (SupportFlow.Application.Test)**

#### 🔵 Testes de Integração
1. 🔲 **Testes para Repositórios (SupportFlow.Infrastructure.Test)**
2. 🔲 **Testes para Endpoints da API (SupportFlow.Api.Test)**

### 7️⃣ - Configurar CI/CD e Publicação
1. 🔲 **Criar um Dockerfile**
2. 🔲 **Configurar pipeline CI/CD (GitHub Actions ou Azure DevOps)**
3. 🔲 **Publicar a API em um ambiente (ex: Railway, Azure, AWS, Render)**

___

## 📊 Funcionalidades Principais

- **Cadastro e Gerenciamento de Chamados:**  
  Inclui tipo, motivo, datas, descrição, ação tomada e tratativa.

- **Dashboard Interativo:**  
  - Total de chamados atendidos  
  - Gráficos de motivos recorrentes (Pizza)  
  - Tipos predominantes (Barras verticais)

- **Gerenciamento de Status:**  
  Definição de status do analista (Online, Almoço, Ocupado, Ausente, Offline).

- **Escalonamento de Chamados:**  
  Registro de chamados escalonados, destino, data, CPF e observações.

- **Guia de Padronização de Respostas:**  
  Inclui tipos, motivos, ações e tratativas recomendadas, além de passo a passo para casos complexos.

- **Integração com Calc e Kanbanize:**  
  - **Calc:** Exportação de relatórios e dados para planilhas.  
  - **Kanbanize:** Sincronização de chamados com quadros kanban para visualização de fluxos de trabalho.

- **Limpeza Mensal Automática:**  
  No primeiro dia de cada mês, os dados do mês anterior são arquivados e a base atual é limpa.

___

## 📐 Diagrama de Dependências

```
SupportFlow.Api        --->  SupportFlow.Application  --->  SupportFlow.Domain
       |                          |                          |
       v                          v                          v
SupportFlow.Infrastructure  SupportFlow.Shared     SupportFlow.Shared
```

### ⚖️ Regras de Dependências
* Camadas superiores podem depender de camadas inferiores.  
* Camadas inferiores **NÃO** devem depender de camadas superiores.  
* **SupportFlow.Shared** pode ser utilizado por qualquer camada (DTOs, Enums, VOs).

**Dependências do Projeto:**
* **SupportFlow.Api** depende de SupportFlow.Application, SupportFlow.Infrastructure e SupportFlow.Shared  
* **SupportFlow.Application** depende de SupportFlow.Domain e SupportFlow.Shared  
* **SupportFlow.Infrastructure** depende de SupportFlow.Domain e SupportFlow.Shared  
* **SupportFlow.Domain** depende apenas de SupportFlow.Shared  
* **SupportFlow.Shared** pode ser usado por todas as camadas

___
