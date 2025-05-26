# 🎯 EXERCÍCIOS PRÁTICOS - PROVA PHP

## Análise e Desenvolvimento de Sistemas

---

## 📚 INSTRUÇÕES GERAIS

- **Faça cada exercício do ZERO** (não copie código pronto)
- **Teste cada exercício** no XAMPP antes da prova
- **Cada exercício cobre conceitos específicos** de uma aula
- **As respostas estão no final** do arquivo
- **Pratique até conseguir fazer sem consultar**

---

## 🟢 EXERCÍCIO 1 - FUNDAMENTOS PHP (Aula 1)

### **Objetivo:** Criar uma página que exibe informações pessoais com diferentes tipos de dados

**Crie um arquivo `exercicio1.php` que:**

1. Declare variáveis para: nome (string), idade (int), salário (float), ativo (boolean)
2. Use interpolação para exibir: "Olá [nome], você tem [idade] anos"
3. Use concatenação para exibir: "Salário: R$ [salário]"
4. Use var_dump() para mostrar o tipo da variável ativo
5. Converta a idade para string e concatene com " anos de experiência"

**Dados para teste:**

- Nome: "Maria Silva"
- Idade: 28
- Salário: 3500.75
- Ativo: true

---

## 🟡 EXERCÍCIO 2 - OPERADORES E ESTRUTURAS (Aula 2)

### **Objetivo:** Sistema de classificação de funcionários

**Crie um arquivo `exercicio2.php` que:**

1. Receba via GET: nome, idade, salario
2. Calcule o salário líquido (desconto de 15% se salário > 3000, senão 10%)
3. Classifique por idade: "Jovem" (<25), "Adulto" (25-50), "Sênior" (>50)
4. Use number_format() para formatar o salário com 2 casas decimais
5. Exiba resultado em HTML com cores diferentes para cada classificação

**URL de teste:** `exercicio2.php?nome=João&idade=30&salario=4500`

**Cores sugeridas:**

- Jovem: verde
- Adulto: azul
- Sênior: laranja

---

## 🔵 EXERCÍCIO 3 - LOOPS E ARRAYS (Aula 3)

### **Objetivo:** Sistema de notas de uma turma

**Crie um arquivo `exercicio3.php` que:**

1. Crie um array com 5 alunos (nome, nota1, nota2, nota3)
2. Use foreach para calcular a média de cada aluno
3. Use for para contar quantos alunos foram aprovados (média >= 7)
4. Crie um array associativo com estatísticas da turma
5. Exiba a maior e menor média da turma

**Dados dos alunos:**

```php
$turma = [
    ["nome" => "Ana", "nota1" => 8.5, "nota2" => 7.0, "nota3" => 9.0],
    ["nome" => "Bruno", "nota1" => 6.0, "nota2" => 5.5, "nota3" => 7.5],
    ["nome" => "Carlos", "nota1" => 9.0, "nota2" => 8.5, "nota3" => 8.0],
    ["nome" => "Diana", "nota1" => 5.0, "nota2" => 6.0, "nota3" => 5.5],
    ["nome" => "Eduardo", "nota1" => 7.5, "nota2" => 8.0, "nota3" => 7.0]
];
```

---

## 🟠 EXERCÍCIO 4 - FUNÇÕES E QUERY STRING (Aula 4)

### **Objetivo:** Calculadora de impostos com múltiplas funções

**Crie um arquivo `exercicio4.php` que:**

1. Crie função `calcularIR($salario)` que retorna o IR (0%, 7.5%, 15%, 22.5%, 27.5%)
2. Crie função `calcularINSS($salario)` que retorna o INSS (8%, 9%, 11%)
3. Crie função `salarioLiquido($salario)` que usa as funções acima
4. Crie função `classificarSalario($salario)` que retorna a faixa salarial
5. Receba salário via GET e exiba todos os cálculos

**Faixas IR:**

- Até R$ 1.903,98: 0%
- R$ 1.903,99 a R$ 2.826,65: 7,5%
- R$ 2.826,66 a R$ 3.751,05: 15%
- R$ 3.751,06 a R$ 4.664,68: 22,5%
- Acima de R$ 4.664,68: 27,5%

**URL de teste:** `exercicio4.php?salario=5000`

---

## 🟣 EXERCÍCIO 5 - FORMULÁRIOS E VALIDAÇÃO (Aula 5)

### **Objetivo:** Formulário de cadastro com validação completa

**Crie um arquivo `exercicio5.php` que:**

1. Crie formulário HTML com: nome, email, idade, senha, confirmar senha
2. Valide se todos os campos foram preenchidos
3. Valide se email tem formato válido (use filter_var)
4. Valide se idade está entre 18 e 65 anos
5. Valide se senha tem pelo menos 6 caracteres e senhas coincidem
6. Exiba mensagens de erro específicas para cada campo
7. Se tudo válido, exiba "Cadastro realizado com sucesso!"

**Validações específicas:**

- Nome: não pode estar vazio
- Email: formato válido
- Idade: entre 18 e 65
- Senha: mínimo 6 caracteres
- Confirmar senha: deve ser igual à senha

---

## 🔴 EXERCÍCIO 6 - SESSÕES E AUTENTICAÇÃO (Aula 6)

