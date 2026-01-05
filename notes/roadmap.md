# Roadmap de Estudo – Zend PHP Certified Engineer (PHP 8.4)

Este arquivo organiza o plano de estudo em **4 semanas** (flexíveis), com foco em:

- Cobrir todos os tópicos que a Zend lista para a prova (até PHP 8.4)
- Priorizar pontos fracos identificados no mini-simulado inicial
- Centralizar o que deve ser produzido em `notes/`, `snippets/` e `katas/`

Use as checkboxes `[ ]` → `[x]` conforme for concluindo as sessões.

---

## Legenda

- **Sessão**: bloco de estudo (~3–4h), não necessariamente um dia fixo de calendário.
- Sempre que uma sessão for concluída:
  - Criar/atualizar um arquivo em `notes/` com o resumo (ex: `2026-01-06-basics.md`)
  - Atualizar a tabela de progresso no `README.md`
  - Criar/atualizar snippets/katas quando indicado

Sugestão de pastas:

- `snippets/basics/`, `snippets/arrays/`, `snippets/functions/`, `snippets/oop/`, etc.
- `katas/week1-basics-functions/` etc.

---

## Semana 0 – Setup & Diagnóstico

Objetivo: configurar ambiente, repositório e obter linha de base de conhecimento.

- [ ] **S0.1 – Setup do repositório e ambiente**
  - [x] Criar repositório `zcp-8.4-prep` no GitHub
  - [x] Criar estrutura inicial de pastas:
    - `notes/`, `snippets/`, `katas/`, `mock/`
  - [ ] Configurar PHP 8.x (idealmente 8.4) com:
    - `error_reporting = E_ALL`
    - `display_errors = 1` (ambiente local)
  - [x] Atualizar `README.md` com:
    - Objetivo
    - Estrutura de pastas
    - Link para `notes/roadmap.md`
- [x] **S0.2 – Mini-simulado diagnóstico**
  - [x] Registrar resultado do mini-simulado em  
         [`notes/2026-01-05-mini-simulado.md`](2026-01-05-mini-simulado.md)
  - [x] Anotar principais pontos fracos:
    - Operadores (`?:`, `??`, truthiness)
    - Arrays (`+` vs `array_merge`)
    - Closures (`use` por valor vs referência)
    - JSON (`json_encode` + `json_last_error`)
    - PDO error mode (`ERRMODE_EXCEPTION`)

---

## Semana 1 – Basics, Types, Functions, Arrays, Strings/Patterns

Foco especial nos pontos fracos identificados: operadores, coerção, arrays, closures.

### Sessão 1 – Operadores, Types, Coerção, strict_types

- [ ] Leitura
  - [ ] Manual PHP: tipos, casting, comparação, operadores (`?:`, `??`, `&&`, `||`, `and`, `or`)
  - [ ] `declare(strict_types=1)` e efeitos em parâmetros/retornos
- [ ] Prática (`snippets/basics/`)
  - [ ] Criar ~10 snippets cobrindo:
    - Comparação fraca/forte com `"0"`, `0`, `""`, `null`, `[]`
    - `?:` vs `??` vs `??=` com valores `0`, `null`, string vazia
  - [ ] Criar ~5 snippets comparando comportamento com e sem `strict_types`
- [ ] Notas
  - [ ] Criar/atualizar `notes/20xx-xx-xx-basics-operators.md` com:
    - Exemplos de pegadinhas e resultados esperados

### Sessão 2 – Functions, parâmetros, variadic, strict_types

- [ ] Leitura
  - [ ] Funções: parâmetros (default, variadic, named), tipos de retorno, union types
- [ ] Prática (`snippets/functions/`)
  - [ ] Implementar funções que:
    - Usem variadic + type hints inteiros (testar com e sem `strict_types`)
    - Usem named arguments e tipos de retorno
- [ ] Notas
  - [ ] Resumir diferença de comportamento de type hints com `strict_types` on/off

### Sessão 3 – Closures, captura por valor vs referência, generators

- [ ] Leitura
  - [ ] Documentação de closures, `use ($var)` vs `use (&$var)`
  - [ ] Arrow functions e diferenças p/ closures normais
  - [ ] Generators (`yield`, `yield from`) – visão geral
- [ ] Prática (`snippets/functions/closures.php`)
  - [ ] Criar exemplos que mostrem claramente:
    - `use ($count)` (captura por valor)
    - `use (&$count)` (captura por referência)
- [ ] Notas
  - [ ] Registrar exemplos típicos de prova com closures e escopo

### Sessão 4 – Arrays (incluindo `+` vs `array_merge`, sort, funções úteis)

- [ ] Leitura
  - [ ] Arrays: chaves numéricas/string, `array_merge`, operador `+`
  - [ ] Funções: `array_map`, `array_filter`, `array_reduce`, `sort`, `asort`, `usort`
