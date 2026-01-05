# 2026-01-05 – Mini-simulado diagnóstico ZCP 8.4

## Contexto

Primeira sessão de diagnóstico para preparação da certificação **Zend PHP Certified Engineer** (PHP 8.4).  
Objetivo: medir nível atual “em modo prova” e identificar pontos fortes/fracos para guiar o plano de estudo.

- Formato: mini-simulado com 24 questões de múltipla escolha
- Tópicos abordados:
  - PHP Basics, strict_types, coerção
  - Arrays, Strings, Operadores (`?:`, `??`, truthiness)
  - Functions, closures, variadic
  - OOP (herança, traits, SPL básica)
  - Error Handling (exceptions, Error em PHP 8+)
  - Web Features (superglobals, uploads, sessions)
  - Security (password_hash, filter_input)
  - JSON, DateTimeImmutable
  - PDO (prepared statements, error mode)

---

## Resultado

- **Acertos:** 18 de 24
- **Percentual:** ~75%

Este resultado, sem preparação específica para o exame, confirma nível sólido de experiência prática (coerente com ~10 anos de PHP) e serve como linha de base para evolução até ≥ 85–90% de acerto nos simulados internos.

---

## Análise por tópico

### Pontos fortes (acertou com segurança)

- **OOP**

  - Herança, `parent::`, overriding (Q10)
  - Traits e resolução de conflitos com `insteadof` (Q11)
  - SPL básica com `IteratorAggregate` + `ArrayIterator` (Q12)

- **Error Handling / Exceptions**

  - Comportamento de `DivisionByZeroError` em PHP 8+ (Q13)
  - Execução de `finally` mesmo após `return` no `catch` (Q14)

- **Web Features / Security**

  - Uso correto de `$_FILES` em uploads (Q15)
  - Boas práticas de sessão com `session_regenerate_id(true)` (Q16)
  - `password_hash` / `password_verify` (Q17)
  - `filter_input` com `FILTER_VALIDATE_EMAIL` (Q18)

- **Data / I/O / DB**

  - `DateTimeImmutable::modify` não altera o objeto original (Q20)
  - Benefício principal de prepared statements em PDO (SQL Injection) (Q21)

- **Fundamentos**
  - Comparação fraca/forte e `empty` com `"0"` e `0` (Q2)
  - `isset` vs `array_key_exists` (Q3)
  - `match` estrito (Q5)
  - `strpos` retornando `0` (falsy) e if errado (Q23)
  - Nullsafe operator com `?->` e `??` (Q24)

### Pontos a reforçar (erros identificados)

1. **Arrays – operador `+` vs `array_merge` (Q4)**

   - `+$b` faz **união de arrays**, preservando valores de `$a` para chaves existentes e adicionando apenas chaves ausentes de `$b`.
   - Foi respondida a saída equivalente a `array_merge`, o que indica confusão entre os dois comportamentos.

2. **Operadores lógicos / ternário / null coalescing (Q6)**

   - Diferença entre:
     - `?:` (testa truthiness – 0 é falsy)
     - `??` (testa apenas null/indefinido – 0 é considerado valor válido).
   - Na questão: `0 ?: 'A'` vs `0 ?? 'B'` → resultado real `A0`, não `AB`.

3. **Coerção de tipos com type hints e strict_types off (Q7)**

   - `strict_types` desabilitado: parâmetros escalares (`int`, `float`, etc.) recebem coerção implícita quando possível.
   - `sum(1, 2, '3')` com `int ...$nums` é válido e resulta em `6`, sem warning.

4. **Closures – captura por valor vs referência (Q8)**

   - `use ($count)`: captura por **valor**, incrementa apenas a cópia interna da closure.
   - O resultado esperado era `0`; a resposta assumiu algum efeito sobre a variável externa (`1`).

5. **JSON e erros de encoding (Q19)**

   - Strings com bytes inválidos para UTF-8 fazem `json_encode` retornar `false`.
   - `json_last_error()` fica diferente de `JSON_ERROR_NONE`.
   - A resposta assumiu `null` e `JSON_ERROR_SYNTAX`, mas o retorno típico é `false`.

6. **PDO error mode (Q22)**
   - Modo recomendado para tratamento via exceptions:
     - `PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION`
   - A resposta escolheu `ERRMODE_WARNING`, que apenas emite warnings.

---

## Ações recomendadas (próximos passos de estudo)

1. **Operadores, tipos e coerção**

   - Revisar:
     - `?:` (ternário), `??`, `??=`, `and/or` vs `&&/||`
     - truthiness de `0`, `"0"`, `""`, `null`, `[]`
     - diferença de comportamento com `declare(strict_types=1)` on/off.
   - Criar snippets específicos em `snippets/basics/` para:
     - comparar `?:` vs `??` com diferentes valores;
     - testar comportamento de funções tipadas com `strict_types` ligado e desligado.

2. **Arrays**

   - Revisar em `snippets/arrays/`:
     - `array_merge` vs operador `+` com diferentes chaves (numéricas/string).
   - Anotar exemplos típicos de prova em `notes/` (diferença prática entre os dois).

3. **Closures**

   - Exercitar:
     - `use ($var)` vs `use (&$var)`, em `snippets/functions/closures.php`.
   - Garantir entendimento de que a captura padrão é por valor (cópia).

4. **JSON e erros**

   - Criar exemplos em `snippets/io/json.php` testando:
     - strings válidas vs inválidas em UTF-8;
     - leitura de `json_last_error()` e `json_last_error_msg()`.

5. **PDO error mode**
   - Em `snippets/pdo/connection.php`, setar sempre:
     ```php
     $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
     ```
   - Anotar em `notes/` como “modo padrão recomendado para prova”.

---

## Conclusão

- Nível atual: **bom** (≈75% de acerto em simulado diagnóstico) com forte base em OOP, exceptions, sessões, segurança básica e uso geral de PHP.
- Pontos fracos mapeados:
  - nuances de operadores/ truthiness,
  - diferenças finas de funções/operadores de arrays,
  - detalhes de captura em closures,
  - tratamento de erro em JSON,
  - configuração recomendada de PDO.

Esses pontos serão priorizados nos primeiros dias do plano intensivo de estudo, para fechar rapidamente as lacunas antes de partir para simulados maiores e revisão geral.