### **Objetivo:** Sistema completo de login com carrinho de compras

**Crie 3 arquivos:**

### **`login6.php`:**

1. Formulário de login (usuário e senha)
2. Validar credenciais: admin/123 ou user/456
3. Se válido, criar sessão e redirecionar para loja6.php
4. Se inválido, exibir erro

### **`loja6.php`:**

1. Verificar se usuário está logado
2. Exibir lista de produtos (array com nome e preço)
3. Permitir adicionar produtos ao carrinho (via GET)
4. Exibir carrinho atual com total
5. Link para logout

### **`logout6.php`:**

1. Destruir sessão
2. Redirecionar para login

**Produtos sugeridos:**

- Notebook: R$ 2500
- Mouse: R$ 50
- Teclado: R$ 150
- Monitor: R$ 800

---

## 🟤 EXERCÍCIO 7 - MANIPULAÇÃO DE STRINGS (Aula 7)

### **Objetivo:** Analisador de texto completo

**Crie um arquivo `exercicio7.php` que:**

1. Receba um texto via POST (textarea)
2. Conte: caracteres, palavras, frases (pontos finais)
3. Encontre a palavra mais longa
4. Substitua palavrões por asteriscos (lista: "droga", "maldito", "idiota")
5. Converta para: maiúscula, minúscula, primeira letra maiúscula
6. Exiba estatísticas completas do texto

**Funções a usar:**

- strlen(), str_word_count(), substr_count()
- str_replace(), strtoupper(), strtolower(), ucfirst()
- explode(), trim()

**Texto de teste:**
"Este é um texto de exemplo. Tem várias palavras e algumas frases. Droga, este exercício está ficando interessante!"

---

## ⚫ EXERCÍCIO 8 - BANCO DE DADOS (Aula 8)

### **Objetivo:** Sistema de tarefas com banco de dados

**Primeiro, crie o banco:**

```sql
CREATE DATABASE exercicio8;
USE exercicio8;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario VARCHAR(50) NOT NULL,
    senha VARCHAR(100) NOT NULL
);

CREATE TABLE tarefas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_usuario INT NOT NULL,
    titulo VARCHAR(100) NOT NULL,
    descricao TEXT,
    concluida BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (id_usuario) REFERENCES usuarios(id)
);

INSERT INTO usuarios (usuario, senha) VALUES ('admin', '123');
```

**Crie um arquivo `exercicio8.php` que:**

1. Conecte com o banco (localhost:3307, root, "", exercicio8)
2. Crie função `fazerLogin($usuario, $senha)` que retorna o ID do usuário
3. Crie função `adicionarTarefa($id_usuario, $titulo, $descricao)`
4. Crie função `listarTarefas($id_usuario)` que retorna array de objetos
5. Crie função `marcarConcluida($id_tarefa)`
6. Implemente interface simples para testar todas as funções

---

## 🔵 EXERCÍCIO 9 - PROJETO COMPLETO (Aulas 9-11)

### **Objetivo:** Sistema MVC de biblioteca

**Crie a estrutura:**

```
exercicio9/
├── index.php
├── config/
│   └── banco.php
├── controller/
│   ├── AuthController.php
│   └── LivrosController.php
└── view/
    ├── login.php
    ├── biblioteca.php
    └── emprestimos.php
```

**Banco de dados:**

```sql
CREATE DATABASE biblioteca;
USE biblioteca;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    senha VARCHAR(100) NOT NULL
);

CREATE TABLE livros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(200) NOT NULL,
    autor VARCHAR(100) NOT NULL,
    disponivel BOOLEAN DEFAULT TRUE
);

CREATE TABLE emprestimos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_usuario INT NOT NULL,
    id_livro INT NOT NULL,
    data_emprestimo DATE NOT NULL,
    data_devolucao DATE,
    FOREIGN KEY (id_usuario) REFERENCES usuarios(id),
    FOREIGN KEY (id_livro) REFERENCES livros(id)
);
```

**Funcionalidades:**

1. Login de usuários
2. Listar livros disponíveis
3. Emprestar livro (marcar como indisponível)
4. Devolver livro (marcar como disponível)
5. Histórico de empréstimos do usuário

**Rotas (index.php):**

- `?p=login` - Tela de login
- `?p=biblioteca` - Lista de livros
- `?p=emprestar&id=X` - Emprestar livro
- `?p=devolver&id=X` - Devolver livro
- `?p=meus-emprestimos` - Histórico do usuário

---

## 🎯 EXERCÍCIO BÔNUS - SIMULAÇÃO DE PROVA

### **Objetivo:** Código com 10 erros típicos para corrigir

**Analise e corrija o código abaixo:**

```php
<?php
// Arquivo com erros para correção
$usuario_logado = $_SESSION["usuario"];
$acao = $_GET["acao"];

$banco = new mysqli("localhost", "root", "", "sistema");

if ($acao == "login") {
    $user = $_POST["usuario"];
    $pass = $_POST["senha"];

    $sql = "SELECT * FROM usuarios WHERE usuario='$user'";
    $resultado = $banco->query($sql);

    $obj_user = $resultado->fetch_object();

    if ($pass == $obj_user->senha) {
        $_SESSION["usuario"] = $user;
        header("Location: dashboard.php");
    }
}

function adicionarTarefa($tarefa) {
    $sql = "INSERT INTO tarefas (texto) VALUES ('$tarefa')";
    $resultado = $banco->query($sql);
    return $resultado;
}

if (is_null($usuario_logado)) {
    header("Location: login.php");
}
?>
```

