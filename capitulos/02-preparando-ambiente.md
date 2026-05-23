# Capítulo 2 — Preparando o ambiente

[⬅ Anterior: Visão geral](01-visao-geral.md) · [Sumário](../README.md) · Próximo: [Capítulo 3 — Rodando a aplicação ➡](03-rodando-aplicacao.md)

---

Antes de escrever uma linha de código, você precisa escolher **como** vai trabalhar. Este capítulo apresenta **três caminhos possíveis** e ajuda você a decidir o melhor para o seu equipamento e perfil. Depois cobre **como criar o repositório** e **a estrutura do projeto**.

## 2.1. Três caminhos possíveis

| Caminho | Como funciona | Vantagens | Limitações |
|---|---|---|---|
| **A — Navegador puro** | Edita arquivos no [github.com](https://github.com) ou [github.dev](https://github.dev) (basta apertar `.` no repo). Commit pela interface web. CI valida tudo. | ✅ Zero instalação<br>✅ Funciona em qualquer SO (Windows, Mac, Linux, ChromeOS, tablet) | ❌ Não roda testes nem Flask localmente — depende do CI<br>❌ Sem terminal |
| **B — GitHub Codespaces** ⭐ | Ambiente Linux completo no navegador, com terminal, VS Code e Python já instalados. Free tier: 120 horas/mês. | ✅ Zero instalação local<br>✅ Mesma experiência de um Linux/Mac<br>✅ Roda tudo na nuvem | ❌ Consome horas do free tier<br>❌ Precisa de internet estável |
| **C — Instalação local** | Você instala Git, Python, IDE no seu computador e roda tudo localmente. | ✅ Mais rápido para iterar<br>✅ Funciona offline<br>✅ Sem cota | ❌ Comandos diferentes por SO<br>❌ Pode ter atrito na instalação |

> 💡 **Recomendação para a aula**: comece pelo **Caminho B (Codespaces)**. Ele dá a experiência completa sem cobrar de você nenhuma instalação, e funciona igual em qualquer máquina. Depois, se quiser, migra para o Caminho C.

## 2.2. Pré-requisitos por caminho

| Item | Caminho A | Caminho B | Caminho C |
|---|---|---|---|
| Conta no [GitHub](https://github.com/signup) | ✅ | ✅ | ✅ |
| Git instalado | ❌ | ❌ (já vem) | ✅ ([download](https://git-scm.com/downloads)) |
| Python 3.11+ | ❌ | ❌ (já vem) | ✅ ([download](https://www.python.org/downloads/)) |
| Editor/IDE | ❌ (web) | ❌ (web) | ✅ ([VS Code](https://code.visualstudio.com/), [Cursor](https://cursor.com/), [Antigravity](https://antigravity.google/), [PyCharm](https://www.jetbrains.com/pycharm/)…) |

Os Caminhos A e B funcionam em **qualquer sistema operacional** e até em tablets ou ChromeBooks.

## 2.3. Criar o repositório no GitHub (todos os caminhos)

1. Acesse <https://github.com/new>.
2. **Repository name**: `tqs-2026` (ou nome de sua escolha).
3. Marque como **Public** — necessário para o GitHub Pages funcionar no plano gratuito.
4. Marque **"Add a README file"** se for usar o **Caminho A** (assim o repo já nasce inicializado e você pode editar pela web). Se for usar B ou C, deixe vazio que vamos criar tudo.
5. **Não** marque "Add .gitignore" nem "Choose a license" — vamos criar localmente.
6. Clique em **Create repository**.

---

## 2.4. Setup do Caminho A — Navegador puro

Você não instala nada. Trabalha tudo pelo navegador.

### Como criar arquivos/pastas pela interface

No repositório no GitHub:

1. Clique em **"Add file" → "Create new file"**.
2. No campo de nome, digite **`src/validators.py`** — as barras (`/`) criam as pastas automaticamente.
3. Cole o conteúdo do arquivo.
4. Role para baixo → **"Commit changes"**.
5. Escolha a branch (a primeira vez será a `main`; depois você vai criar branches para PRs).

### Atalho: github.dev (VS Code no navegador)

No seu repo no GitHub, **aperte `.`** (a tecla ponto) no teclado. Abre o **VS Code rodando no navegador**, com explorador de arquivos, edição em múltiplas abas e painel de Source Control para commits.

- Para criar pasta: botão direito no explorer → "New Folder".
- Para criar arquivo: botão direito → "New File".
- Para commit: painel de Source Control (ícone Git na barra lateral).

> Limitação importante: o github.dev **não tem terminal nem execução**. Você não roda `pytest` nem `flask`. **O CI no GitHub Actions valida seu código a cada commit** — leia o capítulo 7 para entender o pipeline.

### Para encontrar `SEU-USUARIO` no código (sem grep)

Use a **barra de busca do GitHub** com filtro do repo: digite `SEU-USUARIO` na busca dentro do seu repositório. Os 2 arquivos com placeholders aparecem na lista.

---

## 2.5. Setup do Caminho B — GitHub Codespaces ⭐

Esse é o caminho recomendado para a aula.

### Criar o Codespace

1. No seu repositório, clique em **"Code"** (botão verde) → aba **"Codespaces"** → **"Create codespace on main"**.
2. Aguarde ~30 segundos. O ambiente vai abrir o **VS Code no navegador**, já com Python 3.11, Git, terminal, e todas as dependências do projeto instaladas.
3. O arquivo [`.devcontainer/devcontainer.json`](../.devcontainer/devcontainer.json) (que já existe neste projeto) cuida da configuração automática: instala extensões (Python, Pylance, Ruff, GitHub PRs) e roda `pip install -r requirements-dev.txt`.

### Usar o terminal

Abra com `Ctrl + ~` (ou menu **Terminal → New Terminal**). Use exatamente os mesmos comandos que apareceriam no Linux/Mac em qualquer outro capítulo:

```bash
pytest                          # rodar testes
flask --app src.app run         # subir o Flask
ruff check .                    # lint
```

### Ver o Flask no navegador

Quando você rodar `flask --app src.app run`, o Codespace vai detectar a porta 5000 e mostrar um pop-up **"Open in Browser"**. Clique — abre uma URL pública temporária com o seu Flask rodando.

### Cota do free tier

- **120 horas-core/mês** gratuitas para contas pessoais
- Um Codespace de 2 cores consome 2 horas-core por hora de uso
- Para a disciplina toda: dá folgadamente

> **Importante**: **pare** o Codespace quando não estiver usando. Em **github.com/codespaces** você vê todos os seus Codespaces ativos e pode pará-los. Codespace parado não consome cota; só ocupa storage (também limitado).

---

## 2.6. Setup do Caminho C — Instalação local

Você roda tudo na sua máquina. Mais rápido para iterar, mas requer setup.

### Clonar o repositório

```bash
git clone https://github.com/SEU-USUARIO/tqs-2026.git
cd tqs-2026
```

Se estiver criando do zero (sem fork), no lugar acima:

```bash
mkdir tqs-2026 && cd tqs-2026
git init -b main
git remote add origin https://github.com/SEU-USUARIO/tqs-2026.git
```

### Criar o ambiente virtual

Um **ambiente virtual** (venv) isola as dependências do projeto das outras instalações de Python.

**Linux / macOS**:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows (PowerShell)**:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**Windows (CMD)**:

```cmd
python -m venv .venv
.venv\Scripts\activate.bat
```

Você saberá que o ambiente está ativo quando o prompt do terminal mostrar `(.venv)` no início.

### Instalar dependências

```bash
pip install -r requirements-dev.txt
```

### Criar estrutura de pastas (somente se criando do zero)

**Linux / macOS**:

```bash
mkdir -p .github/workflows .github/ISSUE_TEMPLATE src/templates tests docs
```

**Windows (PowerShell)**:

```powershell
New-Item -ItemType Directory -Force -Path .github\workflows, .github\ISSUE_TEMPLATE, src\templates, tests, docs
```

> 💡 No VS Code (qualquer SO), você pode criar pastas pela interface: botão direito no explorer → **New Folder**. Funciona igual em Windows, Mac e Linux. É a forma mais portável.

---

## 2.7. Estrutura final do repositório

Independente do caminho, ao final deste livro seu repositório terá:

```
tqs-2026/
├── .devcontainer/
│   └── devcontainer.json           # config do Codespaces (Caminho B)
├── .github/
│   ├── workflows/
│   │   ├── ci.yml                  # lint + testes + cobertura
│   │   └── deploy.yml              # deploy GitHub Pages
│   ├── ISSUE_TEMPLATE/             # templates para abrir issues
│   ├── pull_request_template.md    # checklist obrigatório de PRs
│   └── CODEOWNERS                  # quem revisa o quê
├── capitulos/                      # este livro didático
├── src/
│   ├── validators.py               # VERSÃO PRINCIPAL da lógica de validação
│   ├── app.py                      # rotas Flask
│   └── templates/index.html        # formulário renderizado pelo Flask
├── tests/
│   ├── test_validators.py          # testes unitários (4)
│   └── test_app.py                 # testes de integração (2)
├── docs/                           # publicado no GitHub Pages
│   ├── index.html
│   ├── validators.js               # ESPELHO em JS de validators.py
│   └── style.css
├── pyproject.toml                  # config ruff + pytest + coverage
├── requirements.txt                # Flask
├── requirements-dev.txt            # pytest, ruff, bandit, coverage
└── README.md                       # sumário do livro
```

## 2.8. Personalizações antes do primeiro `push`

Se você está usando este projeto a partir de um **fork** (ou copiou os arquivos), há **dois lugares** com placeholders para trocar pelo seu usuário do GitHub:

- [`docs/index.html`](../docs/index.html) — no rodapé, troque `SEU-USUARIO` na URL `https://github.com/SEU-USUARIO/tqs-2026` pelo seu usuário.
- [`.github/CODEOWNERS`](../.github/CODEOWNERS) — descomente a linha `# * @SEU-USUARIO` e troque pelo seu usuário.

**Como encontrar todas as ocorrências**:

| Caminho | Como buscar |
|---|---|
| A (navegador) | Use a barra de busca do GitHub no seu repo, digite `SEU-USUARIO` |
| B (Codespaces) ou C (local) | No terminal: `grep -rn "SEU-USUARIO" .` |

Faça as substituições, confira que a busca não retorna mais nada, e só então faça o `push`.

> Os outros lugares com o nome do professor (LICENSE, README, pyproject.toml) são de **autoria** do material didático e devem ficar como estão — quando você forka, herda a licença MIT e o crédito do autor original.

---

Próximo capítulo: [Capítulo 3 — Rodando a aplicação ➡](03-rodando-aplicacao.md)
