# Cronograma

## Fase 0 — Alinhamento e escopo do MVP

>Objetivo: travar o que entra no primeiro ciclo e evitar excesso de escopo.

Entregas:
- definição do MVP;
- priorização dos módulos;
- refinamento das regras de negócio;
- mapa de usuários e permissões;
- validação da arquitetura inicial.

MVP inicial:
- login;
- cadastro de usuários;
- cadastro de salas;
- visualização de disponibilidade;
- reserva de sala;
- HOLD;
- cancelamento básico;
- painel admin simples.

## Fase 1 — Base técnica e fundação do sistema

>Objetivo: criar a infraestrutura mínima para desenvolver com segurança.

Entregas:
- repositório do projeto;
- setup de frontend e backend;
- banco MariaDB;
- autenticação JWT;
- RBAC básico;
- estrutura de deploy;
- padrão de logs e auditoria inicial.

Por que essa fase vem primeiro:
o sistema terá dados sensíveis e permissões diferentes entre Administrador e Psicólogo, então a base de segurança precisa existir antes das funcionalidades de negócio.

Prazo estimado: 1 a 2 semanas.

## Fase 2 — Cadastro e estrutura do domínio

Objetivo: construir os cadastros que sustentam o resto do sistema.

Entregas:
- cadastro de psicólogos;
- cadastro de administradores;
- cadastro de salas;
- tipos de sala;
- disponibilidade básica;
- contatos do usuário;
- endereços.

Observação técnica:
os documentos mostram um modelo relacional com entidades centrais como USUÁRIO, PSICÓLOGO, ADMINISTRATIVO, SALA, AGENDA, TRANSAÇÃO, CONTATO e ENDEREÇO. Isso é a espinha dorsal do sistema.

Prazo estimado: 1 a 2 semanas.

## Fase 3 — Agenda e reserva de salas

Objetivo: entregar o coração do produto.

Entregas:
- calendário de salas;
- visualização de vagas;
- reserva por hora avulsa;
- reserva por turno fixo;
- prevenção de conflito de horário;
- tela de agenda do psicólogo.

Funcionalidade crítica aqui:
o sistema precisa respeitar o requisito de visualização em tempo real, com atualização rápida e sem dupla reserva.

Prazo estimado: 2 semanas.

## Fase 4 — HOLD automático de 120 minutos

Objetivo: implementar a regra mais sensível do fluxo de reserva.

Entregas:
- reserva entra em HOLD;
- contador de expiração;
- liberação automática se o pagamento não for confirmado;
- atualização em tempo real do status da sala.

Por que essa fase merece atenção especial:
o documento destaca que o HOLD parece simples na interface, mas exige jobs assíncronos, controle de concorrência e estratégia robusta de backend.

Prazo estimado: 1 semana.

## Fase 5 — Financeiro e créditos

Objetivo: controlar pagamento, saldo e inadimplência.

Entregas:
- saldo de créditos do psicólogo;
- recarga por Pix, cartão e dinheiro;
- histórico financeiro;
- débito automático;
- multas por cancelamento tardio;
- visão de devedores para o admin;
- exportação em PDF.

Regra importante:
o documento prevê cancelamento com mínimo de 3 horas para não gerar multa; abaixo disso, aplica-se cobrança automática.

Prazo estimado: 2 semanas.

## Fase 6 — Notificações

Objetivo: reduzir faltas, atrasos e falhas de comunicação.

Entregas:
- envio de e-mail;
- SMS;
- WhatsApp;
- pop-up/in-app;
- resumo diário às 06h;
- lembrete 6 horas antes do atendimento;
- notificações de alteração e cancelamento.

Ponto crítico:
o requisito pede entrega em até 30 segundos e taxa mínima de 95% por canal.

Prazo estimado: 1 a 2 semanas.

## Fase 7 — Painel administrativo completo

Objetivo: dar visão centralizada para o gestor.

Entregas:
- status em tempo real das salas;
- bloqueio e desbloqueio de sala;
- edição/cancelamento de reservas pelo admin;
- aprovação/recusa de psicólogos;
- dashboard financeiro.
Prazo estimado: 1 a 2 semanas.

## Fase 8 — Polimento de UX, acessibilidade e performance

Objetivo: melhorar a experiência antes de colocar em uso real.

Entregas:
- validação de fluxo em no máximo 4 interações;
- adequação a WCAG 2.1 AA;
- contraste e navegação por teclado;
- responsividade;
- otimização de performance;
- mensagens de erro e estados vazios.

o sistema foi desenhado para uso em ambiente clínico com pouco tempo entre atendimentos, então a interface precisa ser muito rápida e clara.

Prazo estimado: 1 semana.

## Fase 9 — Testes, segurança e preparação para produção

Objetivo: garantir confiabilidade antes do go-live.

Entregas:
- testes unitários;
- testes de integração;
- testes de concorrência para reservas;
- revisão de segurança;
- logs de auditoria;
- backup e restore;
- monitoramento.

Prazo estimado: 1 semana.