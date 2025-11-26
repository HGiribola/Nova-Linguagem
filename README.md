# Mini Compilador — Nova Linguagem

Projeto acadêmico: mini compilador para uma linguagem imperativa simplificada (variáveis inteiras, input/print, expressões aritméticas, if/else, while).

## Estrutura do projeto
(Arquivos presentes no workspace — adapte se renomeou pastas)
- package/CodeGenerator.java
- package/Expr.java
- package/Instruction.java
- package/Interpreter.java
- package/Lexer.java
- package/Main.java
- package/OpCode.java
- package/Parser.java
- package/SemanticAnalyzer.java
- package/Stmt.java
- package/Token.java
- package/TokenType.java

> Observação importante: evite usar uma pasta chamada `package` — `package` é palavra reservada em Java. Veja seção "Compilar" para correções.

## Objetivo do README
- Explicar como compilar/rodar no Windows
- Descrever sintaxe básica da mini-linguagem
- Listar tokens principais e opcodes usados pela máquina virtual
- Exemplos de uso e erros comuns

---

## Como compilar e executar (Windows — cmd ou PowerShell)

Situação A — código sem declaração de pacote (arquivos na raiz do src):
1. Abra o terminal no diretório:
   cd "c:\Users\Henrique\Documents\Nova Linguagem"
2. Compilar:
   ```
   javac -d out *.java
   ```
3. Executar (classe com main em pacote default):
   ```
   java -cp out Main
   ```

Situação B — código em pacote válido (recomendado: renomear pasta `package` para `mylang` e adicionar `package mylang;` nos sources):
1. Renomeie a pasta:
   - No Explorer: renomeie `package` → `mylang`
2. No topo de cada .java em `mylang/` adicione:
   ```java
   package mylang;
   ```
3. Compilar:
   ```
   javac -d out mylang\*.java
   ```
4. Executar:
   ```
   java -cp out mylang.Main
   ```

Se preferir, posso gerar automaticamente as declarações `package mylang;` para todos os arquivos.

---

## Sintaxe resumida da linguagem

- Declaração de variável:
  ```
  int x;
  ```
- Atribuição:
  ```
  x = 5;
  ```
- Entrada/saída:
  ```
  input x;
  print x;
  ```
- Condicional:
  ```
  if (x == 0) { ... } else { ... }
  ```
- Laço:
  ```
  while (i < x) { ... }
  ```
- Blocos: `{ ... }`
- Terminações: ponto e vírgula `;`

Operadores aritméticos e comparativos comuns: `+ - * / == != < <= > >=`

---

## Tokens (resumo)
- Palavra-chave: `int`, `input`, `print`, `if`, `else`, `while`
- Identificador: letras/underscores seguidas por letras/dígitos
- Número: sequência de dígitos (inteiro)
- Símbolos: `(` `)` `{` `}` `;` `=` `==` `!=` `<` `>` `+` `-` `*` `/`
- Comentários: (ver Lexer) — se não implementado, evitar comentários inline.

---

## Máquina virtual — instruções principais (exemplo)
A implementação real pode variar; aqui estão opcodes típicos usados no projeto:
- PUSH <valor>      — empilha número literal
- LOAD <var>        — empilha valor da variável
- STORE <var>       — desempilha e armazena em variável
- ADD, SUB, MUL, DIV — operações aritméticas (top2)
- PRINT             — imprime topo da pilha
- INPUT <var>       — lê inteiro do usuário e armazena em var
- JUMP <addr>       — salto incondicional
- JZ <addr>         — salto se topo == 0
- JNZ <addr>        — salto se topo != 0
- HALT              — finaliza execução

Exemplo de geração: `i = i + 1;` → LOAD i, PUSH 1, ADD, STORE i

---

## Exemplos

Entrada e Saída
```
int x;
input x;
print x;
```
Usuário digita `7` → saída:
```
7
```

Laço
```
int i;
int x;
i = 0;
x = 3;
while (i < x) {
  print i;
  i = i + 1;
}
```
Saída:
```
0
1
2
```

Condicional
```
int x;
x = 0;
if (x == 0) {
  print 999;
} else {
  print 111;
}
```
Saída: `999`

---

## Erros comuns e como resolver
- Pasta chamada `package`: renomeie para `mylang` ou outro nome válido e adicione `package mylang;` nos arquivos Java.
- Caminho de classes x declaração de pacote: garantIR que estrutura de pastas reflita declarações `package`.
- Erro semântico: uso de variável não declarada — verifique declarações antes do uso (SemanticAnalyzer).
- Exceções em tempo de execução na VM: revisar ordem de geração de instruções e manipulação de pilha.

---

## Testes e execução interativa
- Recomenda-se criar pequenos arquivos .src/.txt com programas de teste.
- Para entrada interativa, o Interpreter deve ler de stdin; ao rodar no terminal, digite valores quando solicitado.

---

## Próximos passos sugeridos
- Gerar automaticamente cabeçalhos `package mylang;` e mover arquivos para `mylang/`.
- Gerar Javadoc a partir do código.
- Documentar a gramática formal (BNF) e precedência de operadores.
- Adicionar testes unitários JUnit para Lexer, Parser, SemanticAnalyzer e Interpreter.

---

Se quiser, eu:
- gero e salvo este README.md no caminho acima agora, e/ou
- insiro automaticamente `package mylang;` em todos os .java e renomeio a pasta `package` → `mylang`.

Responda: "Salvar README" ou "Salvar + adicionar package" (ou apenas diga qual opção prefere).