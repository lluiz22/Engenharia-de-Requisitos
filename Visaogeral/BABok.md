# Sistema de Gestão Inteligente de Projetos com LLM

## 1. Visão Geral

O **Obsidian** funciona como o "cérebro" de conhecimento do sistema, armazenando e organizando informações relevantes dos projetos para que um **LLM (Large Language Model)** possa consultá-las quando necessário.

O sistema permite que os funcionários enviem informações por **texto ou áudio**, principalmente durante os **Dailys**. A LLM poderá interpretar essas informações, consultar os dados existentes nas ferramentas integradas e gerar atualizações para a equipe e para os gestores.

---

# 2. Requisitos de Negócio

## RN01 — Melhorar a comunicação interna

### Descrição

A solução deve facilitar a comunicação entre os membros da equipe, reduzindo a necessidade de atualizações manuais e repetitivas.

### Objetivo

Centralizar e automatizar o compartilhamento de informações relacionadas ao andamento dos projetos.

---

## RN02 — Reduzir atrasos nos projetos

### Descrição

A solução deve permitir identificar antecipadamente:

* Tarefas atrasadas;
* Impedimentos;
* Riscos;
* Atividades sem atualização;
* Possíveis problemas que possam comprometer os prazos.

### Objetivo

Permitir que gestores e equipes atuem de forma preventiva antes que os problemas afetem o cronograma dos projetos.

---

## RN03 — Aumentar a visibilidade da gestão

### Descrição

Os gestores devem possuir uma visão consolidada do andamento dos projetos e das atividades da equipe.

### Objetivo

Facilitar a tomada de decisões por meio de informações centralizadas e atualizadas.

---

## RN04 — Automatizar processos internos

### Descrição

A solução deve automatizar atividades relacionadas ao acompanhamento de:

* Dailys;
* Weeklies;
* Sprints;
* Tarefas;
* Impedimentos;
* Progresso dos projetos.

### Objetivo

Reduzir o trabalho manual e tornar o acompanhamento dos projetos mais eficiente.

---

## RN05 — Centralizar informações

### Descrição

A solução deve utilizar as informações existentes nas ferramentas utilizadas pela empresa para gerar uma visão integrada dos projetos.

### Objetivo

Evitar que informações importantes fiquem isoladas em diferentes sistemas e facilitar o acesso ao conhecimento da organização.

---

# 3. Stack Tecnológica

| Tecnologia          | Função                                                                     |
| ------------------- | -------------------------------------------------------------------------- |
| **LLM / API de IA** | Interpretação de mensagens, análise das informações e geração de respostas |
| **VPS**             | Hospedagem do agente e centralização das integrações                       |
| **GitHub**          | Repositórios de código e informações relacionadas ao desenvolvimento       |
| **Obsidian**        | Base de conhecimento e "cérebro" do agente                                 |
| **Trello**          | Organização e acompanhamento dos projetos e tarefas                        |
| **Google Drive**    | Armazenamento de arquivos e documentos                                     |
| **WhatsApp**        | Interface de comunicação com os funcionários                               |
| **APIs / MCPs**     | Integração entre o agente e as ferramentas                                 |
| **Webhooks**        | Comunicação e acionamento automático entre os sistemas                     |

> **Observação:** informações sensíveis, como senhas e credenciais de acesso, devem ser armazenadas de forma segura. O Google Drive não deve ser utilizado como armazenamento direto de senhas em texto puro.

---

# 4. Arquitetura Proposta

```text
┌─────────────────┐
│   Funcionário   │
└────────┬────────┘
         │
    Texto ou Áudio
         │
         ▼
┌─────────────────┐
│    WhatsApp     │
└────────┬────────┘
         │
      Webhook
         │
         ▼
┌─────────────────┐
│       VPS       │
│                 │
│   Agente / LLM  │
└────────┬────────┘
         │
    ┌────┼────┬──────────────┐
    │    │    │              │
    ▼    ▼    ▼              ▼
┌──────┐ ┌────────┐ ┌───────┐ ┌────────────┐
│GitHub│ │Obsidian│ │Trello │ │Google Drive│
└──────┘ └────────┘ └───────┘ └────────────┘
         │
         ▼
┌─────────────────┐
│       LLM       │
│                 │
│ Análise de dados│
│ Identificação   │
│ de riscos       │
│ Geração de      │
│ atualizações    │
└────────┬────────┘
         │
      Webhook
         │
         ▼
┌─────────────────┐
│ Grupo da Empresa│
│   (Diariamente) │
└─────────────────┘
```