- [ ] Prática (`snippets/arrays/`)
  - [ ] Snippets comparando:
    - `array_merge($a, $b)` vs `$a + $b` com chaves numéricas e string
  - [ ] Exercícios de ordenação com callbacks (`usort`)
- [ ] Notas
  - [ ] Tabela/resumo: diferenças práticas entre `array_merge` e `+`

### Sessão 5 – Strings e Patterns (Regex/PCRE)

- [ ] Leitura
  - [ ] Strings: interpolação, heredoc/nowdoc, funções principais
  - [ ] PCRE: `preg_match`, `preg_replace`, quantificadores, grupos, flags básicas
- [ ] Prática (`snippets/strings/`, `snippets/patterns/`)
  - [ ] Criar ~10 exercícios de manipulação de string
  - [ ] Criar ~10 regex para validação/extração
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-strings-patterns.md` com os padrões mais usados e armadilhas

---

## Semana 2 – OOP, Traits, SPL, Error Handling

### Sessão 6 – OOP: classes, herança, interfaces, polimorfismo

- [ ] Leitura
  - [ ] Classes, herança, visibilidade, `final`, `abstract`
  - [ ] Interfaces, polimorfismo, `instanceof`
- [ ] Prática (`katas/week2-oop-spl/`)
  - [ ] Modelar um domínio simples (ex: pagamento, notificação) só com PHP puro
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-oop-basics.md` com exemplos de herança e contratos

### Sessão 7 – Traits, static/self, late static binding, magic methods

- [ ] Leitura
  - [ ] Traits: conflitos, `insteadof`, `as`
  - [ ] `self` vs `static`, late static binding
  - [ ] Métodos mágicos (`__get`, `__set`, `__call`, `__invoke`, `__toString`, `__clone`)
- [ ] Prática (`snippets/oop/traits.php`, `snippets/oop/magic-methods.php`)
  - [ ] Exemplos de traits com conflito resolvido
  - [ ] Classe usando `__get/__set` para logging ou lazy-loading
- [ ] Notas
  - [ ] Registrar padrões comuns de questões envolvendo traits e magic methods

### Sessão 8 – SPL: Iterator, IteratorAggregate, ArrayAccess, Countable

- [ ] Leitura
  - [ ] SPL: `Iterator`, `IteratorAggregate`, `ArrayAccess`, `Countable`
  - [ ] `ArrayIterator`, `SplFileObject` (visão geral)
- [ ] Prática (`katas/week2-oop-spl/collection.php`)
  - [ ] Implementar `Collection` iterável, contável e acessível como array
- [ ] Notas
  - [ ] Resumir quais interfaces SPL são mais prováveis de cair

### Sessão 9 – Error Handling, Exceptions, set_error_handler

- [ ] Leitura
  - [ ] Diferença entre `Error` e `Exception` em PHP 8+
  - [ ] `TypeError`, `ValueError`, `DivisionByZeroError`
  - [ ] `set_error_handler`, `set_exception_handler`
- [ ] Prática (`snippets/error-handling/`)
  - [ ] Exemplos de divisão por zero, type mismatch, etc.
  - [ ] Transformar warnings em exceptions com `set_error_handler`
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-error-handling.md` com matriz: situação → tipo de erro

### Sessão 10 – Namespaces, Autoload, visão geral de Reflection

- [ ] Leitura
  - [ ] Namespaces, `use`, resolução de nomes
  - [ ] `spl_autoload_register`, PSR-4 (conceito)
  - [ ] Reflection (só visão geral)
- [ ] Prática (`snippets/oop/autoload.php`)
  - [ ] Implementar autoloader simples sem Composer
- [ ] Notas
  - [ ] Dicas de prova envolvendo namespaces e autoload

---

## Semana 3 – Web Features, Security, I/O, JSON/XML, Date/Time

### Sessão 11 – Superglobals, headers, fluxo de request

- [ ] Leitura
  - [ ] `$_GET`, `$_POST`, `$_COOKIE`, `$_FILES`, `$_SERVER`
  - [ ] `header()`, status HTTP, noção de output buffering
- [ ] Prática (`katas/week3-web-security-io/`)
  - [ ] Script simples que lê GET/POST e retorna JSON com headers corretos
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-web-basics.md` com principais chaves de `$_SERVER` e uso de `header()`

### Sessão 12 – Sessions e Cookies, segurança básica de sessão

- [ ] Leitura
  - [ ] `session_start`, `session_regenerate_id`, cookie de sessão
  - [ ] Riscos comuns: fixation, hijacking
- [ ] Prática
  - [ ] Mini login com:
    - regeneração de ID após login
    - flags de cookie de sessão (conceitual: HttpOnly, Secure, SameSite)