**Encontre e corrija os 10 erros!**

---

# 📝 RESPOSTAS DOS EXERCÍCIOS

---

## ✅ RESPOSTA EXERCÍCIO 1

```php
<?php
// Declaração de variáveis
$nome = "Maria Silva";
$idade = 28;
$salario = 3500.75;
$ativo = true;

// Interpolação
echo "Olá $nome, você tem $idade anos<br>";

// Concatenação
echo "Salário: R$ " . $salario . "<br>";

// var_dump do boolean
echo "Tipo da variável ativo: ";
var_dump($ativo);
echo "<br>";

// Conversão e concatenação
$idade_string = (string)$idade;
echo $idade_string . " anos de experiência<br>";
?>
```

---

## ✅ RESPOSTA EXERCÍCIO 2

```php
<?php
$nome = $_GET["nome"] ?? "Visitante";
$idade = $_GET["idade"] ?? 0;
$salario = $_GET["salario"] ?? 0;

// Calcular salário líquido
if ($salario > 3000) {
    $salario_liquido = $salario * 0.85; // 15% desconto
} else {
    $salario_liquido = $salario * 0.90; // 10% desconto
}

// Classificar por idade
if ($idade < 25) {
    $classificacao = "Jovem";
    $cor = "green";
} elseif ($idade <= 50) {
    $classificacao = "Adulto";
    $cor = "blue";
} else {
    $classificacao = "Sênior";
    $cor = "orange";
}

// Formatar salário
$salario_formatado = number_format($salario_liquido, 2, ",", ".");
?>

<!DOCTYPE html>
<html>
<head>
    <title>Classificação de Funcionário</title>
</head>
<body>
    <h1>Resultado da Classificação</h1>
    <p><strong>Nome:</strong> <?= $nome ?></p>
    <p><strong>Idade:</strong> <?= $idade ?> anos</p>
    <p><strong>Salário Bruto:</strong> R$ <?= number_format($salario, 2, ",", ".") ?></p>
    <p><strong>Salário Líquido:</strong> R$ <?= $salario_formatado ?></p>
    <p style="color: <?= $cor ?>"><strong>Classificação:</strong> <?= $classificacao ?></p>
</body>
</html>
```

---

## ✅ RESPOSTA EXERCÍCIO 3

```php
<?php
$turma = [
    ["nome" => "Ana", "nota1" => 8.5, "nota2" => 7.0, "nota3" => 9.0],
    ["nome" => "Bruno", "nota1" => 6.0, "nota2" => 5.5, "nota3" => 7.5],
    ["nome" => "Carlos", "nota1" => 9.0, "nota2" => 8.5, "nota3" => 8.0],
    ["nome" => "Diana", "nota1" => 5.0, "nota2" => 6.0, "nota3" => 5.5],
    ["nome" => "Eduardo", "nota1" => 7.5, "nota2" => 8.0, "nota3" => 7.0]
];

$medias = [];
$aprovados = 0;

// Calcular médias com foreach
foreach ($turma as $aluno) {
    $media = ($aluno["nota1"] + $aluno["nota2"] + $aluno["nota3"]) / 3;
    $medias[] = $media;

    echo "Aluno: " . $aluno["nome"] . " - Média: " . number_format($media, 2) . "<br>";

    if ($media >= 7) {
        echo "<span style='color: green'>APROVADO</span><br><br>";
    } else {
        echo "<span style='color: red'>REPROVADO</span><br><br>";
    }
}

// Contar aprovados com for
for ($i = 0; $i < count($medias); $i++) {
    if ($medias[$i] >= 7) {
        $aprovados++;
    }
}

// Estatísticas da turma
$estatisticas = [
    "total_alunos" => count($turma),
    "aprovados" => $aprovados,
    "reprovados" => count($turma) - $aprovados,
    "maior_media" => max($medias),
    "menor_media" => min($medias),
    "media_turma" => array_sum($medias) / count($medias)
];

echo "<h2>Estatísticas da Turma:</h2>";
foreach ($estatisticas as $chave => $valor) {
    echo ucfirst(str_replace("_", " ", $chave)) . ": " . number_format($valor, 2) . "<br>";
}
?>
```

---

## ✅ RESPOSTA EXERCÍCIO 4