---

# 5. Fluxo de Funcionamento

## 5.1 Entrada da informação

O funcionário envia uma mensagem para o sistema através do **WhatsApp**.

A mensagem pode ser:

* Texto;
* Áudio.

---

## 5.2 Processamento

Caso a mensagem seja um áudio, o sistema realiza a transcrição do conteúdo.

Após a transcrição, a informação é encaminhada ao agente de IA.

```text
Áudio
  ↓
Transcrição
  ↓
Texto
  ↓
LLM
```

---

## 5.3 Consulta às fontes de informação

O LLM recebe a informação enviada pelo funcionário e consulta as fontes disponíveis através da VPS.

```text
              ┌─────────────┐
              │     LLM     │
              └──────┬──────┘
                     │
               Consulta dados
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
     GitHub       Obsidian      Trello
        │            │            │
        └────────────┼────────────┘
                     │
                     ▼
                Google Drive
```

Essas consultas podem ser realizadas utilizando:

* APIs oficiais;
* APIs não oficiais, quando específicas;
* MCPs (Model Context Protocol), dependendo da disponibilidade e das necessidades de cada integração.

---

# 6. Papel do Obsidian

O **Obsidian** será utilizado como o **"cérebro" do sistema**.

Ele terá a função de concentrar o conhecimento relacionado aos projetos, permitindo que um LLM consulte informações como:

* Contexto dos projetos;
* Requisitos;
* Decisões tomadas;
* Documentação;
* Regras de negócio;
* Histórico de atividades;
* Informações importantes da equipe;
* Registros de atividades;
* Informações relacionadas aos Sprints.

A ideia é que o LLM não dependa apenas das informações apresentadas na mensagem recebida, mas também possa consultar o conhecimento previamente armazenado.

---

# 7. Funcionamento do Daily

Um fluxo possível para o Daily seria:

```text
Funcionário envia áudio/texto
            ↓
         WhatsApp
            ↓
         Webhook
            ↓
           VPS
            ↓
  Transcrição de áudio
            ↓
           LLM
            ↓
Consulta das informações
            ↓
┌───────────┼────────────┐
▼           ▼            ▼
GitHub   Obsidian      Trello
            │
            ▼
       Google Drive
            ↓
      Análise pela LLM
            ↓
Identificação de progresso,
atrasos, impedimentos e riscos
            ↓
    Geração do resumo
            ↓
         Webhook
            ↓
    Grupo da empresa
```

---

# 8. Exemplo de Funcionamento

Um desenvolvedor pode enviar pelo WhatsApp:

> "Ontem finalizei uma API de autenticação, mas estou trabalhando na integração com o banco porque estou esperando as credenciais."

O sistema poderá:

1. Receber o áudio ou texto;
2. Transcrever o áudio, caso necessário;
3. Identificar que a tarefa de autenticação foi concluída;
4. Identificar o impedimento relacionado às credenciais;
5. Consultar o Trello para verificar a tarefa correspondente;
6. Consultar o Obsidian para obter o contexto do projeto;
7. Registrar ou sugerir a atualização das informações;
8. Identificar o impedimento;
9. Gerar um resumo para o Daily;
10. Enviar as informações para o grupo da empresa.

### Exemplo de resultado

```text
📋 DAILY — Projeto X

👨‍💻 Desenvolvedor: João

✅ Concluído:
API de autenticação.

🚧 Impedimento:
Integração com o banco aguardando credenciais.

⚠️ Atenção:
A ausência das credenciais pode impactar o prazo da tarefa.

📌 Próxima ação:
Disponibilizar as credenciais para continuidade da integração.
```

---

# 9. Stakeholders

## 9.1 Gestores

Responsáveis por acompanhar o andamento dos projetos, identificar atrasos, analisar riscos e tomar decisões.

