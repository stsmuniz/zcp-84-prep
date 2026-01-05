# Mini-simulado 01 – ZCP 8.4 (Diagnóstico)

Formato: múltipla escolha, 24 questões, alternativas A–D.  
Ideal para uso como diagnóstico ou revisão.

---

## 1. strict_types e coerção

```php
<?php
declare(strict_types=1);

function foo(int $x): int {
    return $x * 2;
}

echo foo("3");
```

O que acontece?

A. Imprime `6`  
B. Imprime `33`  
C. Lança `TypeError`  
D. Imprime nada e termina silenciosamente

---

## 2. Comparação fraca/forte e empty

```php
<?php
$a = "0";
$b = 0;

var_dump(
    $a == $b,
    $a === $b,
    empty($a),
    empty($b)
);
```

Saída?

A.

```text
bool(true)
bool(false)
bool(false)
bool(true)
```

B.

```text
bool(true)
bool(false)
bool(true)
bool(true)
```

C.

```text
bool(false)
bool(false)
bool(true)
bool(false)
```

D.

```text
bool(true)
bool(true)
bool(true)
bool(true)
```

---

## 3. isset vs array_key_exists

```php
<?php
$arr = [
    'a' => 0,
    'b' => null,
];

echo isset($arr['a']) ? '1' : '0';
echo isset($arr['b']) ? '1' : '0';
echo array_key_exists('b', $arr) ? '1' : '0';
```

Saída?

A. `110`  
B. `101`  
C. `010`  
D. `111`

---

## 4. array_merge vs operador +

```php
<?php
$a = [1 => 'a', 2 => 'b'];
$b = [1 => 'c', 3 => 'd'];

print_r($a + $b);
```

Saída de forma simplificada?

A. `[1 => 'a', 2 => 'b', 3 => 'd']`  
B. `[1 => 'c', 2 => 'b', 3 => 'd']`  
C. `[0 => 'a', 1 => 'b', 2 => 'c', 3 => 'd']`  
D. `[1 => 'a', 1 => 'c', 2 => 'b', 3 => 'd']`

---

## 5. match é estrito

```php
<?php
$x = '1';

$result = match ($x) {
    1   => 'int',
    '1' => 'string',
    default => 'other',
};

echo $result;
```

O que é impresso?

A. `int`  
B. `string`  
C. `other`  
D. Gera `TypeError`

---

## 6. Ordem de avaliação (?? e ?:)

```php
<?php
$value = 0;

$result = $value ?: 'A';
$result2 = $value ?? 'B';

echo $result . $result2;
```

Saída?

A. `AB`  
B. `0B`  
C. `A0`  
D. `00`

---

## 7. Função com parâmetro variádico

```php
<?php
function sum(int ...$nums): int {
    return array_sum($nums);
}

echo sum(1, 2, '3');
```

Com `strict_types` **desabilitado** (padrão), o que acontece?

A. Imprime `6`  
B. Imprime `33`  
C. Lança `TypeError`  
D. Lança `Warning` mas imprime `6`

---

## 8. Closures e captura por referência (1)

```php
<?php
$count = 0;

$inc = function() use ($count) {
    $count++;
};

$inc();
$inc();

echo $count;
```

Saída?

A. `0`  
B. `1`  
C. `2`  
D. Depende da versão do PHP

---

## 9. Closures e captura por referência (2)

```php
<?php
$count = 0;

$inc = function() use (&$count) {
    $count++;
};

$inc();
$inc();

echo $count;
```

Saída?

A. `0`  
B. `1`  
C. `2`  
D. Gera erro de escopo

---

## 10. OOP / herança simples

```php
<?php
class A {
    public function foo(): string {
        return 'A';
    }
}

class B extends A {
    public function foo(): string {
        return 'B' . parent::foo();
    }
}

echo (new B())->foo();
```

Saída?

A. `A`  
B. `B`  
C. `BA`  
D. `AB`

---

## 11. Traits e conflitos

```php
<?php
trait T1 {
    public function hello() {
        return 'T1';
    }
}

trait T2 {
    public function hello() {
        return 'T2';
    }
}

class C {
    use T1, T2 {
        T1::hello insteadof T2;
    }
}

echo (new C())->hello();
```

Saída?

A. `T1`  
B. `T2`  
C. Erro fatal de conflito de métodos  
D. `T1T2`

---

## 12. IteratorAggregate

```php
<?php
class Numbers implements IteratorAggregate {
    private array $items = [1, 2, 3];

    public function getIterator(): Traversable {
        return new ArrayIterator($this->items);
    }
}

$sum = 0;
foreach (new Numbers() as $n) {
    $sum += $n;
}
echo $sum;
```

Saída?

A. `0`  
B. `3`  
C. `6`  
D. Erro de tipo em getIterator

---

