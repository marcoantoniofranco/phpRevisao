# 🚨 TODOS OS ERROS POSSÍVEIS - PROVA PHP

## 📋 ÍNDICE RÁPIDO DE ERROS (CTRL+F)

### 🔧 **ERROS DE CONEXÃO COM BANCO**

- [Connection refused](#connection-refused)
- [Access denied](#access-denied)
- [Unknown database](#unknown-database)
- [No database selected](#no-database-selected)
- [Can't connect to MySQL server](#cant-connect-to-mysql-server)

### 🔐 **ERROS DE SESSÃO**

- [session_start()](#session_start)
- [Cannot send session cookie](#cannot-send-session-cookie)
- [headers already sent](#headers-already-sent)

### 📝 **ERROS DE VARIÁVEIS**

- [Undefined index](#undefined-index)
- [Undefined variable](#undefined-variable)
- [Undefined offset](#undefined-offset)
- [Notice: Trying to get property](#notice-trying-to-get-property)

### 💾 **ERROS DE BANCO DE DADOS**

- [Call to a member function](#call-to-a-member-function)
- [fetch_object() on boolean](#fetch_object-on-boolean)
- [Table doesn't exist](#table-doesnt-exist)
- [Unknown column](#unknown-column)
- [You have an error in your SQL syntax](#you-have-an-error-in-your-sql-syntax)

### ⚙️ **ERROS DE FUNÇÃO**

- [Call to undefined function](#call-to-undefined-function)
- [Fatal error: Cannot redeclare](#fatal-error-cannot-redeclare)
- [Too few arguments](#too-few-arguments)

### 🔄 **ERROS DE SINTAXE**

- [Parse error](#parse-error)
- [syntax error, unexpected](#syntax-error-unexpected)
- [Missing argument](#missing-argument)

### 📊 **ERROS DE ARRAY**

- [Array to string conversion](#array-to-string-conversion)
- [Invalid argument supplied](#invalid-argument-supplied)

### 🌐 **ERROS DE INCLUDE/REQUIRE**

- [No such file or directory](#no-such-file-or-directory)
- [Failed opening required](#failed-opening-required)

### ⏱️ **ERROS DE EXECUÇÃO**

- [Maximum execution time](#maximum-execution-time)
- [Fatal error: Allowed memory size](#fatal-error-allowed-memory-size)

---

## 🔧 ERROS DE CONEXÃO COM BANCO

### 🔍 **Connection refused**

**Mensagem completa:**

```
mysqli::__construct(): (HY000/2002): Connection refused
```

**Causa:** MySQL não está rodando ou porta errada

**Soluções:**

```php
// ❌ ERRO
$banco = new mysqli("localhost", "root", "", "banco");

// ✅ SOLUÇÃO 1: Verificar porta
$banco = new mysqli("localhost:3307", "root", "", "banco");

// ✅ SOLUÇÃO 2: Testar múltiplas portas
$portas = [3306, 3307, 3308];
foreach ($portas as $porta) {
    $banco = @new mysqli("localhost:$porta", "root", "", "banco");
    if (!$banco->connect_error) {
        echo "Conectado na porta: $porta";
        break;
    }
}

// ✅ SOLUÇÃO 3: Verificar se XAMPP está ligado
// 1. Abrir XAMPP Control Panel
// 2. Start Apache
// 3. Start MySQL
```

### 🔍 **Access denied**

**Mensagem completa:**

```
mysqli::__construct(): (HY000/1045): Access denied for user 'root'@'localhost'
```

**Causa:** Usuário ou senha incorretos

**Soluções:**

```php
// ❌ ERRO
$banco = new mysqli("localhost:3307", "admin", "123", "banco");

// ✅ SOLUÇÃO: No XAMPP sempre usar root sem senha
$banco = new mysqli("localhost:3307", "root", "", "banco");
//                                    ↑      ↑
//                                 usuário senha
//                                 (root)  (vazio)
```

### 🔍 **Unknown database**

**Mensagem completa:**

```
mysqli::__construct(): (HY000/1049): Unknown database 'nome_banco'
```

**Causa:** Banco de dados não existe

**Soluções:**

```php
// ✅ SOLUÇÃO 1: Criar o banco primeiro
$banco = new mysqli("localhost:3307", "root", "");
$banco->query("CREATE DATABASE IF NOT EXISTS meu_banco");
$banco->select_db("meu_banco");

// ✅ SOLUÇÃO 2: Conectar sem banco e depois selecionar
$banco = new mysqli("localhost:3307", "root", "");
if (!$banco->connect_error) {
    $banco->query("USE meu_banco");
}

// ✅ SOLUÇÃO 3: Verificar se banco existe
$banco = new mysqli("localhost:3307", "root", "");
$resultado = $banco->query("SHOW DATABASES LIKE 'meu_banco'");
if ($resultado->num_rows == 0) {
    $banco->query("CREATE DATABASE meu_banco");
}
```

### 🔍 **No database selected**

**Mensagem completa:**

```
No database selected
```

**Causa:** Esqueceu de especificar o banco na conexão

**Soluções:**

```php
// ❌ ERRO
$banco = new mysqli("localhost:3307", "root", "");
$banco->query("SELECT * FROM usuarios"); // Erro!

// ✅ SOLUÇÃO 1: Especificar banco na conexão
$banco = new mysqli("localhost:3307", "root", "", "meu_banco");

// ✅ SOLUÇÃO 2: Selecionar banco depois
$banco = new mysqli("localhost:3307", "root", "");
$banco->select_db("meu_banco");

// ✅ SOLUÇÃO 3: Usar USE no SQL
$banco = new mysqli("localhost:3307", "root", "");
$banco->query("USE meu_banco");
```

### 🔍 **Can't connect to MySQL server**

**Mensagem completa:**

```
Can't connect to MySQL server on 'localhost'
```

**Causa:** MySQL não está rodando ou IP errado

**Soluções:**

```php
// ✅ SOLUÇÃO 1: Testar diferentes IPs
$ips = ["localhost", "127.0.0.1", "::1"];
foreach ($ips as $ip) {
    $banco = @new mysqli("$ip:3307", "root", "", "banco");
    if (!$banco->connect_error) {
        echo "Conectado com: $ip";
        break;
    }
}

// ✅ SOLUÇÃO 2: Verificar se MySQL está rodando
// No Windows: Ctrl+Shift+Esc → Serviços → MySQL

// ✅ SOLUÇÃO 3: Reiniciar XAMPP
// Fechar XAMPP e abrir novamente como Administrador
```

---

## 🔐 ERROS DE SESSÃO

### 🔍 **session_start()**

**Mensagem completa:**

```
Warning: session_start(): Cannot send session cookie - headers already sent
```

**Causa:** Tentou usar session_start() depois de já ter enviado conteúdo

**Soluções:**

```php
// ❌ ERRO
echo "Algo";
session_start(); // Erro!

// ✅ SOLUÇÃO: session_start() SEMPRE no início
<?php
session_start(); // PRIMEIRA linha após <?php
echo "Agora pode usar sessões";
?>

// ✅ SOLUÇÃO 2: Verificar se já foi iniciada
<?php
if (session_status() == PHP_SESSION_NONE) {
    session_start();
}
?>
```

### 🔍 **Cannot send session cookie**

**Mensagem completa:**

```
Warning: Cannot send session cookie - headers already sent by (output started at arquivo.php:5)
```

**Causa:** Já foi enviado HTML antes de session_start()

**Soluções:**

```php
// ❌ ERRO
<!DOCTYPE html>
<html>
<?php session_start(); ?> <!-- Erro! -->

// ✅ SOLUÇÃO: PHP no início
<?php session_start(); ?>
<!DOCTYPE html>
<html>

// ✅ SOLUÇÃO 2: Usar buffer
<?php
ob_start(); // Inicia buffer
echo "Conteúdo";
session_start(); // Agora funciona
ob_end_flush(); // Envia tudo
?>
```

### 🔍 **headers already sent**

**Mensagem completa:**

```
Warning: Cannot modify header information - headers already sent
```

**Causa:** Tentou usar header() depois de já ter enviado conteúdo

**Soluções:**

```php
// ❌ ERRO
echo "Algo";
header("Location: pagina.php"); // Erro!

// ✅ SOLUÇÃO 1: header() antes de qualquer output
<?php
header("Location: pagina.php");
exit; // SEMPRE usar exit!
?>

// ✅ SOLUÇÃO 2: Usar JavaScript se necessário
<?php
echo "Redirecionando...";
echo "<script>window.location='pagina.php';</script>";
?>

// ✅ SOLUÇÃO 3: Usar buffer
<?php
ob_start();
echo "Conteúdo";
header("Location: pagina.php");
ob_end_clean(); // Limpa buffer
exit;
?>
```

---

## 📝 ERROS DE VARIÁVEIS

### 🔍 **Undefined index**

**Mensagem completa:**

```
Notice: Undefined index: nome in arquivo.php on line 5
```

**Causa:** Tentou acessar chave que não existe em $\_GET, $\_POST ou array

**Soluções:**

```php
// ❌ ERRO
$nome = $_GET["nome"]; // Erro se não existir!
$idade = $_POST["idade"]; // Erro se não existir!

// ✅ SOLUÇÃO 1: Usar ?? (null coalescing)
$nome = $_GET["nome"] ?? "Padrão";
$idade = $_POST["idade"] ?? 0;

// ✅ SOLUÇÃO 2: Usar isset()
if (isset($_GET["nome"])) {
    $nome = $_GET["nome"];
} else {
    $nome = "Padrão";
}

// ✅ SOLUÇÃO 3: Verificar se formulário foi enviado
if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $nome = $_POST["nome"] ?? "";
}

// ✅ SOLUÇÃO 4: Para arrays
$array = ["a" => 1, "b" => 2];
$valor = $array["c"] ?? "Não existe";
```

### 🔍 **Undefined variable**

**Mensagem completa:**

```
Notice: Undefined variable: nome in arquivo.php on line 10
```

**Causa:** Tentou usar variável que não foi definida

**Soluções:**

```php
// ❌ ERRO
echo $nome; // Erro se $nome não foi definida!

// ✅ SOLUÇÃO 1: Definir a variável
$nome = "João";
echo $nome;

// ✅ SOLUÇÃO 2: Verificar se existe
if (isset($nome)) {
    echo $nome;
} else {
    echo "Nome não definido";
}

// ✅ SOLUÇÃO 3: Usar ?? com null
$nome = $nome ?? "Padrão";
echo $nome;

// ✅ SOLUÇÃO 4: Inicializar variáveis
$nome = "";
$idade = 0;
$ativo = false;
```

### 🔍 **Undefined offset**

**Mensagem completa:**

```
Notice: Undefined offset: 5 in arquivo.php on line 8
```

**Causa:** Tentou acessar posição que não existe em array

**Soluções:**

```php
// ❌ ERRO
$array = [1, 2, 3];
echo $array[5]; // Erro! Posição 5 não existe

// ✅ SOLUÇÃO 1: Verificar se existe
if (isset($array[5])) {
    echo $array[5];
} else {
    echo "Posição não existe";
}

// ✅ SOLUÇÃO 2: Usar array_key_exists()
if (array_key_exists(5, $array)) {
    echo $array[5];
}

// ✅ SOLUÇÃO 3: Verificar tamanho do array
if (count($array) > 5) {
    echo $array[5];
}

// ✅ SOLUÇÃO 4: Usar ?? para arrays
echo $array[5] ?? "Não existe";
```

### 🔍 **Notice: Trying to get property**

**Mensagem completa:**

```
Notice: Trying to get property 'nome' of non-object
```

**Causa:** Tentou acessar propriedade de algo que não é objeto

**Soluções:**

```php
// ❌ ERRO
$resultado = $banco->query($sql);
$user = $resultado->fetch_object();
echo $user->nome; // Erro se não há resultados!

// ✅ SOLUÇÃO 1: Verificar se é objeto
$resultado = $banco->query($sql);
if ($resultado && $resultado->num_rows > 0) {
    $user = $resultado->fetch_object();
    echo $user->nome;
} else {
    echo "Usuário não encontrado";
}

// ✅ SOLUÇÃO 2: Verificar se objeto existe
$user = $resultado->fetch_object();
if ($user) {
    echo $user->nome;
} else {
    echo "Sem dados";
}

// ✅ SOLUÇÃO 3: Usar isset() em propriedades
if (isset($user->nome)) {
    echo $user->nome;
}
```

---

## 💾 ERROS DE BANCO DE DADOS

### 🔍 **Call to a member function**

**Mensagem completa:**

```
Fatal error: Call to a member function query() on null
```

**Causa:** Tentou usar método em variável que é null

**Soluções:**

```php
// ❌ ERRO
$banco = new mysqli("localhost", "root", "", "banco");
// Se conexão falhar, $banco pode ser null
$banco->query($sql); // Erro!

// ✅ SOLUÇÃO 1: Verificar conexão
$banco = new mysqli("localhost:3307", "root", "", "banco");
if ($banco->connect_error) {
    die("Erro na conexão: " . $banco->connect_error);
}
$banco->query($sql); // Agora é seguro

// ✅ SOLUÇÃO 2: Verificar se objeto existe
if ($banco && !$banco->connect_error) {
    $banco->query($sql);
}

// ✅ SOLUÇÃO 3: Try-catch
try {
    $banco = new mysqli("localhost:3307", "root", "", "banco");
    $banco->query($sql);
} catch (Exception $e) {
    echo "Erro: " . $e->getMessage();
}
```

### 🔍 **fetch_object() on boolean**

**Mensagem completa:**

```
Fatal error: Call to a member function fetch_object() on boolean
```

**Causa:** Query falhou e retornou false

**Soluções:**

```php
// ❌ ERRO
$resultado = $banco->query($sql);
$user = $resultado->fetch_object(); // Erro se query falhou!

// ✅ SOLUÇÃO 1: Verificar se query funcionou
$resultado = $banco->query($sql);
if ($resultado) {
    $user = $resultado->fetch_object();
} else {
    echo "Erro na query: " . $banco->error;
}

// ✅ SOLUÇÃO 2: Verificar se há resultados
$resultado = $banco->query($sql);
if ($resultado && $resultado->num_rows > 0) {
    $user = $resultado->fetch_object();
} else {
    echo "Nenhum resultado encontrado";
}

// ✅ SOLUÇÃO 3: Função segura
function buscarUsuario($id) {
    global $banco;
    $sql = "SELECT * FROM usuarios WHERE id='$id'";
    $resultado = $banco->query($sql);

    if ($resultado && $resultado->num_rows > 0) {
        return $resultado->fetch_object();
    }
    return null;
}
```

### 🔍 **Table doesn't exist**

**Mensagem completa:**

```
Table 'banco.usuarios' doesn't exist
```

**Causa:** Nome da tabela está errado ou tabela não foi criada

**Soluções:**

```php
// ❌ ERRO
$sql = "SELECT * FROM usuario"; // Tabela 'usuario' não existe

// ✅ SOLUÇÃO 1: Verificar nome correto da tabela
$sql = "SELECT * FROM usuarios"; // Nome correto

// ✅ SOLUÇÃO 2: Listar tabelas existentes
$resultado = $banco->query("SHOW TABLES");
while ($tabela = $resultado->fetch_array()) {
    echo $tabela[0] . "<br>";
}

// ✅ SOLUÇÃO 3: Criar tabela se não existir
$sql = "CREATE TABLE IF NOT EXISTS usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario VARCHAR(50) NOT NULL,
    senha VARCHAR(100) NOT NULL
)";
$banco->query($sql);

// ✅ SOLUÇÃO 4: Verificar se tabela existe
$resultado = $banco->query("SHOW TABLES LIKE 'usuarios'");
if ($resultado->num_rows == 0) {
    echo "Tabela 'usuarios' não existe!";
}
```

### 🔍 **Unknown column**

**Mensagem completa:**

```
Unknown column 'nome' in 'field list'
```

**Causa:** Nome da coluna está errado

**Soluções:**

```php
// ❌ ERRO
$sql = "SELECT nome FROM usuarios"; // Coluna 'nome' não existe

// ✅ SOLUÇÃO 1: Verificar nome correto da coluna
$sql = "SELECT usuario FROM usuarios"; // Nome correto

// ✅ SOLUÇÃO 2: Listar colunas da tabela
$resultado = $banco->query("DESCRIBE usuarios");
while ($coluna = $resultado->fetch_object()) {
    echo $coluna->Field . "<br>";
}

// ✅ SOLUÇÃO 3: Usar * para ver todas as colunas
$sql = "SELECT * FROM usuarios";
$resultado = $banco->query($sql);
if ($resultado->num_rows > 0) {
    $user = $resultado->fetch_object();
    print_r($user); // Ver todas as propriedades
}

// ✅ SOLUÇÃO 4: Verificar estrutura da tabela
$sql = "SHOW COLUMNS FROM usuarios";
$resultado = $banco->query($sql);
```

### 🔍 **You have an error in your SQL syntax**

**Mensagem completa:**

```
You have an error in your SQL syntax; check the manual
```

**Causa:** Erro de sintaxe no SQL

**Soluções:**

```php
// ❌ ERRO
$sql = "SELECT * FROM usuarios WHERE usuario='$usuario'"; // Aspas erradas
$sql = "INSERT INTO usuarios (usuario senha) VALUES ('admin', '123')"; // Falta vírgula

// ✅ SOLUÇÃO 1: Verificar aspas
$sql = "SELECT * FROM usuarios WHERE usuario='$usuario'"; // Aspas simples

// ✅ SOLUÇÃO 2: Verificar vírgulas
$sql = "INSERT INTO usuarios (usuario, senha) VALUES ('admin', '123')";

// ✅ SOLUÇÃO 3: Usar prepared statements
$stmt = $banco->prepare("SELECT * FROM usuarios WHERE usuario=?");
$stmt->bind_param("s", $usuario);
$stmt->execute();

// ✅ SOLUÇÃO 4: Debug do SQL
echo "SQL: " . $sql; // Ver como ficou o SQL
$resultado = $banco->query($sql);
if (!$resultado) {
    echo "Erro SQL: " . $banco->error;
}
```

---

## ⚙️ ERROS DE FUNÇÃO

### 🔍 **Call to undefined function**

**Mensagem completa:**

```
Fatal error: Call to undefined function minhaFuncao()
```

**Causa:** Função não foi definida ou arquivo não foi incluído

**Soluções:**

```php
// ❌ ERRO
echo saudar("João"); // Função não definida!

// ✅ SOLUÇÃO 1: Definir a função
function saudar($nome) {
    return "Olá, $nome!";
}
echo saudar("João");

// ✅ SOLUÇÃO 2: Incluir arquivo com a função
require_once "funcoes.php";
echo saudar("João");

// ✅ SOLUÇÃO 3: Verificar se função existe
if (function_exists('saudar')) {
    echo saudar("João");
} else {
    echo "Função não existe";
}

// ✅ SOLUÇÃO 4: Definir função antes de usar
function calcularIMC($peso, $altura) {
    return $peso / ($altura ** 2);
}

$imc = calcularIMC(70, 1.75);
```

### 🔍 **Fatal error: Cannot redeclare**

**Mensagem completa:**

```
Fatal error: Cannot redeclare function saudar()
```

**Causa:** Função foi definida mais de uma vez

**Soluções:**

```php
// ❌ ERRO
function saudar($nome) { return "Olá!"; }
function saudar($nome) { return "Oi!"; } // Erro!

// ✅ SOLUÇÃO 1: Verificar se já existe
if (!function_exists('saudar')) {
    function saudar($nome) {
        return "Olá, $nome!";
    }
}

// ✅ SOLUÇÃO 2: Usar nomes diferentes
function saudar($nome) { return "Olá, $nome!"; }
function cumprimentar($nome) { return "Oi, $nome!"; }

// ✅ SOLUÇÃO 3: Usar require_once
require_once "funcoes.php"; // Inclui apenas uma vez

// ✅ SOLUÇÃO 4: Usar classes
class Saudacao {
    static function saudar($nome) {
        return "Olá, $nome!";
    }
}
```

### 🔍 **Too few arguments**

**Mensagem completa:**

```
Warning: Too few arguments to function calcularIMC(), 1 passed in arquivo.php on line 10 and exactly 2 expected
```

**Causa:** Chamou função com menos parâmetros que o necessário

**Soluções:**

```php
// ❌ ERRO
function calcularIMC($peso, $altura) {
    return $peso / ($altura ** 2);
}
$imc = calcularIMC(70); // Falta a altura!

// ✅ SOLUÇÃO 1: Passar todos os parâmetros
$imc = calcularIMC(70, 1.75);

// ✅ SOLUÇÃO 2: Usar valores padrão
function calcularIMC($peso, $altura = 1.70) {
    return $peso / ($altura ** 2);
}

// ✅ SOLUÇÃO 3: Verificar parâmetros
function calcularIMC($peso, $altura = null) {
    if (is_null($altura)) {
        return "Altura é obrigatória";
    }
    return $peso / ($altura ** 2);
}

// ✅ SOLUÇÃO 4: Usar func_get_args()
function calcularIMC() {
    $args = func_get_args();
    if (count($args) < 2) {
        return "Peso e altura são obrigatórios";
    }
    return $args[0] / ($args[1] ** 2);
}
```

---

## 🔄 ERROS DE SINTAXE

### 🔍 **Parse error**

**Mensagem completa:**

```
Parse error: syntax error, unexpected ';' in arquivo.php on line 5
```

**Causa:** Erro de sintaxe no código

**Soluções:**

```php
// ❌ ERRO
if ($idade > 18); { // Ponto e vírgula no lugar errado!
    echo "Maior de idade";
}

// ✅ SOLUÇÃO
if ($idade > 18) { // Sem ponto e vírgula
    echo "Maior de idade";
}

// ❌ ERRO
echo "Olá" // Falta ponto e vírgula
echo "Mundo";

// ✅ SOLUÇÃO
echo "Olá"; // Com ponto e vírgula
echo "Mundo";

// ❌ ERRO
$array = [1, 2, 3,]; // Vírgula extra no final

// ✅ SOLUÇÃO
$array = [1, 2, 3]; // Sem vírgula extra
```

### 🔍 **syntax error, unexpected**

**Mensagem completa:**

```
Parse error: syntax error, unexpected 'echo' (T_ECHO)
```

**Causa:** Estrutura de código incorreta

**Soluções:**

```php
// ❌ ERRO
if ($idade > 18)
    echo "Maior";
    echo "de idade"; // Erro! Sem chaves

// ✅ SOLUÇÃO 1: Usar chaves
if ($idade > 18) {
    echo "Maior";
    echo "de idade";
}

// ✅ SOLUÇÃO 2: Uma linha só
if ($idade > 18) echo "Maior de idade";

// ❌ ERRO
for ($i = 0; $i < 10; $i++)
    echo $i;
    echo "<br>"; // Erro!

// ✅ SOLUÇÃO
for ($i = 0; $i < 10; $i++) {
    echo $i;
    echo "<br>";
}
```

### 🔍 **Missing argument**

**Mensagem completa:**

```
Warning: Missing argument 2 for calcularMedia()
```

**Causa:** Função chamada sem todos os argumentos obrigatórios

**Soluções:**

```php
// ❌ ERRO
function calcularMedia($nota1, $nota2, $nota3) {
    return ($nota1 + $nota2 + $nota3) / 3;
}
$media = calcularMedia(8, 7); // Falta $nota3!

// ✅ SOLUÇÃO 1: Passar todos os argumentos
$media = calcularMedia(8, 7, 9);

// ✅ SOLUÇÃO 2: Usar valores padrão
function calcularMedia($nota1, $nota2, $nota3 = 0) {
    return ($nota1 + $nota2 + $nota3) / 3;
}

// ✅ SOLUÇÃO 3: Verificar argumentos
function calcularMedia($nota1, $nota2 = null, $nota3 = null) {
    if (is_null($nota2) || is_null($nota3)) {
        return "Todas as notas são obrigatórias";
    }
    return ($nota1 + $nota2 + $nota3) / 3;
}
```

---

## 📊 ERROS DE ARRAY

### 🔍 **Array to string conversion**

**Mensagem completa:**

```
Notice: Array to string conversion in arquivo.php on line 5
```

**Causa:** Tentou imprimir array como string

**Soluções:**

```php
// ❌ ERRO
$array = ["João", "Maria", "Pedro"];
echo $array; // Erro! Não pode imprimir array direto

// ✅ SOLUÇÃO 1: Usar print_r() ou var_dump()
print_r($array);
var_dump($array);

// ✅ SOLUÇÃO 2: Acessar elemento específico
echo $array[0]; // João

// ✅ SOLUÇÃO 3: Usar implode() para juntar
echo implode(", ", $array); // João, Maria, Pedro

// ✅ SOLUÇÃO 4: Usar foreach
foreach ($array as $nome) {
    echo $nome . "<br>";
}

// ✅ SOLUÇÃO 5: Converter para JSON
echo json_encode($array);
```

### 🔍 **Invalid argument supplied**

**Mensagem completa:**

```
Warning: Invalid argument supplied for foreach()
```

**Causa:** Tentou usar foreach em algo que não é array

**Soluções:**

```php
// ❌ ERRO
$dados = null;
foreach ($dados as $item) { // Erro! $dados não é array
    echo $item;
}

// ✅ SOLUÇÃO 1: Verificar se é array
if (is_array($dados)) {
    foreach ($dados as $item) {
        echo $item;
    }
}

// ✅ SOLUÇÃO 2: Garantir que seja array
$dados = $dados ?? [];
foreach ($dados as $item) {
    echo $item;
}

// ✅ SOLUÇÃO 3: Verificar se não está vazio
if (!empty($dados) && is_array($dados)) {
    foreach ($dados as $item) {
        echo $item;
    }
}

// ✅ SOLUÇÃO 4: Converter para array se necessário
$dados = (array) $dados;
foreach ($dados as $item) {
    echo $item;
}
```

---

## 🌐 ERROS DE INCLUDE/REQUIRE

### 🔍 **No such file or directory**

**Mensagem completa:**

```
Warning: include(arquivo.php): failed to open stream: No such file or directory
```

**Causa:** Arquivo não existe no caminho especificado

**Soluções:**

```php
// ❌ ERRO
include "arquivo.php"; // Arquivo não existe!

// ✅ SOLUÇÃO 1: Verificar se arquivo existe
if (file_exists("arquivo.php")) {
    include "arquivo.php";
} else {
    echo "Arquivo não encontrado";
}

// ✅ SOLUÇÃO 2: Usar caminho absoluto
include __DIR__ . "/arquivo.php";

// ✅ SOLUÇÃO 3: Usar require_once para evitar duplicação
require_once "arquivo.php";

// ✅ SOLUÇÃO 4: Verificar caminho atual
echo "Diretório atual: " . getcwd();
echo "Arquivos: ";
print_r(scandir("."));
```

### 🔍 **Failed opening required**

**Mensagem completa:**

```
Fatal error: require(): Failed opening required 'config.php'
```

**Causa:** Arquivo obrigatório não foi encontrado

**Soluções:**

```php
// ❌ ERRO
require "config.php"; // Arquivo não existe!

// ✅ SOLUÇÃO 1: Usar include em vez de require
include "config.php"; // Não para execução se não encontrar

// ✅ SOLUÇÃO 2: Verificar antes de incluir
if (file_exists("config.php")) {
    require "config.php";
} else {
    die("Arquivo de configuração não encontrado!");
}

// ✅ SOLUÇÃO 3: Usar caminho relativo correto
require_once __DIR__ . "/config/config.php";

// ✅ SOLUÇÃO 4: Criar arquivo se não existir
if (!file_exists("config.php")) {
    file_put_contents("config.php", "<?php // Configurações ?>");
}
require "config.php";
```

---

## ⏱️ ERROS DE EXECUÇÃO

### 🔍 **Maximum execution time**

**Mensagem completa:**

```
Fatal error: Maximum execution time of 30 seconds exceeded
```

**Causa:** Script demorou muito para executar (loop infinito)

**Soluções:**

```php
// ❌ ERRO
while (true) { // Loop infinito!
    echo "Infinito";
}

// ✅ SOLUÇÃO 1: Adicionar condição de parada
$contador = 0;
while ($contador < 100) {
    echo "Contador: $contador";
    $contador++; // IMPORTANTE: incrementar!
}

// ✅ SOLUÇÃO 2: Usar for com limite
for ($i = 0; $i < 1000; $i++) {
    echo $i;
}

// ✅ SOLUÇÃO 3: Aumentar tempo limite (se necessário)
set_time_limit(60); // 60 segundos

// ✅ SOLUÇÃO 4: Verificar condições de loop
$tentativas = 0;
while ($conexao_falhou && $tentativas < 5) {
    // tentar conectar
    $tentativas++;
}
```

### 🔍 **Fatal error: Allowed memory size**

**Mensagem completa:**

```
Fatal error: Allowed memory size of 134217728 bytes exhausted
```

**Causa:** Script consumiu muita memória

**Soluções:**

```php
// ❌ ERRO
$array_gigante = [];
for ($i = 0; $i < 10000000; $i++) {
    $array_gigante[] = "Item $i"; // Consome muita memória!
}

// ✅ SOLUÇÃO 1: Processar em lotes menores
for ($i = 0; $i < 1000; $i++) { // Menos itens
    $array[] = "Item $i";
}

// ✅ SOLUÇÃO 2: Limpar variáveis não usadas
unset($array_gigante);

// ✅ SOLUÇÃO 3: Aumentar limite de memória (se necessário)
ini_set('memory_limit', '256M');

// ✅ SOLUÇÃO 4: Usar geradores para grandes datasets
function gerarNumeros() {
    for ($i = 0; $i < 1000000; $i++) {
        yield $i; // Não carrega tudo na memória
    }
}
```

---

## 🆘 CÓDIGOS DE EMERGÊNCIA PARA ERROS

### 🔧 **Conexão Universal (Resolve 90% dos erros de banco)**

```php
<?php
function conectarBanco($nome_banco = "") {
    $configs = [
        ["localhost:3307", "root", "", $nome_banco],
        ["127.0.0.1:3307", "root", "", $nome_banco],
        ["localhost:3306", "root", "", $nome_banco],
        ["127.0.0.1:3306", "root", "", $nome_banco],
        ["localhost", "root", "", $nome_banco]
    ];

    foreach ($configs as $config) {
        $teste = @new mysqli($config[0], $config[1], $config[2], $config[3]);
        if (!$teste->connect_error) {
            return $teste;
        }
    }

    die("❌ Erro: Não foi possível conectar ao banco!");
}

// Uso:
$banco = conectarBanco("php-segunda-manha");
?>
```

### 🔐 **Sessão Segura (Resolve erros de sessão)**

```php
<?php
// Inicia sessão de forma segura
if (session_status() == PHP_SESSION_NONE) {
    session_start();
}

// Função para verificar login
function verificarLogin() {
    $usuario = $_SESSION["usuario"] ?? null;
    if (is_null($usuario)) {
        header("Location: login.php");
        exit;
    }
    return $usuario;
}

// Função para fazer logout
function logout() {
    session_destroy();
    header("Location: login.php");
    exit;
}
?>
```

### 📝 **Validação Segura (Resolve erros de variáveis)**

```php
<?php
// Função para pegar dados do formulário com segurança
function pegarDado($nome, $metodo = "POST", $padrao = "") {
    if ($metodo === "POST") {
        return $_POST[$nome] ?? $padrao;
    } else {
        return $_GET[$nome] ?? $padrao;
    }
}

// Uso:
$usuario = pegarDado("usuario");
$senha = pegarDado("senha");
$idade = pegarDado("idade", "GET", 0);
?>
```

### 💾 **Query Segura (Resolve erros de banco)**

```php
<?php
function executarQuery($sql) {
    global $banco;

    $resultado = $banco->query($sql);

    if (!$resultado) {
        echo "❌ Erro SQL: " . $banco->error;
        return false;
    }

    return $resultado;
}

function buscarUsuario($usuario) {
    $sql = "SELECT * FROM usuarios WHERE usuario='$usuario'";
    $resultado = executarQuery($sql);

    if ($resultado && $resultado->num_rows > 0) {
        return $resultado->fetch_object();
    }

    return null;
}
?>
```

### 🎯 **Template Completo Sem Erros**

```php
<?php
// 1. Sessão segura
if (session_status() == PHP_SESSION_NONE) {
    session_start();
}

// 2. Conexão universal
function conectar($banco = "") {
    $configs = [
        ["localhost:3307", "root", "", $banco],
        ["127.0.0.1:3307", "root", "", $banco],
        ["localhost:3306", "root", "", $banco]
    ];

    foreach ($configs as $config) {
        $teste = @new mysqli($config[0], $config[1], $config[2], $config[3]);
        if (!$teste->connect_error) return $teste;
    }
    die("Erro: Não foi possível conectar!");
}

$banco = conectar("php-segunda-manha");

// 3. Verificar login (se necessário)
$usuario = $_SESSION["usuario"] ?? null;
if (is_null($usuario)) {
    // Processar login
    if ($_SERVER["REQUEST_METHOD"] === "POST") {
        $user = $_POST["usuario"] ?? "";
        $pass = $_POST["senha"] ?? "";

        if ($user === "admin" && $pass === "123") {
            $_SESSION["usuario"] = $user;
            header("Location: " . $_SERVER['PHP_SELF']);
            exit;
        }
    }

    // Mostrar formulário
    echo '<form method="post">
        Usuário: <input name="usuario">
        Senha: <input name="senha" type="password">
        <input type="submit" value="Login">
    </form>';
    exit;
}

// 4. Área logada
echo "Bem-vindo, $usuario!";
echo " <a href='?logout=1'>Sair</a>";

// 5. Logout
if (isset($_GET["logout"])) {
    session_destroy();
    header("Location: " . $_SERVER['PHP_SELF']);
    exit;
}

// Seu código aqui...
?>
```

---

## 🎯 DICAS FINAIS PARA EVITAR ERROS

### ✅ **Checklist Antes de Executar**

1. **XAMPP ligado?** ✅
2. **session_start() no início?** ✅
3. **Verificou se variáveis existem com ??** ✅
4. **Usou exit após header()?** ✅
5. **Verificou conexão com banco?** ✅
6. **Usou global $banco em funções?** ✅

### 🔍 **Para Debug Rápido**

```php
// Ver conteúdo de variáveis
var_dump($_GET);
var_dump($_POST);
var_dump($_SESSION);

// Mostrar erros
error_reporting(E_ALL);
ini_set('display_errors', 1);

// Testar conexão
$teste = @new mysqli("localhost:3307", "root", "");
echo $teste->connect_error ? "❌ Erro" : "✅ Conectado";
```

### 🚨 **Erros Mais Comuns na Prova**

1. **Esquecer session_start()**
2. **Não verificar se variáveis existem**
3. **Porta do MySQL errada**
4. **Não usar exit após header()**
5. **Esquecer global $banco em funções**
6. **Nome de tabela/coluna errado**
7. **Não verificar se query funcionou**

**🍀 COM ESTE GUIA VOCÊ RESOLVE QUALQUER ERRO! BOA SORTE! 🚀**
