# Exercício 01 — Sistema selecionado para executar


## 01 · CONTEXT

### Contexto do problema

Uma empresa de médio porte com equipes multidisciplinares precisa organizar reuniões internas em salas compartilhadas. Hoje, o processo é manual: reservas são feitas por e-mail, WhatsApp ou planilhas, o que gera conflitos de agenda, atrasos e dificuldade de auditoria.

O sistema proposto será um CRUD de reservas de salas de reunião, com foco em:

- registrar salas disponíveis;
- criar, consultar, atualizar e cancelar reservas;
- verificar disponibilidade por data e horário;
- facilitar a rotina de gestores e colaboradores;
- manter um histórico mínimo das ações realizadas.

### Objetivo do sistema

O sistema deve permitir que usuários reservem salas de reunião de forma simples, rápida e segura, evitando conflitos e reduzindo esforço manual de coordenação.

### Premissas

- Cada sala possui capacidade, localização e disponibilidade por turno.
- Uma reserva não pode se sobrepor a outra na mesma sala.
- Usuários autenticados acessam apenas o que lhes foi autorizado.
- O processo deve funcionar em navegador web, com foco em desktop e tablet.

---

## 02 · PERSON

### Persona primária

#### Ana Silva — Gestora de Operações
- Idade: 34 anos
- Papel: coordena agendamento de reuniões para 3 times distintos.
- Contexto: trabalha em ambiente híbrido e lida com múltiplas solicitações por dia.
- Objetivos:
  - evitar conflitos de agenda;
  - garantir uso eficiente das salas;
  - reduzir tempo gasto em comunicação manual.
- Frustrações:
  - reservas duplicadas;
  - salas indisponíveis sem aviso;
  - dificuldade de visualizar agenda semanal.

### Personas secundárias

#### Bruno Costa — Analista de Produto
- Precisa agendar reuniões de alinhamento e reuniões recorrentes.
- Valoriza rapidez na criação de reservas e visualização da disponibilidade.

#### Carla Mendes — Administradora de Escritório
- Responsável por manter o cadastro das salas e confirmar regras de uso.
- Valoriza organização, controle e rastreabilidade das reservas.

---

## 03 · RF

### Requisitos funcionais

1. RF01 — Cadastro de salas  
   O sistema deve permitir o cadastro de salas com nome, localização, capacidade e status.

2. RF02 — Listagem de salas  
   O sistema deve permitir listar todas as salas disponíveis e filtrar por local, capacidade ou status.

3. RF03 — Criação de reservas  
   O usuário deve poder criar uma reserva informando sala, data, horário de início e fim, responsável e objetivo.

4. RF04 — Validação de conflito de agenda  
   O sistema deve impedir a criação de reservas que se sobreponham em uma mesma sala no mesmo período.

5. RF05 — Edição e cancelamento de reservas  
   O responsável pela reserva deve poder alterar data, horário ou sala, além de cancelar a reserva quando necessário.

6. RF06 — Histórico e consulta  
   O sistema deve permitir consultar reservas futuras, passadas e o histórico por usuário ou sala.

### Critérios de validação dos RFs

- RF01 é testável: verificar se o cadastro aceita dados válidos e rejeita campos obrigatórios vazios.
- RF02 é testável: comparar a listagem retornada com o conjunto de salas cadastradas.
- RF03 é testável: tentar reservar uma sala em horário disponível e confirmar o registro.
- RF04 é testável: reservar a mesma sala em intervalo sobreposto e verificar bloqueio.
- RF05 é testável: editar ou cancelar uma reserva e confirmar o resultado na listagem.
- RF06 é testável: consultar um intervalo de datas e validar registros retornados.

---

## 04 · RNF

### Requisitos não funcionais

1. RNF01 — Performance  
   O sistema deve responder às consultas e gravações em até 2 segundos em cenários normais de uso.

2. RNF02 — Segurança  
   As operações de criação, edição e cancelamento devem exigir autenticação e autorização por perfil de usuário.