```php
<?php
function calcularIR($salario) {
    if ($salario <= 1903.98) {
        return 0;
    } elseif ($salario <= 2826.65) {
        return $salario * 0.075;
    } elseif ($salario <= 3751.05) {
        return $salario * 0.15;
    } elseif ($salario <= 4664.68) {
        return $salario * 0.225;
    } else {
        return $salario * 0.275;
    }
}

function calcularINSS($salario) {
    if ($salario <= 1100) {
        return $salario * 0.08;
    } elseif ($salario <= 2203.48) {
        return $salario * 0.09;
    } else {
        return $salario * 0.11;
    }
}

function salarioLiquido($salario) {
    $ir = calcularIR($salario);
    $inss = calcularINSS($salario);
    return $salario - $ir - $inss;
}

function classificarSalario($salario) {
    if ($salario <= 1412) {
        return "Salário Mínimo";
    } elseif ($salario <= 3000) {
        return "Classe C";
    } elseif ($salario <= 6000) {
        return "Classe B";
    } else {
        return "Classe A";
    }
}

$salario = $_GET["salario"] ?? 0;

if ($salario > 0) {
    $ir = calcularIR($salario);
    $inss = calcularINSS($salario);
    $liquido = salarioLiquido($salario);
    $classificacao = classificarSalario($salario);

    echo "<h1>Calculadora de Impostos</h1>";
    echo "<p><strong>Salário Bruto:</strong> R$ " . number_format($salario, 2, ",", ".") . "</p>";
    echo "<p><strong>IR:</strong> R$ " . number_format($ir, 2, ",", ".") . "</p>";
    echo "<p><strong>INSS:</strong> R$ " . number_format($inss, 2, ",", ".") . "</p>";
    echo "<p><strong>Salário Líquido:</strong> R$ " . number_format($liquido, 2, ",", ".") . "</p>";
    echo "<p><strong>Classificação:</strong> $classificacao</p>";
} else {
    echo "<p>Por favor, informe um salário válido via GET: ?salario=5000</p>";
}
?>
```

---

## ✅ RESPOSTA EXERCÍCIO 5

```php
<?php
$erros = [];
$sucesso = false;

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $nome = $_POST["nome"] ?? "";
    $email = $_POST["email"] ?? "";
    $idade = $_POST["idade"] ?? "";
    $senha = $_POST["senha"] ?? "";
    $confirmar_senha = $_POST["confirmar_senha"] ?? "";

    // Validar nome
    if (empty($nome)) {
        $erros[] = "Nome é obrigatório";
    }

    // Validar email
    if (empty($email)) {
        $erros[] = "Email é obrigatório";
    } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $erros[] = "Email deve ter formato válido";
    }

    // Validar idade
    if (empty($idade)) {
        $erros[] = "Idade é obrigatória";
    } elseif ($idade < 18 || $idade > 65) {
        $erros[] = "Idade deve estar entre 18 e 65 anos";
    }

    // Validar senha
    if (empty($senha)) {
        $erros[] = "Senha é obrigatória";
    } elseif (strlen($senha) < 6) {
        $erros[] = "Senha deve ter pelo menos 6 caracteres";
    }

    // Validar confirmação de senha
    if (empty($confirmar_senha)) {
        $erros[] = "Confirmação de senha é obrigatória";
    } elseif ($senha !== $confirmar_senha) {
        $erros[] = "Senhas não coincidem";
    }

    // Se não há erros
    if (empty($erros)) {
        $sucesso = true;
    }
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Formulário de Cadastro</title>
    <style>
        .erro { color: red; }
        .sucesso { color: green; }
        .form-group { margin-bottom: 15px; }
    </style>
</head>
<body>
    <h1>Cadastro de Usuário</h1>

    <?php if ($sucesso): ?>
        <p class="sucesso">Cadastro realizado com sucesso!</p>
    <?php endif; ?>

    <?php if (!empty($erros)): ?>
        <div class="erro">
            <ul>
                <?php foreach ($erros as $erro): ?>
                    <li><?= $erro ?></li>
                <?php endforeach; ?>
            </ul>
        </div>
    <?php endif; ?>

    <form method="post">
        <div class="form-group">
            <label>Nome:</label>
            <input type="text" name="nome" value="<?= $_POST['nome'] ?? '' ?>">
        </div>

        <div class="form-group">
            <label>Email:</label>
            <input type="email" name="email" value="<?= $_POST['email'] ?? '' ?>">
        </div>

        <div class="form-group">
            <label>Idade:</label>
            <input type="number" name="idade" value="<?= $_POST['idade'] ?? '' ?>">
        </div>

        <div class="form-group">
            <label>Senha:</label>
            <input type="password" name="senha">
        </div>

        <div class="form-group">
            <label>Confirmar Senha:</label>
            <input type="password" name="confirmar_senha">
        </div>

        <input type="submit" value="Cadastrar">
    </form>
</body>
</html>
```

---

## ✅ RESPOSTA EXERCÍCIO 6

### **login6.php:**

```php
<?php
session_start();

// Se já está logado, redireciona
if (isset($_SESSION["usuario"])) {
    header("Location: loja6.php");
    exit;
}

$erro = "";

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $usuario = $_POST["usuario"] ?? "";
    $senha = $_POST["senha"] ?? "";

    if (($usuario === "admin" && $senha === "123") ||
        ($usuario === "user" && $senha === "456")) {
        $_SESSION["usuario"] = $usuario;
        header("Location: loja6.php");
        exit;
    } else {
        $erro = "Usuário ou senha incorretos!";
    }
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h1>Login</h1>

    <?php if ($erro): ?>
        <p style="color: red"><?= $erro ?></p>
    <?php endif; ?>

    <form method="post">
        <p>
            Usuário: <input type="text" name="usuario">
        </p>
        <p>
            Senha: <input type="password" name="senha">
        </p>
        <p>
            <input type="submit" value="Entrar">
        </p>
    </form>

    <p><small>Usuários: admin/123 ou user/456</small></p>
</body>
</html>
```