## 13. Error handling: divisão por zero

```php
<?php
function test() {
    $a = 1 / 0;
    echo "Done";
}

test();
```

Assumindo configurações padrão, o que acontece em PHP 8+?

A. Erro fatal, nada é impresso  
B. Warning é emitido, mas `Done` é impresso  
C. Lança `DivisionByZeroError` e nada é impresso  
D. Lança `DivisionByZeroError` e `Done` é impresso

---

## 14. Exceptions e finally

```php
<?php
function f() {
    try {
        throw new RuntimeException("fail");
    } catch (Exception $e) {
        echo "catch";
        return;
    } finally {
        echo "finally";
    }
}

f();
```

Saída?

A. `catch`  
B. `finally`  
C. `catchfinally`  
D. `finallycatch`

---

## 15. Superglobals e upload

Em um script de upload, qual é a forma correta de acessar informações sobre o arquivo enviado?

A. `$_POST['file']`  
B. `$_GET['file']`  
C. `$_FILES['file']`  
D. `$_SERVER['file']`

---

## 16. Sessions e segurança

Qual das opções **melhor** descreve uma boa prática ao autenticar um usuário com `session_start()`?

A. Não é necessário fazer nada após login; o ID de sessão atual é seguro  
B. Chamar `session_regenerate_id(true)` após login para mitigar fixation  
C. Apagar o cookie de sessão manualmente com `setcookie()`  
D. Mudar apenas o nome da sessão com `session_name()`

---

## 17. password_hash / password_verify

Escolha a afirmação **correta**:

A. `password_hash()` sempre gera o mesmo hash para a mesma senha  
B. `password_verify()` compara a senha em texto puro com o hash e considera o salt embutido no hash  
C. `password_hash()` exige que você forneça manualmente o salt  
D. `password_verify()` só funciona com `md5()`

---

## 18. filter_var e filter_input

Para validar um e-mail vindo de `$_POST['email']` usando filtros nativos, qual é a forma mais adequada?

A.

```php
filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);
```

B.

```php
filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
```

C.

```php
filter_input(INPUT_GET, 'email', FILTER_SANITIZE_EMAIL);
```

D.

```php
htmlspecialchars($_POST['email'], ENT_QUOTES);
```

---

## 19. JSON e erros

```php
<?php
$data = "\xB1\x31"; // sequência inválida para UTF-8

$json = json_encode($data);
var_dump($json, json_last_error());
```

O que é mais provável em PHP 8+?

A. `$json` é uma string JSON válida e `json_last_error()` retorna `JSON_ERROR_NONE`  
B. `$json` é `false` e `json_last_error()` é diferente de `JSON_ERROR_NONE`  
C. `$json` é `null` e `json_last_error()` é `JSON_ERROR_SYNTAX`  
D. Lança Exception automaticamente

---

## 20. DateTimeImmutable

```php
<?php
$dt = new DateTimeImmutable('2024-01-01 12:00:00', new DateTimeZone('UTC'));
$dt2 = $dt->modify('+1 day');

echo $dt->format('Y-m-d H:i') . ' | ' . $dt2->format('Y-m-d H:i');
```

Saída?

A. `2024-01-02 12:00 | 2024-01-02 12:00`  
B. `2024-01-01 12:00 | 2024-01-02 12:00`  
C. `2024-01-01 12:00 | 2024-01-01 12:00`  
D. Depende do timezone do PHP.ini

---

## 21. PDO e prepared statements

Qual é a principal vantagem de usar prepared statements com PDO?

A. Melhorar apenas a performance, sem impacto em segurança  
B. Reduzir a necessidade de índices no banco  
C. Ajudar a prevenir SQL Injection ao separar a query dos dados  
D. Permitir usar qualquer driver de banco sem DSN

---

## 22. PDO error mode

Qual é o modo de erro recomendado para tratar erros de PDO de forma estruturada via Exceptions?

A.

```php
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_SILENT);
```

B.

```php
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_WARNING);
```

C.

```php
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

D. Nenhum; o modo padrão já lança Exception

---

## 23. Strings: strpos

```php
<?php
$pos = strpos("foobar", "foo");

if ($pos) {
    echo "found";
} else {
    echo "not found";
}
```

Saída?

A. `found`  
B. `not found`  
C. Warning e nenhuma saída  
D. Depende da posição da substring

---

## 24. Nullsafe operator

```php
<?php
class User {
    public ?Address $address = null;
}

class Address {
    public string $city;
    public function __construct(string $city) {
        $this->city = $city;
    }
}

$user = new User();
echo $user?->address?->city ?? 'N/A';
```

Saída?

A. Erro fatal ao acessar propriedade de null  
B. `null`  
C. `N/A`  
D. String vazia

---

## Gabarito

[Gabarito](gabaritos/mini-simulado-01.txt)