3. RNF03 — Usabilidade  
   A interface deve ser intuitiva para usuários com pouco treinamento, com fluxo de reserva em até 3 cliques.

4. RNF04 — Confiabilidade  
   O sistema deve manter consistência de dados e exibir mensagens claras de erro para falhas de validação ou conflito de agenda.

---

## 05 · US

### Histórias de usuário

#### US01 — Reservar uma sala para reunião
Como colaborador, eu quero reservar uma sala e informar data e horário, para garantir um espaço adequado para a reunião.

Critérios de aceite:
- AC01: o usuário consegue acessar a tela de reservas.
- AC02: o sistema valida campos obrigatórios antes de salvar.
- AC03: a reserva é criada com sucesso quando o horário está disponível.

#### US02 — Verificar disponibilidade da sala
Como gestor, eu quero visualizar a disponibilidade das salas em um período, para escolher a melhor opção sem conflito.

Critérios de aceite:
- AC01: o sistema exibe salas e horários livres por data.
- AC02: o sistema indica salas ocupadas em um período selecionado.
- AC03: o sistema bloqueia a criação em horários já reservados.

#### US03 — Cancelar ou alterar uma reserva
Como responsável pela reunião, eu quero editar ou cancelar uma reserva, para ajustar a agenda sem gerar conflitos.

Critérios de aceite:
- AC01: o sistema permite alterar dados da reserva antes do início.
- AC02: o sistema permite cancelar a reserva com confirmação.
- AC03: após alteração ou cancelamento, a disponibilidade é atualizada imediatamente.

### Priorização MoSCoW

- Must have (M): US01, US02, US03
- Should have (S): histórico de reservas por sala e responsável
- Could have (C): alertas por e-mail ou notificação
- Won't have (W): integração com calendário pessoal externo no escopo inicial

---

## 06 · AC

### Critérios de aceite do sistema

#### AC01 — Cadastro de sala
Dado que o administrador acessa o módulo de salas, quando ele informa nome, localização e capacidade válidos, então a sala é cadastrada com sucesso.

#### AC02 — Reserva em horário livre
Dado que exista uma sala disponível no intervalo solicitado, quando o usuário envia a reserva, então o sistema grava a reserva e a exibe na agenda.

#### AC03 — Reserva em horário ocupado
Dado que a sala já esteja reservada no período informado, quando o usuário tentar salvar a reserva, então o sistema rejeita a operação e exibe uma mensagem de conflito.

#### AC04 — Atualização de reserva
Dado que o usuário seja o responsável pela reserva, quando ele alterar data ou horário, então o sistema valida a nova disponibilidade e salva as mudanças.

#### AC05 — Cancelamento
Dado que a reserva exista, quando o usuário cancelar, então o sistema remove o registro e libera o espaço para novas reservas.

#### AC06 — Consulta de agenda
Dado que o usuário escolha uma data, quando ele consultar a agenda, então o sistema exibe todas as reservas do período e os horários disponíveis.

---

## 07 · OUT

### Fora de escopo

- integração com Google Calendar, Outlook ou outros calendários pessoais;
- autenticação por login social ou MFA em versão inicial;
- acesso mobile dedicado com experiência nativa;
- relatórios analíticos avançados ou dashboards gerenciais;
- notificações push para todos os dispositivos;
- exportação de dados em PDF/Excel no MVP.

### Observações

O foco inicial é resolver o problema de agendamento de salas com alta confiabilidade, baixa curva de aprendizagem e organização básica da agenda. A partir do MVP, é possível evoluir para integrações e relatórios mais completos.

---

## Checklist de validação humana

- [x] Cruxamento  
  Cada RF tem pessoa associada? Cada RNF é mensurável?

- [x] Clareza  
  Um dev novo consegue ler e entender em 5 minutos?

- [x] Segurança  
  RNFs cobrem autenticação, dados sensíveis e LGPD?
# Exercicio-1