### **loja6.php:**

```php
<?php
session_start();

$usuario = $_SESSION["usuario"] ?? null;

if (is_null($usuario)) {
    header("Location: login6.php");
    exit;
}

// Produtos disponíveis
$produtos = [
    1 => ["nome" => "Notebook", "preco" => 2500],
    2 => ["nome" => "Mouse", "preco" => 50],
    3 => ["nome" => "Teclado", "preco" => 150],
    4 => ["nome" => "Monitor", "preco" => 800]
];

// Inicializar carrinho se não existe
if (!isset($_SESSION["carrinho"])) {
    $_SESSION["carrinho"] = [];
}

// Adicionar produto ao carrinho
$adicionar = $_GET["adicionar"] ?? null;
if ($adicionar && isset($produtos[$adicionar])) {
    $_SESSION["carrinho"][] = $produtos[$adicionar];
}

// Calcular total do carrinho
$total = 0;
foreach ($_SESSION["carrinho"] as $item) {
    $total += $item["preco"];
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Loja Online</title>
</head>
<body>
    <h1>Bem-vindo à Loja, <?= $usuario ?>!</h1>

    <h2>Produtos Disponíveis</h2>
    <?php foreach ($produtos as $id => $produto): ?>
        <p>
            <?= $produto["nome"] ?> - R$ <?= number_format($produto["preco"], 2, ",", ".") ?>
            <a href="?adicionar=<?= $id ?>">Adicionar ao Carrinho</a>
        </p>
    <?php endforeach; ?>

    <h2>Seu Carrinho</h2>
    <?php if (empty($_SESSION["carrinho"])): ?>
        <p>Carrinho vazio</p>
    <?php else: ?>
        <?php foreach ($_SESSION["carrinho"] as $item): ?>
            <p><?= $item["nome"] ?> - R$ <?= number_format($item["preco"], 2, ",", ".") ?></p>
        <?php endforeach; ?>
        <p><strong>Total: R$ <?= number_format($total, 2, ",", ".") ?></strong></p>
    <?php endif; ?>

    <p><a href="logout6.php">Sair</a></p>
</body>
</html>
```

### **logout6.php:**

```php
<?php
session_start();
session_destroy();
header("Location: login6.php");
exit;
?>
```

---

## ✅ RESPOSTA EXERCÍCIO 7

```php
<?php
$resultado = "";

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $texto = $_POST["texto"] ?? "";

    if (!empty($texto)) {
        // Estatísticas básicas
        $caracteres = strlen($texto);
        $palavras = str_word_count($texto);
        $frases = substr_count($texto, ".") + substr_count($texto, "!") + substr_count($texto, "?");

        // Encontrar palavra mais longa
        $array_palavras = explode(" ", $texto);
        $palavra_mais_longa = "";
        foreach ($array_palavras as $palavra) {
            $palavra = trim($palavra, ".,!?");
            if (strlen($palavra) > strlen($palavra_mais_longa)) {
                $palavra_mais_longa = $palavra;
            }
        }

        // Substituir palavrões
        $palavroes = ["droga", "maldito", "idiota"];
        $texto_limpo = $texto;
        foreach ($palavroes as $palavrao) {
            $asteriscos = str_repeat("*", strlen($palavrao));
            $texto_limpo = str_ireplace($palavrao, $asteriscos, $texto_limpo);
        }

        // Conversões
        $maiuscula = strtoupper($texto);
        $minuscula = strtolower($texto);
        $primeira_maiuscula = ucfirst(strtolower($texto));

        $resultado = "
        <h2>Análise do Texto</h2>
        <p><strong>Caracteres:</strong> $caracteres</p>
        <p><strong>Palavras:</strong> $palavras</p>
        <p><strong>Frases:</strong> $frases</p>
        <p><strong>Palavra mais longa:</strong> $palavra_mais_longa (" . strlen($palavra_mais_longa) . " caracteres)</p>

        <h3>Texto sem palavrões:</h3>
        <p>$texto_limpo</p>

        <h3>Conversões:</h3>
        <p><strong>Maiúscula:</strong> $maiuscula</p>
        <p><strong>Minúscula:</strong> $minuscula</p>
        <p><strong>Primeira maiúscula:</strong> $primeira_maiuscula</p>
        ";
    }
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Analisador de Texto</title>
</head>
<body>
    <h1>Analisador de Texto</h1>

    <form method="post">
        <p>
            <label>Digite seu texto:</label><br>
            <textarea name="texto" rows="5" cols="50"><?= $_POST["texto"] ?? "" ?></textarea>
        </p>
        <p>
            <input type="submit" value="Analisar">
        </p>
    </form>

    <?= $resultado ?>

    <p><small>Texto de teste: "Este é um texto de exemplo. Tem várias palavras e algumas frases. Droga, este exercício está ficando interessante!"</small></p>
</body>
</html>
```

---

## ✅ RESPOSTA EXERCÍCIO 8

