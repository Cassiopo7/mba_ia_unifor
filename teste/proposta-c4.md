# Proposta de Arquitetura C4 - Sistema de Conciliação de Notas Fiscais

## Visão Geral
Sistema para cruzamento automático de notas fiscais emitidas com o contas a receber, permitindo identificar divergências, confirmar recebimentos e facilitar a reconciliação financeira.

---

## Nível 1: Diagrama de Contexto

```mermaid
C4Context
    title Diagrama de Contexto - Sistema de Conciliação Fiscal

    Person(usuario, "Usuário Financeiro", "Analista responsável pela conciliação financeira")
    Person(gestor, "Gestor Financeiro", "Acompanha relatórios e indicadores")

    System(sistema_conciliacao, "Sistema de Conciliação Fiscal", "Cruza notas fiscais emitidas com contas a receber e identifica divergências")

    System_Ext(erp, "Sistema ERP", "Gerencia contas a receber e dados financeiros")
    System_Ext(nfe, "Sistema de NF-e", "Gerencia emissão de notas fiscais eletrônicas")
    System_Ext(sefaz, "SEFAZ", "Consulta status e valida notas fiscais")
    System_Ext(email, "Servidor de E-mail", "Envia notificações e alertas")

    Rel(usuario, sistema_conciliacao, "Realiza conciliação, visualiza divergências")
    Rel(gestor, sistema_conciliacao, "Visualiza relatórios e dashboards")
    Rel(sistema_conciliacao, erp, "Importa contas a receber", "API REST")
    Rel(sistema_conciliacao, nfe, "Importa notas fiscais emitidas", "API REST")
    Rel(sistema_conciliacao, sefaz, "Consulta status das NF-e", "Web Service")
    Rel(sistema_conciliacao, email, "Envia notificações", "SMTP")
```

---

## Nível 2: Diagrama de Contêiner

```mermaid
C4Container
    title Diagrama de Contêiner - Sistema de Conciliação Fiscal

    Person(usuario, "Usuário Financeiro", "Analista responsável pela conciliação")

    System_Boundary(sistema, "Sistema de Conciliação Fiscal") {
        Container(webapp, "Aplicação Web", "React.js", "Interface web para gerenciamento de conciliações")
        Container(api, "API Backend", "Node.js/Express", "Fornece funcionalidades de conciliação via API REST")
        Container(worker, "Worker de Processamento", "Node.js", "Processa conciliações em background")
        Container(db, "Banco de Dados", "PostgreSQL", "Armazena NFs, contas a receber e conciliações")
        Container(cache, "Cache", "Redis", "Cache de dados e fila de processamento")
        Container(storage, "Armazenamento", "S3/MinIO", "Armazena XMLs das NF-e e relatórios")
    }

    System_Ext(erp, "Sistema ERP", "Contas a receber")
    System_Ext(nfe, "Sistema de NF-e", "Notas fiscais")
    System_Ext(sefaz, "SEFAZ", "Validação de NF-e")

    Rel(usuario, webapp, "Usa", "HTTPS")
    Rel(webapp, api, "Consome", "JSON/HTTPS")
    Rel(api, db, "Lê/Escreve", "SQL")
    Rel(api, cache, "Lê/Escreve", "Redis Protocol")
    Rel(api, storage, "Armazena arquivos", "S3 API")
    Rel(worker, cache, "Consome filas", "Redis Protocol")
    Rel(worker, db, "Lê/Escreve", "SQL")
    Rel(worker, storage, "Lê XMLs", "S3 API")
    Rel(api, erp, "Importa dados", "API REST")
    Rel(api, nfe, "Importa NF-e", "API REST")
    Rel(worker, sefaz, "Consulta status", "SOAP/REST")
```

---

## Nível 3: Diagrama de Componentes (API Backend)

