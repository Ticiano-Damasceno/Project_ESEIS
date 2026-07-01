# Eseís — Plataforma de Gestão para Clínica de Psicologia

(mk9q8FLEpW2EIOa)

Sistema para unificar, em uma única plataforma, a gestão operacional de uma clínica de psicologia, contemplando **gestor**, **psicólogo** e **paciente**.

## Visão geral

- **reservas e agendamento de salas**;
- **controle de disponibilidade em tempo real**;
- **sistema de HOLD de 120 minutos**;
- **controle financeiro e créditos**;
- **notificações automáticas**;
- **gestão de usuários, papéis e permissões**;
- **acompanhamento operacional da clínica em tempo real**.
- **preparação para conformidade com LGPD e sigilo profissional**.

## Contexto do projeto

A solução foi desenhada para clínicas de psicologia de pequeno e médio porte, com fluxo diário de uso por:

- Administrador / Gestor da clínica
- Psicólogo
- Paciente / Cliente

Os documentos do projeto mostram que o principal problema é a fragmentação das ferramentas de agenda, financeiro, comunicação e registro, gerando retrabalho e perda de informação. A proposta é unificar esses processos em uma única plataforma.

## Principais funcionalidades

### Para o psicólogo
- visualizar salas disponíveis em tempo real;
- reservar sala por **hora avulsa** ou **turno fixo**;
- manter reserva em **HOLD por 120 minutos** até confirmar pagamento;
- cancelar reservas com política de multa;
- acompanhar agenda semanal;
- consultar saldo de créditos e histórico financeiro;
- receber notificações por e-mail, SMS, WhatsApp e pop-up.

### Para o administrador
- cadastrar e gerenciar salas;
- visualizar ocupação em tempo real;
- bloquear/desbloquear salas;
- criar, editar e cancelar reservas;
- gerenciar psicólogos;
- controlar financeiro da clínica;
- acompanhar devedores, multas e pagamentos;
- registrar compensações manuais.

### Para o paciente
- receber notificações;
- acessar fluxos simples de confirmação e comunicação;
- ter uma experiência acessível e objetiva.

---

## Requisitos não funcionais principais

- atualização em tempo real com baixa latência;
- interface simples e rápida;
- suporte a desktop, tablet e smartphone;
- conformidade com **LGPD**;
- controle de acesso por perfil;
- acessibilidade básica e foco em usabilidade;
- escalabilidade para crescimento futuro.

---

## Regras de negócio relevantes

- Um horário reservado entra em HOLD por até 120 minutos.
- Cancelamentos com menos de 3 horas de antecedência podem gerar multa.
- O psicólogo pode ser notificado para validar alterações feitas pelo administrador.
- O administrador precisa visualizar ocupação de salas em tempo real.
- O sistema deve respeitar perfis de acesso distintos.
- O sistema lida com dados sensíveis e exige cuidado com segurança e privacidade.

## Boas práticas esperadas

- código organizado por domínio;
- controle de acesso por perfil;
- logs de auditoria;
- validação em backend;
- transações no banco para evitar inconsistência;
- interface simples e rápida;
- foco em usabilidade para ambiente clínico.

## Objetivo do repositório

Este repositório será usado para construir a plataforma de forma incremental, validando primeiro o núcleo operacional e evoluindo depois para módulos complementares.


## Stack técnica

A tecnologia foi ajustada para aproveitar a infraestrutura disponível na HomeHost:

- **Frontend:** React
- **Backend:** PHP
- **Banco de dados:** MariaDB
- **Hospedagem/Infraestrutura:** HomeHost
- **Acesso inicial ao ambiente:** domínio, FTP e banco já disponíveis

## Estratégia recomendada

Para este cenário, a recomendação é construir o sistema em camadas:

1. **Frontend React**
   - Interface para administrador, psicólogo e paciente
   - Fluxos rápidos e responsivos
   - Possibilidade de evolução para PWA no futuro

2. **Backend PHP**
   - API para regras de negócio
   - Controle de autenticação e autorização
   - Processamento de agenda, reservas, financeiro e notificações

3. **Banco MySQL**
   - Modelagem relacional para usuários, salas, agenda, transações, contatos e endereços
   - Consistência transacional para evitar conflitos de reserva

---


## Estrutura de dados principal

Entidades centrais previstas no domínio:

- `usuario`
- `psicologo`
- `administrativo`
- `paciente`
- `sala`
- `agenda`
- `transacao`
- `pagamento`
- `contato`
- `endereco`
- `paciente_atendimento`


### Fase 1
- setup do projeto;
- banco de dados;
- autenticação;
- RBAC;
- estrutura base do backend e frontend.

### Fase 2
- cadastro de usuários;
- cadastro de salas;
- tipos de sala;
- permissões iniciais.

### Fase 3
- agenda;
- reservas;
- prevenção de conflito;
- HOLD automático.

### Fase 4
- financeiro;
- créditos;
- multas;
- histórico e relatórios.

### Fase 5
- notificações multicanal;
- tempo real;
- ajustes de UX;
- testes e preparação para produção.

---

## Segurança e privacidade

Este projeto trabalha com dados sensíveis de saúde. Portanto:

- use HTTPS/TLS em produção;
- criptografe dados sensíveis em repouso;
- aplique RBAC com menor privilégio;
- registre logs de auditoria;
- trate dados pessoais conforme a LGPD;
- restrinja acesso a informações clínicas.

---