```php
<?php
// Conexão com banco
$banco = new mysqli("localhost:3307", "root", "", "exercicio8");

if ($banco->connect_error) {
    die("Erro na conexão: " . $banco->connect_error);
}

function fazerLogin($usuario, $senha) {
    global $banco;

    $sql = "SELECT * FROM usuarios WHERE usuario='$usuario'";
    $resultado = $banco->query($sql);

    if ($resultado->num_rows > 0) {
        $obj_usuario = $resultado->fetch_object();
        if ($senha == $obj_usuario->senha) {
            return $obj_usuario->id;
        }
    }
    return false;
}

function adicionarTarefa($id_usuario, $titulo, $descricao) {
    global $banco;

    $sql = "INSERT INTO tarefas (id_usuario, titulo, descricao) VALUES ('$id_usuario', '$titulo', '$descricao')";
    $resultado = $banco->query($sql);

    return $resultado;
}

function listarTarefas($id_usuario) {
    global $banco;

    $sql = "SELECT * FROM tarefas WHERE id_usuario='$id_usuario'";
    $resultado = $banco->query($sql);

    $tarefas = [];
    if ($resultado->num_rows > 0) {
        while ($tarefa = $resultado->fetch_object()) {
            $tarefas[] = $tarefa;
        }
    }

    return $tarefas;
}

function marcarConcluida($id_tarefa) {
    global $banco;

    $sql = "UPDATE tarefas SET concluida=1 WHERE id='$id_tarefa'";
    $resultado = $banco->query($sql);

    return $resultado;
}

// Interface de teste
session_start();

$acao = $_GET["acao"] ?? "";
$mensagem = "";

// Processar ações
if ($acao === "login") {
    $usuario = $_POST["usuario"] ?? "";
    $senha = $_POST["senha"] ?? "";

    $id_usuario = fazerLogin($usuario, $senha);
    if ($id_usuario) {
        $_SESSION["id_usuario"] = $id_usuario;
        $_SESSION["usuario"] = $usuario;
        $mensagem = "Login realizado com sucesso!";
    } else {
        $mensagem = "Usuário ou senha incorretos!";
    }
}

if ($acao === "adicionar" && isset($_SESSION["id_usuario"])) {
    $titulo = $_POST["titulo"] ?? "";
    $descricao = $_POST["descricao"] ?? "";

    if (!empty($titulo)) {
        if (adicionarTarefa($_SESSION["id_usuario"], $titulo, $descricao)) {
            $mensagem = "Tarefa adicionada com sucesso!";
        }
    }
}

if ($acao === "concluir" && isset($_SESSION["id_usuario"])) {
    $id_tarefa = $_GET["id"] ?? "";
    if (marcarConcluida($id_tarefa)) {
        $mensagem = "Tarefa marcada como concluída!";
    }
}

if ($acao === "logout") {
    session_destroy();
    header("Location: exercicio8.php");
    exit;
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Sistema de Tarefas</title>
</head>
<body>
    <h1>Sistema de Tarefas</h1>

    <?php if ($mensagem): ?>
        <p style="color: green"><?= $mensagem ?></p>
    <?php endif; ?>

    <?php if (!isset($_SESSION["usuario"])): ?>
        <!-- Formulário de Login -->
        <h2>Login</h2>
        <form method="post" action="?acao=login">
            <p>Usuário: <input type="text" name="usuario"></p>
            <p>Senha: <input type="password" name="senha"></p>
            <p><input type="submit" value="Entrar"></p>
        </form>
        <p><small>Use: admin / 123</small></p>
    <?php else: ?>
        <!-- Área logada -->
        <p>Bem-vindo, <?= $_SESSION["usuario"] ?>! <a href="?acao=logout">Sair</a></p>

        <!-- Adicionar tarefa -->
        <h2>Adicionar Tarefa</h2>
        <form method="post" action="?acao=adicionar">
            <p>Título: <input type="text" name="titulo"></p>
            <p>Descrição: <textarea name="descricao"></textarea></p>
            <p><input type="submit" value="Adicionar"></p>
        </form>

        <!-- Listar tarefas -->
        <h2>Suas Tarefas</h2>
        <?php
        $tarefas = listarTarefas($_SESSION["id_usuario"]);
        if (empty($tarefas)):
        ?>
            <p>Nenhuma tarefa encontrada.</p>
        <?php else: ?>
            <?php foreach ($tarefas as $tarefa): ?>
                <div style="border: 1px solid #ccc; padding: 10px; margin: 10px 0;">
                    <h3><?= $tarefa->titulo ?></h3>
                    <p><?= $tarefa->descricao ?></p>
                    <p>Status:
                        <?php if ($tarefa->concluida): ?>
                            <span style="color: green">Concluída</span>
                        <?php else: ?>
                            <span style="color: orange">Pendente</span>
                            <a href="?acao=concluir&id=<?= $tarefa->id ?>">Marcar como concluída</a>
                        <?php endif; ?>
                    </p>
                </div>
            <?php endforeach; ?>
        <?php endif; ?>
    <?php endif; ?>
</body>
</html>
```

---

## ✅ RESPOSTA EXERCÍCIO 9

### **index.php:**