```mermaid
C4Component
    title Diagrama de Componentes - API Backend

    Container_Boundary(api, "API Backend") {
        Component(auth, "Autenticação", "Middleware", "Gerencia autenticação JWT e autorização")
        Component(nf_controller, "Controller NF-e", "Express Router", "Endpoints para importação e consulta de NF-e")
        Component(cr_controller, "Controller Contas a Receber", "Express Router", "Endpoints para contas a receber")
        Component(conciliacao_controller, "Controller Conciliação", "Express Router", "Endpoints para conciliação")

        Component(nf_service, "Serviço NF-e", "Service Layer", "Lógica de negócio para NF-e")
        Component(cr_service, "Serviço Contas a Receber", "Service Layer", "Lógica de negócio para CR")
        Component(conciliacao_service, "Serviço Conciliação", "Service Layer", "Algoritmo de matching e conciliação")
        Component(integracao_service, "Serviço Integração", "Service Layer", "Integrações com sistemas externos")

        Component(repository, "Repositórios", "Data Access Layer", "Acesso aos dados via ORM")
        Component(queue, "Gerenciador de Filas", "Bull Queue", "Enfileira processamentos assíncronos")
    }

    Container_Ext(db, "PostgreSQL", "Banco de Dados")
    Container_Ext(cache, "Redis", "Cache e Filas")
    Container_Ext(erp, "Sistema ERP", "Dados externos")

    Rel(nf_controller, auth, "Usa")
    Rel(cr_controller, auth, "Usa")
    Rel(conciliacao_controller, auth, "Usa")

    Rel(nf_controller, nf_service, "Usa")
    Rel(cr_controller, cr_service, "Usa")
    Rel(conciliacao_controller, conciliacao_service, "Usa")

    Rel(nf_service, repository, "Usa")
    Rel(cr_service, repository, "Usa")
    Rel(conciliacao_service, repository, "Usa")
    Rel(conciliacao_service, queue, "Enfileira processamento")

    Rel(integracao_service, erp, "Consome API")
    Rel(nf_service, integracao_service, "Usa")
    Rel(cr_service, integracao_service, "Usa")

    Rel(repository, db, "SQL")
    Rel(queue, cache, "Redis Protocol")
```

---

## Descrição dos Componentes Principais

### Frontend (Aplicação Web)
- **Tecnologia**: React.js com TypeScript
- **Funcionalidades**:
  - Dashboard com indicadores de conciliação
  - Listagem de NF-e e Contas a Receber
  - Interface de matching manual
  - Visualização de divergências
  - Exportação de relatórios

### Backend (API)
- **Tecnologia**: Node.js com Express
- **Responsabilidades**:
  - Importação de dados do ERP e NF-e
  - Algoritmo de matching automático
  - Gerenciamento de regras de conciliação
  - Exposição de APIs REST
  - Validação de dados

### Worker de Processamento
- **Tecnologia**: Node.js
- **Responsabilidades**:
  - Processamento assíncrono de conciliações em lote
  - Consulta periódica ao SEFAZ
  - Geração de relatórios
  - Envio de notificações

### Banco de Dados
- **Tecnologia**: PostgreSQL
- **Entidades Principais**:
  - NotasFiscais
  - ContasReceber
  - Conciliacoes
  - Divergencias
  - Usuarios
  - ConfiguracoesRegras

---

## Fluxo de Conciliação

1. **Importação**: Sistema importa NF-e e Contas a Receber dos sistemas externos
2. **Matching Automático**: Algoritmo cruza os dados baseado em regras configuráveis:
   - Número da NF-e
   - CNPJ do cliente
   - Valor
   - Data de emissão/vencimento
3. **Identificação de Divergências**: Sistema identifica:
   - NF-e sem CR correspondente
   - CR sem NF-e
   - Diferenças de valor
   - Diferenças de data
4. **Conciliação Manual**: Usuário pode fazer matching manual de itens não conciliados
5. **Relatórios**: Geração de relatórios de conciliação e divergências

---

## Tecnologias Sugeridas

### Frontend
- React.js / Next.js
- TypeScript
- TailwindCSS ou Material-UI
- Chart.js para gráficos

### Backend
- Node.js com Express ou NestJS
- TypeScript
- Prisma ou TypeORM
- Bull para filas

### Infraestrutura
- PostgreSQL 14+
- Redis 6+
- MinIO ou AWS S3
- Docker / Docker Compose
- Nginx como reverse proxy

---

## Próximos Passos

1. Validar requisitos funcionais detalhados
2. Definir regras de matching/conciliação
3. Modelar banco de dados completo
4. Criar protótipos de telas
5. Implementar MVP com funcionalidades core
