# 🚀 REVISÃO RÁPIDA - PROVA PHP

## 📋 ÍNDICE RÁPIDO

1. [🔧 XAMPP & Banco](#xampp--banco-passo-a-passo)
2. [🏫 Problemas nos PCs da Faculdade](#problemas-nos-pcs-da-faculdade)
3. [📝 Sintaxe Básica](#sintaxe-básica)
4. [🔄 Estruturas](#estruturas)
5. [📊 Arrays](#arrays)
6. [⚙️ Funções](#funções)
7. [📋 Formulários](#formulários)
8. [🔤 Strings](#strings-e-funções-de-texto)
9. [🔐 Sessões](#sessões)
10. [💾 Banco de Dados](#banco-de-dados)
11. [🐛 Debug](#debug-e-ferramentas-úteis)
12. [🚨 Erros Comuns](#erros-comuns-ctrlf-aqui)
13. [✅ Checklist](#checklist)

---

## 🔧 XAMPP & Banco (PASSO A PASSO)

### 🚀 **PASSO 1: Ligar o XAMPP**

1. Abra o **XAMPP Control Panel**
2. Clique em **"Start"** no **Apache** ✅
3. Clique em **"Start"** no **MySQL** ✅
4. Se der erro, mude a porta do MySQL para **3307**

### 🔍 **PASSO 2: Descobrir a porta do MySQL**

```php
// Cole isso em um arquivo .php para descobrir a porta:
<?php
// Testa porta 3306
$teste1 = new mysqli("localhost:3306", "root", "");
if (!$teste1->connect_error) {
    echo "✅ Sua porta é: 3306";
} else {
    // Testa porta 3307
    $teste2 = new mysqli("localhost:3307", "root", "");
    if (!$teste2->connect_error) {
        echo "✅ Sua porta é: 3307";
    } else {
        echo "❌ MySQL não está funcionando";
    }
}
?>
```

### 🎯 **PASSO 3: Conexão Básica (COPIE E COLE)**

```php
<?php
// MODELO PADRÃO - sempre use este:
$banco = new mysqli("localhost:3307", "root", "", "nome_do_banco");

// SEMPRE verificar se conectou:
if ($banco->connect_error) {
    die("❌ Erro na conexão: " . $banco->connect_error);
}

echo "✅ Conectado com sucesso!";
?>
```

### 📝 **PASSO 4: Entendendo cada parte**

```php
$banco = new mysqli("HOST", "USUÁRIO", "SENHA", "BANCO");
//                    ↓        ↓        ↓        ↓
//               localhost   root      ""    meu_banco
//               :3307    (padrão)  (vazio)  (nome que você criou)
```

### 🏗️ **PASSO 5: Criar banco de dados**

```sql
-- No phpMyAdmin ou MySQL, execute:
CREATE DATABASE meu_banco;
USE meu_banco;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario VARCHAR(50) NOT NULL,
    senha VARCHAR(100) NOT NULL
);

-- Inserir dados de teste:
INSERT INTO usuarios (usuario, senha) VALUES ('admin', '123');
```

### ⚡ **CÓDIGOS PRONTOS PARA COPIAR**

#### 🔗 **Conexão Simples (sem banco específico)**

```php
<?php
$banco = new mysqli("localhost:3307", "root", "");
if ($banco->connect_error) {
    die("Erro: " . $banco->connect_error);
}
echo "Conectado!";
?>
```

#### 🔗 **Conexão com Banco Específico**

```php
<?php
$banco = new mysqli("localhost:3307", "root", "", "meu_banco");
if ($banco->connect_error) {
    die("Erro: " . $banco->connect_error);
}
echo "Conectado ao banco 'meu_banco'!";
?>
```

#### 🔗 **Conexão Completa com Teste**

```php
<?php
// Tenta conectar
$banco = new mysqli("localhost:3307", "root", "", "meu_banco");

// Verifica se deu erro
if ($banco->connect_error) {
    echo "❌ ERRO: " . $banco->connect_error;
    echo "<br>🔧 Verifique se:";
    echo "<br>- XAMPP está ligado";
    echo "<br>- MySQL está rodando";
    echo "<br>- A porta está correta (3306 ou 3307)";
    echo "<br>- O banco 'meu_banco' existe";
    die();
}

echo "✅ Conectado com sucesso!";
echo "<br>📊 Banco: " . $banco->server_info;
?>
```

### 🚨 **ERROS MAIS COMUNS E SOLUÇÕES**

#### ❌ **"Connection refused"**

```php
// PROBLEMA: Porta errada ou MySQL parado
// SOLUÇÃO: Verificar porta e ligar MySQL no XAMPP

// Teste as duas portas:
$banco = new mysqli("localhost:3306", "root", "", ""); // Porta 3306
// OU
$banco = new mysqli("localhost:3307", "root", "", ""); // Porta 3307
```

#### ❌ **"Unknown database"**

```php
// PROBLEMA: Banco não existe
// SOLUÇÃO: Criar o banco primeiro

// 1. Conecte sem especificar banco:
$banco = new mysqli("localhost:3307", "root", "");

// 2. Crie o banco:
$banco->query("CREATE DATABASE meu_banco");

// 3. Agora conecte com o banco:
$banco = new mysqli("localhost:3307", "root", "", "meu_banco");
```

#### ❌ **"Access denied"**

```php
// PROBLEMA: Usuário ou senha errados
// SOLUÇÃO: No XAMPP, sempre use:

$banco = new mysqli("localhost:3307", "root", "", "banco");
//                                    ↑      ↑
//                                 usuário senha
//                                 (root)  (vazio)
```

### 🏫 **PROBLEMAS NOS PCs DA FACULDADE**

#### 🚨 **Problema: "Localhost não funciona" ou "Connection refused"**

##### ⚡ **SOLUÇÃO RÁPIDA - Descobrir o IP correto:**

```php
// Cole isso para descobrir qual IP usar:
<?php
echo "🔍 Testando conexões...<br>";

// Testa localhost
$teste1 = @new mysqli("localhost:3307", "root", "");
if (!$teste1->connect_error) {
    echo "✅ Use: localhost:3307<br>";
} else {
    // Testa 127.0.0.1
    $teste2 = @new mysqli("127.0.0.1:3307", "root", "");
    if (!$teste2->connect_error) {
        echo "✅ Use: 127.0.0.1:3307<br>";
    } else {
        // Testa IP da máquina
        $ip = $_SERVER['SERVER_ADDR'] ?? 'localhost';
        $teste3 = @new mysqli("$ip:3307", "root", "");
        if (!$teste3->connect_error) {
            echo "✅ Use: $ip:3307<br>";
        } else {
            echo "❌ Nenhuma conexão funcionou<br>";
            echo "🔧 Siga os passos abaixo...<br>";
        }
    }
}
?>
```

#### 🔧 **CONFIGURAÇÕES PARA CORRIGIR**

##### **1. Arquivo: `C:\xampp\mysql\bin\my.ini`**

```ini
# Procure por estas linhas e altere:

[mysqld]
port = 3307
bind-address = 0.0.0.0
# OU se não funcionar:
bind-address = 127.0.0.1

# Se não existir, adicione:
skip-networking = 0
```

##### **2. Arquivo: `C:\xampp\apache\conf\httpd.conf`**

```apache
# Procure por:
Listen 80

# Se der conflito, mude para:
Listen 8080
# Ou qualquer porta livre (8081, 8082, etc.)
```

##### **3. Arquivo: `C:\xampp\phpMyAdmin\config.inc.php`**

```php
// Procure por:
$cfg['Servers'][$i]['host'] = 'localhost';

// Mude para:
$cfg['Servers'][$i]['host'] = '127.0.0.1';
// OU para o IP que funcionou no teste acima
```

#### 🆘 **SOLUÇÕES DE EMERGÊNCIA**

##### **Solução 1: Forçar IP específico**

```php
// Se localhost não funcionar, teste estes IPs:
$ips = ["127.0.0.1", "localhost", "::1"];
$banco = null;

foreach ($ips as $ip) {
    $teste = @new mysqli("$ip:3307", "root", "", "banco");
    if (!$teste->connect_error) {
        $banco = $teste;
        echo "✅ Conectado com: $ip";
        break;
    }
}

if (!$banco) {
    die("❌ Nenhum IP funcionou!");
}
```

##### **Solução 2: Múltiplas portas**

```php
// Testa várias portas automaticamente:
$portas = [3306, 3307, 3308, 3309];
$banco = null;

foreach ($portas as $porta) {
    $teste = @new mysqli("localhost:$porta", "root", "", "banco");
    if (!$teste->connect_error) {
        $banco = $teste;
        echo "✅ Conectado na porta: $porta";
        break;
    }
}

if (!$banco) {
    die("❌ Nenhuma porta funcionou!");
}
```

##### **Solução 3: Conexão universal (COPIE ESTA!)**

```php
// Esta função testa tudo automaticamente:
function conectarBanco($nome_banco = "") {
    $hosts = ["localhost", "127.0.0.1", "::1"];
    $portas = [3306, 3307, 3308];

    foreach ($hosts as $host) {
        foreach ($portas as $porta) {
            $teste = @new mysqli("$host:$porta", "root", "", $nome_banco);
            if (!$teste->connect_error) {
                echo "✅ Conectado: $host:$porta<br>";
                return $teste;
            }
        }
    }

    die("❌ Não foi possível conectar!");
}

// Use assim:
$banco = conectarBanco("meu_banco");
```

#### 🔥 **COMANDOS PARA REINICIAR XAMPP**

##### **No Windows (Prompt como Administrador):**

```cmd
# Parar serviços:
net stop apache2.4
net stop mysql

# Iniciar serviços:
net start apache2.4
net start mysql

# OU reiniciar XAMPP:
taskkill /f /im xampp-control.exe
# Depois abrir XAMPP novamente
```

#### 🎯 **CÓDIGO FINAL PARA A PROVA**

```php
// COLE ESTE CÓDIGO - FUNCIONA EM QUALQUER PC:
<?php
session_start();

// Função que sempre conecta:
function conectar($banco = "") {
    $configs = [
        ["localhost:3307", "root", "", $banco],
        ["127.0.0.1:3307", "root", "", $banco],
        ["localhost:3306", "root", "", $banco],
        ["127.0.0.1:3306", "root", "", $banco]
    ];

    foreach ($configs as $config) {
        $teste = @new mysqli($config[0], $config[1], $config[2], $config[3]);
        if (!$teste->connect_error) {
            return $teste;
        }
    }

    die("Erro: Não foi possível conectar ao banco!");
}

// Use assim:
$banco = conectar("nome_do_banco");
echo "✅ Conectado!";
?>
```

### 🎯 **DICA DE OURO PARA A PROVA**

```php
// SEMPRE cole este código no início dos seus arquivos:
<?php
session_start(); // Se usar sessões

// Conexão padrão que sempre funciona:
$banco = new mysqli("localhost:3307", "root", "", "nome_do_banco");

// Verificação obrigatória:
if ($banco->connect_error) {
    die("Erro na conexão: " . $banco->connect_error);
}

// Agora pode usar $banco em todo o arquivo!
?>
```

---

## 📝 Sintaxe Básica

### Variáveis e Tipos

```php
<?php
$nome = "João";           // String
$idade = 25;              // Integer
$salario = 2500.50;       // Float
$ativo = true;            // Boolean

// Mostrar na tela
echo "Olá $nome!";                    // Com interpolação
echo "Salário: " . $salario;          // Com concatenação
echo "Idade: {$idade} anos";          // Com chaves
?>
```

### Verificar se Existe

```php
// SEMPRE use isso para GET/POST
$nome = $_GET["nome"] ?? "Padrão";
$idade = $_POST["idade"] ?? 0;

// Ou assim
if (isset($_GET["nome"])) {
    $nome = $_GET["nome"];
}

// Operador ternário (alternativa ao ??)
$n1 = isset($_GET["n1"]) ? $_GET["n1"] : 0;
$n2 = isset($_GET["n2"]) ? $_GET["n2"] : 1;
```

### 🔢 **Formatação de Números (number_format)**

```php
<?php
$preco = 1234.567;

// Sintaxe: number_format(número, decimais, separador_decimal, separador_milhares)
echo number_format($preco, 2, ",", "."); // 1.234,57 (formato brasileiro)
echo number_format($preco, 2); // 1,234.57 (formato americano)

// Exemplo prático:
$salario = 2500.7359;
echo "R$ " . number_format($salario, 2, ",", "."); // R$ 2.500,74
?>
```

### 📊 **Operadores Matemáticos**

```php
<?php
$a = 10; $b = 3;

// Básicos
echo $a + $b;  // 13 (soma)
echo $a - $b;  // 7 (subtração)
echo $a * $b;  // 30 (multiplicação)
echo $a / $b;  // 3.333... (divisão)
echo $a % $b;  // 1 (resto da divisão)
echo $a ** $b; // 1000 (potência)

// Incremento
$num = 5;
echo $num++;   // 5 (mostra depois incrementa)
echo ++$num;   // 7 (incrementa depois mostra)

// Atribuição combinada
$x = 10;
$x += 5;  // $x = $x + 5 = 15
$x *= 2;  // $x = $x * 2 = 30
?>
```

### 🔤 **Interpolação vs Concatenação**

```php
<?php
$nome = "João";

// Interpolação (aspas duplas)
echo "Olá $nome!";           // Olá João!
echo "Olá {$nome}!";         // Olá João! (mais seguro)

// Concatenação (com ponto)
echo "Olá " . $nome . "!";   // Olá João!

// Aspas simples não interpola
echo 'Olá $nome!'; // Mostra: Olá $nome! (literal)
?>
```

---

## 🔄 Estruturas

### IF/ELSE

```php
<?php
$idade = 18;

if ($idade >= 18) {
    echo "Maior de idade";
} else {
    echo "Menor de idade";
}

// Múltiplas condições
if ($idade < 18) {
    echo "Menor";
} elseif ($idade < 60) {
    echo "Adulto";
} else {
    echo "Idoso";
}
?>
```

### FOR e WHILE

```php
<?php
// FOR - quando sabe quantas vezes
for ($i = 0; $i < 10; $i++) {
    echo "Número: $i<br>";
}

// WHILE - enquanto condição for verdadeira
$contador = 0;
while ($contador < 5) {
    echo "Contador: $contador<br>";
    $contador++;
}

// DO-WHILE - executa pelo menos uma vez
$valor = 0;
do {
    echo "Do While: $valor<br>";
    $valor += 1.2;
} while ($valor <= 5);
?>
```

### 🔄 **Estruturas Avançadas**

```php
<?php
// IF alternativo (útil em HTML)
$idade = 18;
?>
<?php if ($idade >= 18): ?>
    <p>Maior de idade</p>
<?php else: ?>
    <p>Menor de idade</p>
<?php endif; ?>

<?php
// SWITCH
$dia = "segunda";
switch ($dia) {
    case "segunda":
    case "terça":
        echo "Dia útil";
        break;
    case "sábado":
        echo "Final de semana";
        break;
    default:
        echo "Dia inválido";
}

// Operadores importantes
$a = 5; $b = "5";
var_dump($a == $b);  // true (igual)
var_dump($a === $b); // false (idêntico)
var_dump($a && $b);  // true (E lógico)
var_dump($a || $b);  // true (OU lógico)
?>
```

---

## 📊 Arrays

### Array Simples

```php
<?php
$frutas = ["Maçã", "Banana", "Laranja"];

// Acessar
echo $frutas[0]; // Maçã

// Percorrer
foreach ($frutas as $fruta) {
    echo $fruta . "<br>";
}
?>
```

### Array Associativo

```php
<?php
$pessoa = [
    "nome" => "João",
    "idade" => 25,
    "cidade" => "Curitiba"
];

// Acessar
echo $pessoa["nome"]; // João

// Percorrer
foreach ($pessoa as $chave => $valor) {
    echo "$chave: $valor<br>";
}
?>
```

### Array de Arrays

```php
<?php
$alunos = [
    ["nome" => "Ana", "nota" => 8.5],
    ["nome" => "Bruno", "nota" => 7.0],
    ["nome" => "Carlos", "nota" => 9.0]
];

foreach ($alunos as $aluno) {
    echo $aluno["nome"] . ": " . $aluno["nota"] . "<br>";
}
?>
```

### 📊 **Funções de Array**

```php
<?php
$frutas = ["Maçã", "Banana", "Laranja"];
$pessoa = ["nome" => "João", "idade" => 25];

// Básicas
echo count($frutas); // 3
$frutas[] = "Uva";   // Adiciona no final

// Verificar
if (in_array("Banana", $frutas)) {
    echo "Banana existe";
}

// Juntar e separar
$texto = implode(", ", $frutas);        // Array para string
$palavras = explode(" ", "João Silva"); // String para array

print_r($frutas);
?>
```

### 🔄 **Foreach com Chaves**

```php
<?php
$produtos = ["notebook" => 2500.00, "mouse" => 45.99];

// Foreach com chave e valor
foreach ($produtos as $produto => $preco) {
    echo "$produto: R$ " . number_format($preco, 2, ",", ".") . "<br>";
}

// Com arrays multidimensionais
$turma = [
    ["nome" => "João", "idade" => 18],
    ["nome" => "Maria", "idade" => 20]
];

foreach ($turma as $aluno) {
    echo "<p>{$aluno['nome']}: {$aluno['idade']} anos</p>";
}
?>
```

---

## ⚙️ Funções

### Função Simples

```php
<?php
function saudar($nome) {
    return "Olá, $nome!";
}

echo saudar("Maria"); // Olá, Maria!
?>
```

### Função com Múltiplos Parâmetros

```php
<?php
function calcularMedia($nota1, $nota2, $nota3) {
    return ($nota1 + $nota2 + $nota3) / 3;
}

$media = calcularMedia(8, 7, 9);
echo "Média: $media";
?>
```

### Função com Valor Padrão

```php
<?php
function cumprimentar($nome = "Visitante") {
    return "Bem-vindo, $nome!";
}

echo cumprimentar();        // Bem-vindo, Visitante!
echo cumprimentar("João");  // Bem-vindo, João!
?>
```

### ⚙️ **Funções Avançadas**

```php
<?php
// Múltiplos parâmetros
function somarNumeros(...$numeros) {
    $soma = 0;
    foreach ($numeros as $num) {
        $soma += $num;
    }
    return $soma;
}
echo somarNumeros(1, 2, 3); // 6

// Função com referência (&$variavel)
function incrementar(&$numero) {
    $numero += 5;
}
$valor = 10;
incrementar($valor);
echo $valor; // 15

// Validação
function varValida($variavel) {
    return (!is_null($variavel) && !empty($variavel));
}
?>
```

### 🎯 **Escopo de Variáveis**

```php
<?php
$global = "Variável global";

function testeEscopo() {
    global $global; // IMPORTANTE: usar global
    echo $global;   // Agora funciona
}

// Variável estática (mantém valor entre chamadas)
function contador() {
    static $count = 0;
    $count++;
    echo "Chamada: $count<br>";
}
contador(); // Chamada: 1
contador(); // Chamada: 2
?>
```

---

## 📋 Formulários

### HTML Básico

```html
<form method="get">
  Nome: <input type="text" name="nome" /> Idade:
  <input type="number" name="idade" />
  <input type="submit" value="Enviar" />
</form>

<form method="post">
  Usuário: <input type="text" name="usuario" /> Senha:
  <input type="password" name="senha" />
  <input type="submit" value="Login" />
</form>
```

### Processar Formulário

```php
<?php
// GET
$nome = $_GET["nome"] ?? "";
$idade = $_GET["idade"] ?? 0;

// POST
$usuario = $_POST["usuario"] ?? "";
$senha = $_POST["senha"] ?? "";

// Verificar se foi enviado
if ($_SERVER["REQUEST_METHOD"] === "POST") {
    // Processar dados
    if (!empty($usuario) && !empty($senha)) {
        echo "Dados recebidos!";
    } else {
        echo "Preencha todos os campos!";
    }
}
?>
```

### Validação Simples

```php
<?php
$peso = $_GET["peso"] ?? 0;
$altura = $_GET["altura"] ?? 0;

if ($peso > 0 && $altura > 0) {
    $imc = $peso / ($altura ** 2);
    echo "IMC: " . number_format($imc, 2);
} else {
    echo "Valores inválidos!";
}
?>
```

### 📋 **Formulário Completo**

```php
<form method="get">
    Peso: <input type="number" step="0.1" name="peso" required><br>
    Altura: <input type="number" step="0.01" name="altura" required><br>
    <input type="submit" value="Calcular IMC">
</form>

<?php
function calcularIMC($peso, $altura) {
    return $peso / ($altura ** 2);
}

$peso = $_GET["peso"] ?? null;
$altura = $_GET["altura"] ?? null;

if (!is_null($peso) && !is_null($altura)) {
    if (!empty($peso) && !empty($altura)) {
        $imc = calcularIMC($peso, $altura);
        echo "<p>IMC: " . number_format($imc, 2, ",", ".") . "</p>";
    } else {
        echo "<p>Preencha todos os campos!</p>";
    }
}
?>
```

---

## 🔤 Strings e Funções de Texto

### 📝 **Aspas e Strings**

```php
<?php
$nome = "João";

// Aspas duplas interpola, simples não
echo "Olá $nome!";     // Olá João!
echo 'Olá $nome!';     // Olá $nome! (literal)

// Escape quando necessário
echo "Caminho: C:\\pasta\\arquivo";
echo 'Ele disse: "Olá"';
?>
```

### 🔧 **Funções de String**

```php
<?php
$texto = "  PHP é uma Linguagem  ";

// Básicas
echo strlen($texto);        // Tamanho
echo trim($texto);          // Remove espaços
echo strtoupper($texto);    // MAIÚSCULO
echo strtolower($texto);    // minúsculo
echo ucfirst($texto);       // Primeira maiúscula

// Buscar e substituir
echo strpos($texto, "PHP");              // Posição
echo str_replace("PHP", "Python", $texto); // Substituir

// Dividir e juntar
$palavras = explode(" ", "João Silva");  // String para array
$nome = implode(" ", $palavras);         // Array para string
?>
```

---

## 🔐 Sessões

### Iniciar Sessão

```php
<?php
session_start(); // SEMPRE no início do arquivo

// Definir variável
$_SESSION["usuario"] = "admin";
$_SESSION["id"] = 123;

// Ler variável
$usuario = $_SESSION["usuario"] ?? null;
?>
```

### Sistema de Login

```php
<?php
session_start();

// Verificar se já está logado
if (isset($_SESSION["usuario"])) {
    echo "Bem-vindo, " . $_SESSION["usuario"];
} else {
    // Processar login
    $usuario = $_POST["usuario"] ?? "";
    $senha = $_POST["senha"] ?? "";

    if ($usuario === "admin" && $senha === "123") {
        $_SESSION["usuario"] = $usuario;
        header("Location: dashboard.php");
        exit;
    }
}
?>
```

### Logout

```php
<?php
session_start();
session_destroy();
header("Location: login.php");
exit;
?>
```

### Proteger Página

```php
<?php
session_start();

if (!isset($_SESSION["usuario"])) {
    header("Location: login.php");
    exit;
}

echo "Área restrita para: " . $_SESSION["usuario"];
?>
```

---

## 💾 Banco de Dados

### Conectar

```php
<?php
$banco = new mysqli("localhost:3307", "root", "", "nome_banco");

if ($banco->connect_error) {
    die("Erro: " . $banco->connect_error);
}
?>
```

### SELECT (Buscar)

```php
<?php
function buscarUsuario($usuario) {
    global $banco;

    $sql = "SELECT * FROM usuarios WHERE usuario='$usuario'";
    $resultado = $banco->query($sql);

    if ($resultado->num_rows > 0) {
        return $resultado->fetch_object();
    }
    return null;
}

$user = buscarUsuario("admin");
if ($user) {
    echo "Nome: " . $user->nome;
}
?>
```

### INSERT (Adicionar)

```php
<?php
function adicionarTarefa($texto) {
    global $banco;

    $sql = "INSERT INTO tarefas (texto) VALUES ('$texto')";
    return $banco->query($sql);
}

if (adicionarTarefa("Estudar PHP")) {
    echo "Tarefa adicionada!";
}
?>
```

### UPDATE (Atualizar)

```php
<?php
function atualizarTarefa($id, $novo_texto) {
    global $banco;

    $sql = "UPDATE tarefas SET texto='$novo_texto' WHERE id='$id'";
    return $banco->query($sql);
}
?>
```

### DELETE (Excluir)

```php
<?php
function excluirTarefa($id) {
    global $banco;

    $sql = "DELETE FROM tarefas WHERE id='$id'";
    return $banco->query($sql);
}
?>
```

### Login com Banco

```php
<?php
function fazerLogin($usuario, $senha) {
    global $banco;

    $sql = "SELECT * FROM usuarios WHERE usuario='$usuario'";
    $resultado = $banco->query($sql);

    if ($resultado->num_rows > 0) {
        $user = $resultado->fetch_object();
        if ($senha == $user->senha) {
            $_SESSION["usuario"] = $usuario;
            $_SESSION["id"] = $user->id;
            return true;
        }
    }
    return false;
}
?>
```

---

## 🚨 Erros Comuns (CTRL+F aqui!)

### 🔍 **"session_start()"** ou **"Cannot send session"**

**Mensagem:** `Warning: session_start(): Cannot send session cookie`

```php
// ❌ ERRO
$_SESSION["usuario"] = "admin";

// ✅ CORRETO
session_start(); // SEMPRE no início!
$_SESSION["usuario"] = "admin";
```

### 🔍 **"headers already sent"** ou **"Cannot modify header"**

**Mensagem:** `Warning: Cannot modify header information - headers already sent`

```php
// ❌ ERRO
echo "Algo";
header("Location: pagina.php");

// ✅ CORRETO
header("Location: pagina.php");
exit; // SEMPRE usar exit!
```

### 🔍 **"Undefined index"** ou **"Undefined variable"**

**Mensagem:** `Notice: Undefined index: nome` ou `Notice: Undefined variable: nome`

```php
// ❌ ERRO
echo $_GET["nome"];
$resultado = $variavel_inexistente;

// ✅ CORRETO
echo $_GET["nome"] ?? "Padrão";
$resultado = $variavel ?? "valor_padrao";
```

### 🔍 **"Call to a member function"** ou **"fetch_object()"**

**Mensagem:** `Fatal error: Call to a member function fetch_object() on boolean`

```php
// ❌ ERRO
$resultado = $banco->query($sql);
$user = $resultado->fetch_object(); // Erro se query falhou!

// ✅ CORRETO
$resultado = $banco->query($sql);
if ($resultado && $resultado->num_rows > 0) {
    $user = $resultado->fetch_object();
}
```

### 🔍 **"Undefined variable: banco"** em função

**Mensagem:** `Notice: Undefined variable: banco`

```php
// ❌ ERRO
function buscar() {
    $sql = "SELECT * FROM tabela";
    $banco->query($sql); // Erro!
}

// ✅ CORRETO
function buscar() {
    global $banco; // Adicionar esta linha!
    $sql = "SELECT * FROM tabela";
    $banco->query($sql);
}
```

### 🔍 **"Connection refused"** ou **"Can't connect"**

**Mensagem:** `mysqli::__construct(): (HY000/2002): Connection refused`

```php
// ❌ ERRO (porta errada)
$banco = new mysqli("localhost", "root", "", "banco");

// ✅ CORRETO (verificar porta)
$banco = new mysqli("localhost:3307", "root", "", "banco");
// OU
$banco = new mysqli("localhost:3306", "root", "", "banco");
```

### 🔍 **"Parse error"** ou **"syntax error"**

**Mensagem:** `Parse error: syntax error, unexpected ';'`

```php
// ❌ ERRO (ponto e vírgula no lugar errado)
if ($idade > 18); {
    echo "Maior";
}

// ✅ CORRETO
if ($idade > 18) {
    echo "Maior";
}
```

### 🔍 **"Array to string conversion"**

**Mensagem:** `Notice: Array to string conversion`

```php
// ❌ ERRO
$array = ["a", "b", "c"];
echo $array; // Não pode imprimir array direto!

// ✅ CORRETO
print_r($array); // Para ver estrutura
// OU
echo $array[0]; // Para ver um elemento
// OU
echo implode(", ", $array); // Para juntar elementos
```

### 🔍 **"Maximum execution time"** ou **"Fatal error: Maximum"**

**Mensagem:** `Fatal error: Maximum execution time of 30 seconds exceeded`

```php
// ❌ ERRO (loop infinito)
while (true) {
    echo "Infinito";
}

// ✅ CORRETO (sempre ter condição de parada)
$contador = 0;
while ($contador < 10) {
    echo "Contador: $contador";
    $contador++; // IMPORTANTE: incrementar!
}
```

### 🔍 **"No database selected"**

**Mensagem:** `No database selected`

```php
// ❌ ERRO (esqueceu de selecionar banco)
$banco = new mysqli("localhost:3307", "root", "");

// ✅ CORRETO (especificar nome do banco)
$banco = new mysqli("localhost:3307", "root", "", "nome_do_banco");
```

### 🔍 **"Table doesn't exist"**

**Mensagem:** `Table 'banco.tabela' doesn't exist`

```php
// ❌ ERRO (nome da tabela errado)
$sql = "SELECT * FROM usuario"; // Tabela não existe

// ✅ CORRETO (verificar nome correto)
$sql = "SELECT * FROM usuarios"; // Nome correto da tabela
```

### 🔍 **"Column not found"** ou **"Unknown column"**

**Mensagem:** `Unknown column 'nome' in 'field list'`

```php
// ❌ ERRO (coluna não existe)
$sql = "SELECT nome FROM usuarios"; // Coluna 'nome' não existe

// ✅ CORRETO (verificar nome da coluna)
$sql = "SELECT usuario FROM usuarios"; // Nome correto da coluna
```

## 🆘 **SOLUÇÕES RÁPIDAS**

### ⚡ **Erro de conexão?**

```php
// Cole isso para testar:
$banco = new mysqli("localhost:3307", "root", "", "");
if ($banco->connect_error) {
    echo "❌ Erro: " . $banco->connect_error;
} else {
    echo "✅ Conectado!";
}
```

### ⚡ **Variável não existe?**

```php
// Sempre use ?? para verificar:
$nome = $_GET["nome"] ?? "padrão";
$idade = $_POST["idade"] ?? 0;
$usuario = $_SESSION["usuario"] ?? null;
```

### ⚡ **Sessão não funciona?**

```php
// SEMPRE no início do arquivo:
<?php
session_start();
// resto do código...
```

### ⚡ **Redirecionamento não funciona?**

```php
// SEMPRE usar exit após header:
header("Location: pagina.php");
exit; // Esta linha é obrigatória!
```

### ⚡ **Função não acessa banco?**

```php
// SEMPRE usar global:
function minhaFuncao() {
    global $banco; // Esta linha é obrigatória!
    // resto da função...
}
```

---

## 🐛 Debug e Ferramentas Úteis

### 🔍 **Funções de Debug**

```php
<?php
// Básicas para debug
var_dump($variavel);    // Mostra tipo e valor
print_r($array);        // Mostra estrutura
echo gettype($valor);   // Mostra tipo

// Verificar se existe
echo isset($variavel);  // Se existe
echo empty($variavel);  // Se está vazio
echo is_array($dados);  // Se é array
?>
```

### 📋 **Debug Rápido**

```php
<?php
// Cole para debugar formulários
echo "<h3>🔍 DEBUG</h3>";
echo "<h4>GET:</h4>"; print_r($_GET);
echo "<h4>POST:</h4>"; print_r($_POST);
echo "<h4>SESSION:</h4>"; print_r($_SESSION);
?>
```

---

## ✅ Checklist

### 🚀 **Antes de Começar a Prova**

- [ ] **XAMPP ligado** (Apache ✅ + MySQL ✅)
- [ ] **Testar porta MySQL** (3306 ou 3307)
- [ ] **Criar banco de dados** se necessário
- [ ] **Verificar phpMyAdmin** funcionando
- [ ] **Testar conexão** com código de teste
- [ ] **Preparar estrutura de pastas** organizadas

### 📝 **Em Todo Arquivo PHP**

- [ ] **`<?php`** no início (sempre!)
- [ ] **`session_start()`** se usar sessões (primeira linha após <?php)
- [ ] **Verificar conexão** com banco (se usar)
- [ ] **`exit`** após `header()` (obrigatório!)
- [ ] **Encoding UTF-8** se usar acentos
- [ ] **Comentários** explicando o código

### 🏗️ **Estrutura Básica Completa**

```php
<?php
// 1. Iniciar sessão (se necessário)
session_start();

// 2. Configurar erros (para desenvolvimento)
error_reporting(E_ALL);
ini_set('display_errors', 1);

// 3. Conexão com banco (se necessário)
$banco = new mysqli("localhost:3307", "root", "", "nome_banco");
if ($banco->connect_error) {
    die("❌ Erro na conexão: " . $banco->connect_error);
}

// 4. Verificar autenticação (se necessário)
$usuario_logado = $_SESSION["usuario"] ?? null;
if (is_null($usuario_logado)) {
    header("Location: login.php");
    exit;
}

// 5. Processar formulários
if ($_SERVER["REQUEST_METHOD"] === "POST") {
    // Processar dados POST
    $nome = trim($_POST["nome"] ?? "");

    if (!empty($nome)) {
        // Processar dados válidos
        echo "✅ Dados processados!";
    } else {
        echo "❌ Erro: Dados inválidos!";
    }
}

// 6. Buscar dados do banco (se necessário)
$dados = [];
$sql = "SELECT * FROM tabela ORDER BY id DESC";
$resultado = $banco->query($sql);
if ($resultado && $resultado->num_rows > 0) {
    while ($row = $resultado->fetch_assoc()) {
        $dados[] = $row;
    }
}
?>

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha Página</title>
</head>
<body>
    <h1>Minha Aplicação PHP</h1>

    <!-- Seu HTML aqui -->

</body>
</html>
```

### 🔍 **Para Debug e Teste**

```php
// Debug básico
var_dump($variavel);     // Ver conteúdo detalhado
print_r($array);         // Ver estrutura de array
echo "Debug: $valor";    // Verificar valor simples

// Debug avançado
echo "<pre>";
print_r($_GET);          // Ver dados GET
print_r($_POST);         // Ver dados POST
print_r($_SESSION);      // Ver dados de sessão
echo "</pre>";

// Verificar tipos
echo gettype($variavel);
echo is_array($dados) ? "É array" : "Não é array";
echo empty($valor) ? "Vazio" : "Tem valor";

// Debug de banco
if ($banco->connect_error) {
    echo "❌ Erro de conexão: " . $banco->connect_error;
} else {
    echo "✅ Banco conectado!";
}

// Debug de consultas
$sql = "SELECT * FROM usuarios";
$resultado = $banco->query($sql);
echo "Registros encontrados: " . ($resultado ? $resultado->num_rows : 0);
```

### 📋 **Checklist de Validação**

#### **Formulários:**

- [ ] Verificar se `$_POST` ou `$_GET` não está vazio
- [ ] Usar `?? ""` para valores padrão
- [ ] Validar campos obrigatórios com `empty()`
- [ ] Usar `trim()` para remover espaços
- [ ] Validar email com `filter_var()`
- [ ] Verificar números com `is_numeric()`

#### **Banco de Dados:**

- [ ] Verificar `$banco->connect_error`
- [ ] Usar `global $banco` em funções
- [ ] Verificar `$resultado->num_rows > 0`
- [ ] Usar `fetch_object()` ou `fetch_assoc()`
- [ ] Fechar conexões se necessário

#### **Sessões:**

- [ ] `session_start()` no início
- [ ] Verificar se usuário está logado
- [ ] Usar `$_SESSION["chave"] ?? null`
- [ ] `session_destroy()` para logout
- [ ] `header()` + `exit` para redirecionamentos

#### **Segurança:**

- [ ] Não mostrar senhas em debug
- [ ] Validar dados antes de inserir no banco
- [ ] Usar prepared statements se possível
- [ ] Verificar permissões de acesso
- [ ] Escapar dados para HTML se necessário

### 🎯 **Templates Prontos para Copiar**

#### **Login Completo:**

```php
<?php
session_start();
$banco = new mysqli("localhost:3307", "root", "", "banco");

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $usuario = trim($_POST["usuario"] ?? "");
    $senha = $_POST["senha"] ?? "";

    if (!empty($usuario) && !empty($senha)) {
        $sql = "SELECT * FROM usuarios WHERE usuario='$usuario'";
        $resultado = $banco->query($sql);

        if ($resultado && $resultado->num_rows > 0) {
            $user = $resultado->fetch_object();
            if ($senha == $user->senha) {
                $_SESSION["usuario"] = $usuario;
                $_SESSION["id"] = $user->id;
                header("Location: dashboard.php");
                exit;
            }
        }
        $erro = "Usuário ou senha inválidos!";
    } else {
        $erro = "Preencha todos os campos!";
    }
}
?>

<form method="post">
    <?php if (isset($erro)): ?>
        <p style="color: red;"><?= $erro ?></p>
    <?php endif; ?>

    Usuário: <input type="text" name="usuario" required><br>
    Senha: <input type="password" name="senha" required><br>
    <input type="submit" value="Login">
</form>
```

#### **CRUD Básico:**

```php
<?php
session_start();
$banco = new mysqli("localhost:3307", "root", "", "banco");

// CREATE
if (isset($_POST["adicionar"])) {
    $nome = trim($_POST["nome"]);
    if (!empty($nome)) {
        $sql = "INSERT INTO itens (nome) VALUES ('$nome')";
        $banco->query($sql);
    }
}

// DELETE
if (isset($_GET["excluir"])) {
    $id = (int)$_GET["excluir"];
    $sql = "DELETE FROM itens WHERE id='$id'";
    $banco->query($sql);
}

// READ
$sql = "SELECT * FROM itens ORDER BY id DESC";
$resultado = $banco->query($sql);
?>

<form method="post">
    Nome: <input type="text" name="nome" required>
    <input type="submit" name="adicionar" value="Adicionar">
</form>

<ul>
<?php if ($resultado && $resultado->num_rows > 0): ?>
    <?php while ($item = $resultado->fetch_object()): ?>
        <li>
            <?= $item->nome ?>
            <a href="?excluir=<?= $item->id ?>">Excluir</a>
        </li>
    <?php endwhile; ?>
<?php else: ?>
    <li>Nenhum item encontrado</li>
<?php endif; ?>
</ul>
```

### 🚨 **Erros Mais Comuns - Soluções Rápidas**

1. **"session_start()"** → Colocar no início do arquivo
2. **"headers already sent"** → Usar `exit` após `header()`
3. **"undefined index"** → Usar `?? ""` ou `isset()`
4. **"connection refused"** → Verificar porta MySQL
5. **"undefined variable: banco"** → Usar `global $banco`
6. **"fetch_object() on boolean"** → Verificar se query funcionou
7. **"no database selected"** → Especificar nome do banco na conexão

### 🏆 **Dicas de Ouro para a Prova**

1. **Leia o enunciado 2x** antes de começar
2. **Teste a conexão** com banco primeiro
3. **Use var_dump()** para debugar
4. **Comente seu código** para não se perder
5. **Teste cada funcionalidade** antes de passar para a próxima
6. **Mantenha backup** do código funcionando
7. **Organize arquivos** em pastas lógicas
8. **Use nomes descritivos** para variáveis e funções

---

## 🎯 Dicas Finais

1. **Leia com calma** - Identifique o que cada parte faz
2. **Teste aos poucos** - Corrija um erro por vez
3. **Use var_dump()** para ver o que tem nas variáveis
4. **Sempre verifique** - Conexões, sessões, variáveis
5. **Mantenha a calma** - Os erros do PHP são bem claros

### Comandos úteis

```php
// Ver estrutura
print_r($_GET);
print_r($_POST);
print_r($_SESSION);

// Ver erros
error_reporting(E_ALL);
ini_set('display_errors', 1);
```

**🍀 BOA SORTE NA PROVA! 🚀**