```php
<?php
$pagina = $_GET["p"] ?? "login";

switch ($pagina) {
    case "login":
        require_once "controller/AuthController.php";
        AuthController::login();
        break;

    case "biblioteca":
        require_once "controller/LivrosController.php";
        LivrosController::index();
        break;

    case "emprestar":
        require_once "controller/LivrosController.php";
        LivrosController::emprestar();
        break;

    case "devolver":
        require_once "controller/LivrosController.php";
        LivrosController::devolver();
        break;

    case "meus-emprestimos":
        require_once "controller/LivrosController.php";
        LivrosController::meusEmprestimos();
        break;

    case "logout":
        require_once "controller/AuthController.php";
        AuthController::logout();
        break;

    default:
        require_once "controller/AuthController.php";
        AuthController::login();
        break;
}
?>
```

### **config/banco.php:**

```php
<?php
$banco = new mysqli("localhost:3307", "root", "", "biblioteca");

if ($banco->connect_error) {
    die("Erro na conexão: " . $banco->connect_error);
}
?>
```

### **controller/AuthController.php:**

```php
<?php
require_once __DIR__ . "/../config/banco.php";

class AuthController {

    static function login() {
        global $banco;

        session_start();

        // Se já está logado, redireciona
        if (isset($_SESSION["usuario_id"])) {
            header("Location: ?p=biblioteca");
            exit;
        }

        $erro = "";

        if ($_SERVER["REQUEST_METHOD"] === "POST") {
            $email = $_POST["email"] ?? "";
            $senha = $_POST["senha"] ?? "";

            $sql = "SELECT * FROM usuarios WHERE email='$email'";
            $resultado = $banco->query($sql);

            if ($resultado->num_rows > 0) {
                $usuario = $resultado->fetch_object();
                if ($senha == $usuario->senha) {
                    $_SESSION["usuario_id"] = $usuario->id;
                    $_SESSION["usuario_nome"] = $usuario->nome;
                    header("Location: ?p=biblioteca");
                    exit;
                } else {
                    $erro = "Senha incorreta!";
                }
            } else {
                $erro = "Usuário não encontrado!";
            }
        }

        include __DIR__ . "/../view/login.php";
    }

    static function logout() {
        session_start();
        session_destroy();
        header("Location: ?p=login");
        exit;
    }
}
?>
```

### **controller/LivrosController.php:**

```php
<?php
require_once __DIR__ . "/../config/banco.php";

class LivrosController {

    static function verificarLogin() {
        session_start();
        if (!isset($_SESSION["usuario_id"])) {
            header("Location: ?p=login");
            exit;
        }
    }

    static function index() {
        global $banco;

        self::verificarLogin();

        $sql = "SELECT * FROM livros WHERE disponivel=1";
        $livros = $banco->query($sql);

        include __DIR__ . "/../view/biblioteca.php";
    }

    static function emprestar() {
        global $banco;

        self::verificarLogin();

        $id_livro = $_GET["id"] ?? "";
        $id_usuario = $_SESSION["usuario_id"];

        if (!empty($id_livro)) {
            // Marcar livro como indisponível
            $sql = "UPDATE livros SET disponivel=0 WHERE id='$id_livro'";
            $banco->query($sql);

            // Registrar empréstimo
            $data_hoje = date("Y-m-d");
            $sql = "INSERT INTO emprestimos (id_usuario, id_livro, data_emprestimo) VALUES ('$id_usuario', '$id_livro', '$data_hoje')";
            $banco->query($sql);
        }

        header("Location: ?p=biblioteca");
        exit;
    }

    static function devolver() {
        global $banco;

        self::verificarLogin();

        $id_emprestimo = $_GET["id"] ?? "";

        if (!empty($id_emprestimo)) {
            // Buscar empréstimo
            $sql = "SELECT * FROM emprestimos WHERE id='$id_emprestimo'";
            $resultado = $banco->query($sql);

            if ($resultado->num_rows > 0) {
                $emprestimo = $resultado->fetch_object();

                // Marcar livro como disponível
                $sql = "UPDATE livros SET disponivel=1 WHERE id='" . $emprestimo->id_livro . "'";
                $banco->query($sql);

                // Atualizar data de devolução
                $data_hoje = date("Y-m-d");
                $sql = "UPDATE emprestimos SET data_devolucao='$data_hoje' WHERE id='$id_emprestimo'";
                $banco->query($sql);
            }
        }

        header("Location: ?p=meus-emprestimos");
        exit;
    }

    static function meusEmprestimos() {
        global $banco;

        self::verificarLogin();

        $id_usuario = $_SESSION["usuario_id"];

        $sql = "SELECT e.*, l.titulo, l.autor FROM emprestimos e
                JOIN livros l ON e.id_livro = l.id
                WHERE e.id_usuario='$id_usuario'
                ORDER BY e.data_emprestimo DESC";
        $emprestimos = $banco->query($sql);

        include __DIR__ . "/../view/emprestimos.php";
    }
}
?>
```

### **view/login.php:**

```php
<!DOCTYPE html>
<html>
<head>
    <title>Login - Biblioteca</title>
</head>
<body>
    <h1>Sistema de Biblioteca</h1>

    <?php if (isset($erro) && $erro): ?>
        <p style="color: red"><?= $erro ?></p>
    <?php endif; ?>

    <form method="post">
        <p>Email: <input type="email" name="email"></p>
        <p>Senha: <input type="password" name="senha"></p>
        <p><input type="submit" value="Entrar"></p>
    </form>
</body>
</html>
```

