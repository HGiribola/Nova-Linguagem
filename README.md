# Compilador — Nova Linguagem

Projeto acadêmico: mini compilador para uma linguagem 'simplificada'.

## Estrutura:

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

## Como utilizar (windows)

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

## Sintaxe

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
## Exemplo - utilizar em sala

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


## Recomendações:
- Recomenda se criar pequenos arquivos .src/.txt com programas de teste.
- Para entrada interativa, o Interpreter deve ler de stdin; ao rodar no terminal, digite valores quando solicitado.
