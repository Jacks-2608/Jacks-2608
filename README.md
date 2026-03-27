# Jacks-2608

## Como Instalar Skills do GitHub no Cursor

### O que são Skills?

**Agent Skills** é um padrão aberto para estender o Cursor AI com capacidades especializadas. Skills são pacotes portáteis e versionados que ensinam aos agentes como executar tarefas específicas de domínio. Podem incluir scripts, templates e referências.

### Diretórios de Skills

O Cursor descobre automaticamente skills nos seguintes diretórios:

| Localização | Escopo |
|---|---|
| `.agents/skills/` | Projeto |
| `.cursor/skills/` | Projeto |
| `~/.cursor/skills/` | Usuário (global) |

Para compatibilidade, o Cursor também carrega skills de: `.claude/skills/`, `.codex/skills/`, `~/.claude/skills/` e `~/.codex/skills/`.

### Estrutura de uma Skill

Cada skill deve ser uma pasta contendo um arquivo `SKILL.md`:

```text
.agents/
└── skills/
    └── minha-skill/
        └── SKILL.md
```

Uma skill pode incluir diretórios opcionais para scripts, referências e assets:

```text
.agents/
└── skills/
    └── deploy-app/
        ├── SKILL.md
        ├── scripts/
        │   ├── deploy.sh
        │   └── validate.py
        ├── references/
        │   └── REFERENCE.md
        └── assets/
            └── config-template.json
```

### Formato do arquivo SKILL.md

```markdown
---
name: minha-skill
description: Descrição curta do que essa skill faz e quando usá-la.
---

# Minha Skill

Instruções detalhadas para o agente.

## Quando Usar

- Use essa skill quando...
- Essa skill é útil para...

## Instruções

- Orientações passo a passo para o agente
- Convenções específicas do domínio
- Boas práticas e padrões
```

#### Campos do frontmatter

| Campo | Obrigatório | Descrição |
|---|---|---|
| `name` | Sim | Identificador da skill. Apenas letras minúsculas, números e hífens. Deve corresponder ao nome da pasta. |
| `description` | Sim | Descreve o que a skill faz e quando usá-la. Usado pelo agente para determinar relevância. |
| `license` | Não | Nome da licença ou referência a um arquivo de licença. |
| `compatibility` | Não | Requisitos do ambiente (pacotes do sistema, acesso à rede, etc.). |
| `metadata` | Não | Mapeamento chave-valor arbitrário para metadados adicionais. |
| `disable-model-invocation` | Não | Quando `true`, a skill só é incluída quando explicitamente invocada via `/nome-da-skill`. |

### Instalando Skills do GitHub

Existem duas formas de instalar skills de repositórios do GitHub:

#### Método 1: Via Interface do Cursor (Recomendado)

1. Abra as **Configurações do Cursor** (`Cmd+Shift+J` no Mac, `Ctrl+Shift+J` no Windows/Linux)
2. Navegue até a aba **Rules**
3. Na seção **Project Rules**, clique em **Add Rule**
4. Selecione **Remote Rule (GitHub)**
5. Insira a URL do repositório GitHub que contém as skills
6. As skills serão importadas para o diretório `.cursor/skills/` do seu projeto

#### Método 2: Manualmente via Git

1. Clone ou copie a pasta da skill de um repositório GitHub
2. Coloque a pasta dentro de um dos diretórios de skills reconhecidos:
   - `.agents/skills/` (nível de projeto)
   - `.cursor/skills/` (nível de projeto)
   - `~/.cursor/skills/` (nível de usuário/global)
3. Certifique-se de que a skill contém um arquivo `SKILL.md` válido

### Visualizando Skills Instaladas

Para ver as skills descobertas pelo Cursor:

1. Abra as **Configurações do Cursor** (`Cmd+Shift+J` / `Ctrl+Shift+J`)
2. Navegue até **Rules**
3. As skills aparecem na seção **Agent Decides**

### Usando Skills

- **Automaticamente:** o agente aplica skills automaticamente quando determina que são relevantes para o contexto atual.
- **Manualmente:** digite `/` no chat do Agent e procure pelo nome da skill.

### Migrando Regras Existentes para Skills

O Cursor (a partir da versão 2.4) inclui uma skill integrada `/migrate-to-skills` que converte regras dinâmicas e slash commands existentes em skills:

1. Digite `/migrate-to-skills` no chat do Agent
2. O agente identificará regras e comandos elegíveis e os converterá em skills
3. Revise as skills geradas em `.cursor/skills/`

### Conectando o Cursor ao GitHub

Para a integração completa com o GitHub:

1. Abra as **Configurações do Cursor**
2. Vá em **Integrations** → **GitHub**
3. Autorize o Cursor a acessar seus repositórios
4. Selecione e clone repositórios diretamente no ambiente local
5. Use a funcionalidade Git integrada do Cursor para commits e push

### Saiba Mais

- [Documentação oficial do Cursor sobre Skills](https://www.cursor.com/docs/context/skills)
- [Padrão aberto Agent Skills](https://agentskills.io/)
- [Integração GitHub no Cursor](https://docs.cursor.com/en/integrations/github)
