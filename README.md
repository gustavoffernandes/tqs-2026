# TQS 2026 — Projeto-exemplo de Teste e Qualidade de Software

> Material didático da disciplina **Teste e Qualidade de Software (PC010027)** — graduação, Universidade Federal do Oeste do Pará (UFOPA).
> Prof. **Helvecio Bezerra Leal Neto** · 2026

Este repositório é um **livro prático em capítulos**. Construímos juntos uma pequena aplicação web (um validador de CPF e e-mail) e usamos cada etapa para demonstrar um conceito da disciplina: testes automatizados, TDD, qualidade de código, CI/CD, deploy automatizado e workflow de Pull Requests.

A ideia é que você **leia e execute cada capítulo em ordem**, terminando com um projeto completo que você reproduziu do zero.

🌐 **Demo público**: `https://<seu-usuario>.github.io/tqs-2026/`

---

## 📖 Sumário do livro

| # | Capítulo | O que você aprende |
|---|---|---|
| 1 | [Visão geral](capitulos/01-visao-geral.md) | Sobre a aplicação, decisões arquiteturais, stack |
| 2 | [Preparando o ambiente](capitulos/02-preparando-ambiente.md) | Pré-requisitos (Git, Python, IDE), criar repo, venv |
| 3 | [Rodando a aplicação](capitulos/03-rodando-aplicacao.md) | Subir o Flask local, testar manualmente, entender o fluxo |
| 4 | [Testes automatizados](capitulos/04-testes-automatizados.md) | Unitários vs integração, pytest, cobertura, `parametrize` |
| 5 | [TDD na prática](capitulos/05-tdd-na-pratica.md) | Ciclo Red→Green→Refactor, walkthrough completo |
| 6 | [Qualidade de código](capitulos/06-qualidade-de-codigo.md) | ruff (lint+format), bandit (segurança), cobertura como portão |
| 7 | [CI com GitHub Actions](capitulos/07-ci-github-actions.md) | Pipeline `ci.yml` linha-a-linha, lendo logs de falha |
| 8 | [Deploy automatizado](capitulos/08-deploy-automatizado.md) | GitHub Pages, workflow `deploy.yml`, configuração inicial |
| 9 | [Pull Requests](capitulos/09-pull-requests.md) | Fluxo de PR, branch protection, code review, CODEOWNERS |
| 10 | [Atividade prática](capitulos/10-atividade-pratica.md) | 5 tarefas hands-on (CNPJ via TDD, quebrar o CI, etc.) |
| 11 | [Recursos & Licença](capitulos/11-recursos-e-licenca.md) | Documentação, bibliografia, para ir além |

> 💡 Cada capítulo tem navegação **anterior ↔ próximo**, então você pode lê-los de ponta a ponta como um livro.

---

## ⚡ Quick start

Você tem **três caminhos** para acompanhar este livro (detalhes no [capítulo 2](capitulos/02-preparando-ambiente.md#21-três-caminhos-possíveis)):

| Caminho | Como | Para quem |
|---|---|---|
| **A** — Navegador puro | Edite tudo em [github.com](https://github.com) (aperta `.` para abrir VS Code web) | Sem instalar nada, qualquer SO |
| **B** — GitHub Codespaces ⭐ | Botão **Code → Codespaces → Create codespace** no repo | **Recomendado para a aula** — zero instalação local, ambiente completo |
| **C** — Instalação local | Comandos abaixo | Mais rápido para iterar, funciona offline |

### Caminho C — local (Linux/Mac)

```bash
git clone https://github.com/SEU-USUARIO/tqs-2026.git
cd tqs-2026
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements-dev.txt

pytest                              # 6 testes, 82% cobertura
flask --app src.app run             # http://localhost:5000
```

No **Windows**, troque a linha do venv por `python -m venv .venv && .venv\Scripts\activate`.

### Verificações que o CI roda (antes de cada commit)

```bash
ruff check . && ruff format --check .
bandit -r src/
pytest --cov=src --cov-fail-under=80
```

---

## 🗂️ Estrutura do repositório

```
tqs-2026/
├── .devcontainer/
│   └── devcontainer.json           # config GitHub Codespaces (Caminho B)
├── .github/
│   ├── workflows/
│   │   ├── ci.yml                  # lint + testes + cobertura
│   │   └── deploy.yml              # deploy GitHub Pages
│   ├── ISSUE_TEMPLATE/             # templates de issue
│   ├── pull_request_template.md    # checklist obrigatório de PRs
│   └── CODEOWNERS                  # quem revisa o quê
├── capitulos/                      # 📖 ESTE LIVRO (11 capítulos)
├── src/
│   ├── validators.py               # ⭐ VERSÃO PRINCIPAL da lógica
│   ├── app.py                      # rotas Flask
│   └── templates/index.html        # formulário (Flask)
├── tests/
│   ├── test_validators.py          # 4 testes unitários
│   └── test_app.py                 # 2 testes de integração
├── docs/                           # publicado no GitHub Pages
│   ├── index.html
│   ├── validators.js               # espelho JS de validators.py
│   └── style.css
├── pyproject.toml                  # config ruff + pytest + coverage
├── requirements.txt                # Flask
├── requirements-dev.txt            # pytest, ruff, bandit
├── LICENSE                         # MIT
└── README.md                       # você está aqui
```

---

## 🎯 Status atual

| Métrica | Valor |
|---|---|
| Testes | **6 passando** (4 unitários + 2 integração) |
| Cobertura | **82%** (piso do CI: 80%) |
| Lint | ✅ ruff sem warnings |
| Segurança | ✅ bandit sem issues |

> Por que só 6 testes? A suíte é proposital­mente enxuta — o objetivo é que você **leia, entenda e expanda**. A [atividade prática](capitulos/10-atividade-pratica.md) pede para você adicionar testes de casos de borda (todos dígitos iguais, tamanho errado, etc.) usando TDD.

---

## 📜 Licença

[MIT](LICENSE) — use, modifique e distribua livremente, inclusive em sala de aula.

---

**Comece a leitura** → [Capítulo 1 — Visão geral ➡](capitulos/01-visao-geral.md)