### Necessidades

* Visão consolidada dos projetos;
* Identificação de atrasos;
* Identificação de riscos;
* Acompanhamento da equipe;
* Relatórios de progresso.

---

## 9.2 Desenvolvedores

Responsáveis pela execução das atividades e pelo registro de progresso, dificuldades e impedimentos.

### Necessidades

* Registrar atividades rapidamente;
* Comunicar impedimentos;
* Atualizar tarefas;
* Reduzir atividades manuais;
* Interagir com o sistema por texto ou áudio.

---

## 9.3 Analistas de Negócio

Responsáveis por levantar, analisar e organizar as necessidades da empresa.

### Necessidades

* Organizar requisitos;
* Acompanhar necessidades dos projetos;
* Garantir o alinhamento entre negócio e equipe técnica.

---

## 9.4 Engenheiros de Requisitos

Responsáveis pela documentação, análise e organização dos requisitos.

### Necessidades

* Centralizar requisitos;
* Manter documentação atualizada;
* Relacionar requisitos às atividades dos projetos;
* Facilitar o rastreamento das mudanças.

---

## 9.5 Usuários / Funcionários

Interagem diretamente com o sistema, principalmente por meio de mensagens de texto ou áudio.

### Necessidades

* Facilidade de uso;
* Comunicação rápida;
* Pouca necessidade de preenchimento manual;
* Possibilidade de envio de informações por áudio.

---

## 9.6 Equipe de Infraestrutura

Responsável pela manutenção da VPS, APIs, integrações e demais componentes técnicos.

### Necessidades

* Monitoramento dos serviços;
* Segurança;
* Disponibilidade;
* Gerenciamento das integrações;
* Controle de acessos;
* Manutenção da infraestrutura.

---

## 9.7 LLM / Agente de IA

Componente responsável por interpretar informações, consultar as fontes de dados e gerar respostas e atualizações.

### Responsabilidades

* Interpretar mensagens;
* Processar transcrições;
* Consultar informações;
* Correlacionar dados de diferentes ferramentas;
* Identificar atrasos e impedimentos;
* Gerar resumos;
* Auxiliar na comunicação da equipe;
* Automatizar atividades relacionadas a Dailys, Weeklies e Sprints.

---

# 10. Visão Geral da Solução

A proposta de solução busca transformar diversas ferramentas isoladas em um **ecossistema integrado de gestão ágil**, no qual o LLM atua como uma camada inteligente entre os funcionários, gestores e as fontes de informação da empresa.

```text
                 FUNCIONÁRIOS
                      │
                      ▼
               ┌────────────┐
               │  WhatsApp  │
               └──────┬─────┘
                      │
                Texto / Áudio
                      │
                      ▼
               ┌────────────┐
               │     VPS    │
               └──────┬─────┘
                      │
                      ▼
               ┌────────────┐
               │    LLM     │
               │   AGENTE   │
               └──────┬─────┘
                      │
          ┌───────────┼───────────┐
          │           │           │
          ▼           ▼           ▼
       GitHub      Obsidian     Trello
          │           │           │
          └───────────┼───────────┘
                      │
                      ▼
                 Google Drive
                      │
                      ▼
             ┌─────────────────┐
             │ Análise          │
             │ Inteligente      │
             └────────┬────────┘
                      │
             ┌────────┴────────┐
             ▼                 ▼
        Gestão / Alertas   Dailys / Weeklies
             │                 │
             └────────┬────────┘
                      ▼
                Equipe / Gestores
```

---

# 11. Resultado Esperado

Com a implementação da solução, espera-se:

* Melhorar a comunicação interna;
* Reduzir atrasos nos projetos;
* Identificar impedimentos antecipadamente;
* Identificar riscos de forma preventiva;
* Aumentar a visibilidade dos gestores;
* Reduzir atualizações manuais;
* Automatizar o acompanhamento de Dailys, Weeklies e Sprints;
* Centralizar informações de diferentes ferramentas;
* Facilitar o acesso ao conhecimento dos projetos;
* Aumentar a eficiência dos processos internos.

---

# 12. Ferramentas Utilizadas

* **usamos gpt para formatação em md**
