# Preparação Zend Certified PHP Engineer (PHP 8.4)

Repositório para organizar meu estudo para a certificação **Zend PHP Certified Engineer**, versão cobrindo **PHP 8.4**.

## Objetivo

- Consolidar conhecimento de PHP “puro” (sem framework) com foco nos tópicos da prova:
  - PHP Basics, Functions, Arrays, Strings/Patterns
  - Data Formats and Types
  - Web Features
  - Object-Oriented Programming
  - Security
  - I/O (filesystem, streams, JSON/XML)
  - Databases and SQL (PDO)
  - Error Handling
  - Outros conceitos correlatos (SPL, autoload, etc.)
- Atingir **≥ 85%** de acerto em simulados internos antes de comprar o voucher da prova.

---

## Estrutura do Repositório

```text
.
├─ README.md                 # Este arquivo: visão geral + progresso
├─ notes/                    # Anotações, progresso diário, resumos
│  ├─ 2026-01-05-mini-simulado.md
│  └─ roadmap.md
├─ snippets/                 # Snippets PHP pequenos para testar comportamento
│  ├─ basics/
│  ├─ arrays/
│  ├─ oop/
│  ├─ error-handling/
│  └─ ...
├─ katas/                    # Exercícios mais completos (katas)
│  ├─ week1-basics-functions/
│  ├─ week2-oop-spl/
│  ├─ week3-web-security-io/
│  └─ week4-pdo-sql-review/
└─ mock/                     # Mini-simulados e simulados completos
   ├─ mini-simulados/
   └─ full-simulados/
```

## Plano de Estudo (alto nível)

Planejado inicialmente para ~4 semanas, 5 dias por semana, ~4h/dia.

- Semana 1 – Basics, Types, Functions, Arrays, Strings/Patterns
- Semana 2 – OOP (sem framework), Traits, SPL, Error Handling/Exceptions
- Semana 3 – Web Features (superglobals, sessions, cookies, uploads), Security, I/O, JSON/XML, Date/Time
- Semana 4 – Databases/PDO/SQL + Revisão geral + Simulados internos
  Detalhamento do plano por dia ficará em [notes/roadmap.md](notes/roadmap.md).

## Progresso

| Data       | Atividade                                                                                       | Arquivo/Notas                                                            | Status       |
| ---------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ------------ |
| 2026-01-05 | Mini-simulado diagnóstico inicial ([mini-simulado-01](mock/mini-simulados/mini-simulado-01.md)) | [`notes/2026-01-05-mini-simulado.md`](notes/2026-01-05-mini-simulado.md) | ✅ Concluído |

> **Convenção de status:**
> ✅ Concluído
> 🟡 Em andamento
> ⏳ Planejado

À medida que eu for estudando, cada sessão relevante ganha:

- um arquivo `.md` em `notes/` com resumo/insights,
- uma linha nesta tabela com link para o arquivo.

Um acompanhamento detalhado dos simulados pode ser visto em [mock/README.md](mock/README.md)

## Como usar este repositório

- Durante o estudo diário
  - Criar/atualizar snippets em `snippets/` para testar comportamentos.
  - Guardar exercícios mais longos em `katas/`.
  - Documentar o que foi estudado no dia em um arquivo novo em `notes/` (ou atualizar o do dia).
  - Atualizar a tabela de progresso acima.
- Revisões
  - Ler os `.md` em `notes/`, especialmente:
    - pegadinhas (comparação, operadores, strict_types),
    - pontos onde errei em simulados/katas.
- Pré-prova
  - Usar mock/ para concentrar mini-simulados e ver evolução de percentual de acerto.