- [ ] Notas
  - [ ] Boas práticas de sessão para prova

### Sessão 13 – Security: password_hash, filter_input, hash_hmac

- [ ] Leitura
  - [ ] `password_hash`, `password_verify`, `password_needs_rehash`
  - [ ] `filter_input`, `filter_var`
  - [ ] `hash_hmac`, `hash_equals`
- [ ] Prática (`snippets/security/`)
  - [ ] Fluxo de registro/login usando `password_hash`
  - [ ] Validação de inputs com `filter_input`
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-security.md` com padrões recomendados

### Sessão 14 – I/O, JSON, XML

- [ ] Leitura
  - [ ] Filesystem: `fopen`, `fread`, `fwrite`, `file_get_contents`
  - [ ] Streams/wrappers (visão geral)
  - [ ] `json_encode`, `json_decode`, `json_last_error`, `json_last_error_msg`
  - [ ] Noções de XML e riscos (XXE, conceitual)
- [ ] Prática (`snippets/io/`)
  - [ ] Snippets com:
    - JSON válido vs inválido (especialmente UTF-8 quebrado)
    - Tratamento de erro com `json_last_error`
- [ ] Notas
  - [ ] Resumo específico sobre comportamento de `json_encode` com dados inválidos

### Sessão 15 – DateTime / DateTimeImmutable

- [ ] Leitura
  - [ ] `DateTime` vs `DateTimeImmutable`
  - [ ] `modify`, timezones, `DateInterval`
- [ ] Prática (`snippets/datetime/`)
  - [ ] Funções para normalizar timezone e calcular diferenças
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-datetime.md` com exemplos de uso mais prováveis

---

## Semana 4 – PDO, SQL, Revisão & Simulados internos

### Sessão 16 – PDO basics, DSN, prepared statements

- [ ] Leitura
  - [ ] Criação de conexão via PDO, DSN, credenciais
  - [ ] `prepare`, `execute`, `bindParam`, `bindValue`
  - [ ] `ATTR_ERRMODE` (focar em `ERRMODE_EXCEPTION`)
- [ ] Prática (`katas/week4-pdo-sql-review/`)
  - [ ] CRUD simples com PDO usando prepared statements
  - [ ] Exemplo explícito configurando `ERRMODE_EXCEPTION`
- [ ] Notas
  - [ ] `notes/20xx-xx-xx-pdo.md` com resumo de boas práticas

### Sessão 17 – SQL básico e transações (visão de prova)

- [ ] Leitura
  - [ ] SELECT, WHERE, JOIN simples, ORDER BY, LIMIT
  - [ ] Transações: begin/commit/rollback em PDO
- [ ] Prática
  - [ ] Exemplos de queries típicas e uso de transação em operação com múltiplos updates/inserts
- [ ] Notas
  - [ ] Checklist de “itens que a prova pode cobrar” em SQL

### Sessão 18 – Revisão dirigida por tópico

- [ ] Revisar `notes/` tema a tema:
  - [ ] Basics/Operators/Types/Functions/Arrays/Strings/Patterns
  - [ ] OOP/Traits/SPL/Error Handling
  - [ ] Web/Sessions/Cookies/Security/I/O/JSON/XML/DateTime
  - [ ] PDO/SQL
- [ ] Identificar temas com mais dúvida/erros e marcar para revisão extra

### Sessão 19 – Consolidar pegadinhas (cheat sheet)

- [ ] Criar `notes/cheat-sheet-pegadinhas.md` com:
  - [ ] Comparação fraca vs forte e truthiness
  - [ ] `?:` vs `??` vs `??=`
  - [ ] `array_merge` vs `+`
  - [ ] Closures (valor vs referência)
  - [ ] `json_encode` + `json_last_error`
  - [ ] `ERRMODE_EXCEPTION` em PDO
  - [ ] Nullsafe operator + `??`
  - [ ] Outros pontos que aparecerem ao longo do estudo

### Sessão 20 – Simulado interno + ajuste final

- [ ] Montar ou refazer um conjunto de questões internas (mini-simulado)
  - [ ] Misturar questões de todos os tópicos
  - [ ] Registrar desempenho e dúvidas em um novo `.md` em `notes/`
- [ ] Ajustar roadmap se decidir estender estudo antes de comprar o voucher

---

## Observação final

Este roadmap é flexível.  
Se alguma sessão se mostrar muito tranquila, você pode:

- Juntar duas sessões em um dia, ou
- Usar o tempo extra para reforçar os tópicos que mais errar nos seus próprios exercícios e anotações.

A cada nova sessão importante, lembre de:

1. Criar/atualizar o `.md` correspondente em `notes/`
2. Atualizar a tabela de progresso no `README.md` com link para esse arquivo