### **view/biblioteca.php:**

```php
<!DOCTYPE html>
<html>
<head>
    <title>Biblioteca</title>
</head>
<body>
    <h1>Biblioteca - Livros Disponíveis</h1>

    <p>Bem-vindo, <?= $_SESSION["usuario_nome"] ?>!
       <a href="?p=meus-emprestimos">Meus Empréstimos</a> |
       <a href="?p=logout">Sair</a>
    </p>

    <?php if ($livros->num_rows > 0): ?>
        <?php while ($livro = $livros->fetch_object()): ?>
            <div style="border: 1px solid #ccc; padding: 10px; margin: 10px 0;">
                <h3><?= $livro->titulo ?></h3>
                <p><strong>Autor:</strong> <?= $livro->autor ?></p>
                <a href="?p=emprestar&id=<?= $livro->id ?>">Emprestar</a>
            </div>
        <?php endwhile; ?>
    <?php else: ?>
        <p>Nenhum livro disponível no momento.</p>
    <?php endif; ?>
</body>
</html>
```

### **view/emprestimos.php:**

```php
<!DOCTYPE html>
<html>
<head>
    <title>Meus Empréstimos</title>
</head>
<body>
    <h1>Meus Empréstimos</h1>

    <p><a href="?p=biblioteca">Voltar à Biblioteca</a> | <a href="?p=logout">Sair</a></p>

    <?php if ($emprestimos->num_rows > 0): ?>
        <?php while ($emprestimo = $emprestimos->fetch_object()): ?>
            <div style="border: 1px solid #ccc; padding: 10px; margin: 10px 0;">
                <h3><?= $emprestimo->titulo ?></h3>
                <p><strong>Autor:</strong> <?= $emprestimo->autor ?></p>
                <p><strong>Data do Empréstimo:</strong> <?= date("d/m/Y", strtotime($emprestimo->data_emprestimo)) ?></p>

                <?php if (is_null($emprestimo->data_devolucao)): ?>
                    <p style="color: orange"><strong>Status:</strong> Em aberto</p>
                    <a href="?p=devolver&id=<?= $emprestimo->id ?>">Devolver</a>
                <?php else: ?>
                    <p style="color: green"><strong>Status:</strong> Devolvido em <?= date("d/m/Y", strtotime($emprestimo->data_devolucao)) ?></p>
                <?php endif; ?>
            </div>
        <?php endwhile; ?>
    <?php else: ?>
        <p>Você não possui empréstimos.</p>
    <?php endif; ?>
</body>
</html>
```

---

## ✅ RESPOSTA EXERCÍCIO BÔNUS

### **Código corrigido:**

```php
<?php
session_start(); // 1. Adicionar session_start()

$usuario_logado = $_SESSION["usuario"] ?? null; // 2. Adicionar ?? null
$acao = $_GET["acao"] ?? null; // 3. Adicionar ?? null

$banco = new mysqli("localhost", "root", "", "sistema");

// 4. Adicionar verificação de conexão
if ($banco->connect_error) {
    die("Erro na conexão: " . $banco->connect_error);
}

if ($acao == "login") {
    $user = $_POST["usuario"] ?? null; // 5. Adicionar ?? null
    $pass = $_POST["senha"] ?? null; // 6. Adicionar ?? null

    $sql = "SELECT * FROM usuarios WHERE usuario='$user'";
    $resultado = $banco->query($sql);

    // 7. Verificar se há resultados antes de fetch_object
    if ($resultado->num_rows > 0) {
        $obj_user = $resultado->fetch_object();

        if ($pass == $obj_user->senha) {
            $_SESSION["usuario"] = $user;
            header("Location: dashboard.php");
            exit; // 8. Adicionar exit após header
        }
    }
}

function adicionarTarefa($tarefa) {
    global $banco; // 9. Adicionar global $banco

    $sql = "INSERT INTO tarefas (texto) VALUES ('$tarefa')";
    $resultado = $banco->query($sql);
    return $resultado;
}

if (is_null($usuario_logado)) {
    header("Location: login.php");
    exit; // 10. Adicionar exit após header
}
?>
```

### **Os 10 erros encontrados:**

1. **Faltava `session_start()`** no início
2. **`$_SESSION["usuario"]`** sem verificação `?? null`
3. **`$_GET["acao"]`** sem verificação `?? null`
4. **`new mysqli()`** sem verificação de erro de conexão
5. **`$_POST["usuario"]`** sem verificação `?? null`
6. **`$_POST["senha"]`** sem verificação `?? null`
7. **`fetch_object()`** sem verificar se `num_rows > 0`
8. **`header()`** sem `exit` após redirecionamento
9. **Função sem `global $banco`**
10. **Segundo `header()`** sem `exit`

---

**🎉 PARABÉNS! VOCÊ COMPLETOU TODOS OS EXERCÍCIOS!**

**🚀 AGORA VOCÊ ESTÁ PREPARADO PARA A PROVA!**

**🍀 BOA SORTE! 🏆**
