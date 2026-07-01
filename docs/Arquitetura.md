# Arquitetura do Software

> Monólito modular em camadas

Um monólito modular, organizado por domínios de negócio, e não por “tipo de arquivo” apenas.

**Por quê?**<br>
`Porque o sistema tem escopo bem definido;
depende fortemente de dados compartilhados;
precisa de consistência transacional;
terá uma equipe pequena no início;
e deve rodar bem em ambiente de hospedagem compartilhada.
Os documentos inclusive defendem a abordagem monolítica para o MVP, justamente por a agenda, o financeiro e as notificações compartilharem muitos dados e por o escopo ainda ser controlado
`

## Camadas da arquitetura
**1) Apresentação**

- telas do React;
- formulários;
- navegação;
- estados visuais;
- validações básicas de interface.

**2) API**

- autenticação;
- regras de negócio;
- autorização;
- orquestração dos casos de uso;
- retorno dos dados para o frontend.

**3) Domínio**

- entidades;
- regras centrais do negócio;
- políticas de reserva;
- multas;
- HOLD;
- transações financeiras.

**4) Persistência
Responsável por:**

- acesso ao MariaDB;
- consultas;
- inserts/updates;
- transações;
- integridade relacional.

**5) Infraestrutura e integrações**

- envio de e-mail;
- SMS;
- WhatsApp;
- geração de PDF;
- cron jobs;
- logs;
- armazenamento de arquivos.

## Backend em PHP

Como o backend será em PHP com Laravel.

**Vantagens:**
- estrutura pronta;
- migrations;
- ORM;
- validação;
- scheduler;
- jobs;
- autenticação mais organizada;
- melhor manutenção.


## Arquitetura lógica do sistema

**Módulos principais**
- Auth
- Usuários
- Psicólogos
- Pacientes
- Salas
- Agenda / Reservas
- Financeiro / Créditos
- Notificações
- Auditoria
- Configurações

Isso está alinhado com o modelo conceitual e relacional dos documentos, que centraliza o sistema em entidades como `USUÁRIO`, `PSICÓLOGO`, `PACIENTE`, `SALA`, `AGENDA`, `TRANSAÇÃO`, `CONTATO` e `ENDEREÇO`, além da entidade associativa de atendimento

## Arquitetura de pastas


```bash
eseis-clinica/
├── README.md
├── .gitignore
├── .env.example
├── docs/
│   ├── arquitetura/
│   ├── banco-de-dados/
│   ├── regras-de-negocio/
│   └── api/
├── frontend/
│   ├── public/
│   └── src/
└── backend/
    ├── app/
    ├── config/
    ├── database/
    ├── public/
    ├── routes/
    ├── storage/
    └── tests/
```

## Estrutura para o frontend React

```bash
frontend/
├── public/
└── src/
    ├── assets/
    ├── components/
    ├── features/
    │   ├── auth/
    │   ├── agenda/
    │   ├── salas/
    │   ├── financeiro/
    │   ├── notificacoes/
    │   ├── pacientes/
    │   └── psicologos/
    ├── hooks/
    ├── layouts/
    ├── pages/
    ├── routes/
    ├── services/
    ├── store/
    ├── styles/
    ├── utils/
    └── main.jsx
```

Ideia da organização:

- components/: componentes reutilizáveis
- features/: módulos por domínio
- pages/: telas finais
- services/: consumo da API
- store/: estado global
- utils/: funções auxiliares

## Estrutura para o backend PHP

```bash
backend/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   ├── Middleware/
│   │   └── Requests/
│   ├── Models/
│   ├── Services/
│   ├── Repositories/
│   ├── Jobs/
│   ├── Mail/
│   ├── Notifications/
│   ├── Policies/
│   └── Helpers/
├── bootstrap/
├── config/
├── database/
│   ├── migrations/
│   ├── seeders/
│   └── factories/
├── public/
├── resources/
├── routes/
├── storage/
└── tests/
```
Separação por responsabilidade:
- Controllers: recebem requests e retornam responses
- Requests: validação de entrada
- Services: regras de negócio
- Repositories: acesso aos dados
- Models: entidades persistidas
- Jobs: tarefas assíncronas
- Policies: autorização
- Notifications: envio multicanal

## Desenho dos fluxos críticos
Fluxo de reserva com HOLD
Psicólogo escolhe sala e horário.
Sistema cria reserva em HOLD.
Banco trava o slot.
Registra hold_expires_at.
Pagamento confirmado?
sim: confirma reserva;
não: cron/job libera automaticamente.
Os documentos deixam claro que o HOLD é central e precisa de concorrência controlada para evitar dupla reserva

Fluxo de cancelamento com multa
Usuário cancela a reserva.
Sistema compara horário atual com início do atendimento.
Se faltarem menos de 3 horas, aplica multa.
Multa é debitada dos créditos.
Registro vai para auditoria e financeiro.
Fluxo financeiro
cada recarga vira uma transação;
cada atendimento concluído debita saldo;
cada multa vira lançamento financeiro;
todo movimento precisa ficar auditável.
