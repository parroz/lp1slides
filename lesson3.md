---
marp: true
theme: default
paginate: true
incremental: true
header: "📚 Linguagens de Programação 1 | LEI, LEIRT, LIG"
footer: "![logo](./logo_lp1.png)![logo](./logo_lusofona.png)  Pedro Arroz Serra | pedro.serra@ulusofona.pt"
---


<style>
img[alt="logo"] {
  width: auto;  /* Adjust width */
  height: 25px; /* Keep aspect ratio */
  vertical-align: bottom; /* Align text with the image */
}
img[alt="pic_middle"] {
  width: auto;  /* Adjust width */
  height: 150px; /* Keep aspect ratio */
  vertical-align: middle; /* Align text with the image */
}
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
ul { list-style-type: none; padding-left: 0;}

</style>

# 📢 Linguagens de Programação 1

```c
int aula = 1;
printf("\aAula #%d\n", ++aula + 1);
```

### 💬 Message of the Day 
*“UNIX is simple. It just takes a genius to understand its simplicity.”*
*“C is quirky, flawed, and an enormous success.””* 
— Dennis Ritchie

---

# 🎓 Dennis Ritchie (1941–2011)
* Criador da linguagem de programação **C**.
* Foi um dos criadores do sistema operativo **UNIX**
* Fundou o **World Wide Web Consortium** W3C

---

# 📌 Conteúdo da Aula  
* ✅ **Entradas e Saídas Pré-formatadas**
    * ✅ **Funções `printf()` e `scanf()`**  
* ✅ **Operadores**  
    * ✅ **Operadores Aritméticos**  
    * ✅ **Operadores Primários**  
    * ✅ **Operadores Relacionais**  
    * ✅ **Operadores Lógicos**  

---

# 🎤 Entradas e Saídas Pré-formatadas 🎤


* 📌 O C possui funções específicas para **entrada e saída de dados**, sendo as principais:
* ✅ `printf()` → Exibir dados formatados na saída padrão (ecrã).
* ✅ `scanf()` → Ler dados formatados da entrada padrão (teclado).

---

## 🖥️ Função `printf()`

* 📌 A função `printf()` escreve um **texto formatado** no terminal.
* 📌 Aceita um número variável de argumentos.
* 📌 Sintaxe:

<div data-marpit-fragment>

```c
printf("Texto com %formato", variáveis);
```

</div>

* 📌 **Exemplo Simples:**

<div data-marpit-fragment>

```c
int idade = 25;
printf("Idade: %d anos\n", idade);
```
✅ **Saída:** `Idade: 25 anos`

</div>

---

### 🔠 Formatadores de `printf()`

| Formato | Tipo de Dado | Exemplo | Saída |
|---------|------------|---------|-------|
| `%d` ou `%i`    | Inteiro Decimal | `printf("%d", 42);` | `42` |
| `%x`, `X`    | Hexadecimal | `printf("%x, %X", 255, 170);` | `ff, AA` |
| `%o`    | Octal | `printf("%o", 255);` | `377` |
| `%u`    | Inteiro Decimal sem sinal | `printf("%u", 10);` | `10` |

---

### 🔠 Formatadores de `printf()` (cont.)

| Formato | Tipo de Dado | Exemplo | Saída |
|---------|------------|---------|-------|
| `%c`    | Caractere | `printf("%c", 'A');` | `A` |
| `%s`    | String | `printf("%s", "Ola");` | `Ola` |
| `%f`    | Numero real | `printf("%.2f", 3.1415);` | `3.14` |

---

### 🔠 Formatadores de `printf()` (cont.)

| Formato | Tipo de Dado | Exemplo | Saída |
|---------|------------|---------|-------|
| `%e`    | Numero real notação científica | `printf("%e", 0.001);` | `1e-3` |
| `%E`    | Numero real em notação científica | `printf("%E", 0.01);` | `1E-2` |
| `%g`    | escolhe automaticamente a forma que ocupar menos espaço| `printf("%g", 0.00001);` | `1E-5` |

---

### 🎭 Opções de Formatação no `printf()`

```c
int a = 42
```

| Formato | Exemplo | Saída | Explicação |
|---------|---------|-------|------------|
| `%5d`  | `printf("*%5d*", a);` | `*   42*` | imprime `a` ocupando 5 caracteres |
| `%-5d` | `printf("*%-5d*",a);` | `*42   *` | imprime `a` ocupando 5 caracteres alinhado à esquerda | 
| `%06d` | `printf("*%06d*",a);` | `*000042*` | imprime `a` ocupando 6 caracteres, preenche os epaços com 0's |

---
### 🎭 Opções de Formatação no `printf()` (cont.)

```c
float pi = 3.14159
```
| Formato | Exemplo | Saída | Explicação |
|---------|---------|-------|------------|
| `%4.2f` | `printf("*%4.2f*", pi);` | `*3.14*` | imprime `pi` ocupando 4 caracteres, 2 à direita da vírgula. |
| `%05.2f` | `printf("*%4.2f*", pi);` | `*03.14*` | imprime `pi` ocupando 4 caracteres, 2 à direita da vírgula. Preenche os epaços com 0's |


⚠️ **A vírgula também é um caracter**

---

## 🎤 Função `scanf()`

* 📌 `scanf()` permite **ler valores formatados do teclado**.
* 📌 **Sintaxe:**

<div data-marpit-fragment>

```c
scanf("%formato", &variavel);
```

</div>

* 📌 **Exemplo:**

<div data-marpit-fragment>

```c
int num;
scanf("%d", &num);
```

</div>

---

# 📝 Formatadores de `scanf()`

<div class='grid'>
<div>


| Formato | Tipo de Dado | Exemplo de Entrada |
|---------|------------|----------------|
| `%d`    | Inteiro | `42` |
| `%f`    | Float | `3.14` |
| `%c`    | Caractere | `A` |
| `%s`    | String | `Hello` |
| `%x`    | Hexadecimal | `ff` |

</div>
<div>

* 📌 **IMPORTANTE:**
* ✅ `scanf("%d", &var);` **→ Usa `&` para armazenar valores em variáveis!**
* ⚠️ **Exceção:** Para strings (`%s`), **não é necessário `&`** 🤔🤔

</div>
</div>

---

# ⚠️ Erros Comuns no `scanf()`

<div class='grid'>
<div>

* ❌ **Falta do `&` (passagem por referência)**

<div data-marpit-fragment>

```c
int x;
scanf("%d", x);  // ❌ ERRO
```

</div>

* ✅ **Correcto:**

<div data-marpit-fragment>

```c
int x;
scanf("%d", &x);  // ✔️ Correto
```
</div>

</div>
<div>

* ❌ **Leitura insegura de strings:**

<div data-marpit-fragment>

```c
char nome[10];
scanf("%s", nome);
// ⚠️ PERIGOSO! Pode causar `buffer overflow`
```

</div>

* ✅ **Solução mais segura:**

<div data-marpit-fragment>

```c
scanf("%9s", nome);
// ✔️ Limita a entrada a 9 caracteres
```

</div>

</div>
</div>


---


# 🎯 Exemplo Completo

```c
#include <stdio.h>
int main() {
    int idade;
    float altura;
    char nome[20];
    printf("Digite seu nome: ");
    scanf("%19s", nome);  // Limita a 19 caracteres
    printf("Digite sua idade e altura: ");
    scanf("%d %f", &idade, &altura);
    printf("Nome: %s | Idade: %d | Altura: %.2f\n", nome, idade, altura);
    return 0;
}
```
✅ **Entrada:** `Alice 25 1.65`
✅ **Saída:** `Nome: Alice | Idade: 25 | Altura: 1.65`

---

# 🔣 Operadores

---

## 🎯 O que são Operadores?  
* 📌 **Operadores são símbolos que realizam operações em literais ou variáveis.**  
* 📌 **Exemplo:** `+` é o operador de soma.  
* 📌 **Podem ser:**
    * ✅ Operadores **Aritméticos**  
    * ✅ Operadores **Relacionais**  
    * ✅ Operadores **Atribuição**  
    * ✅ Operadores **Lógicos**  

---

## ➕ Operadores Aritméticos

* São Utilizados em **tipos inteiros e reais**.  
* 📌 **Podem ser:**
* ✅ **Unários** → Requerem **um único operando** (`x++`, `-a`).
* ✅ **Binários** → Requerem **dois operandos** (`x + y`, `a * b`).

<div data-marpit-fragment>

### Operadores Aritméticos Unários

| Operador  | Nome        | Exemplo  |
|-----------|-------------|----------|
| `+`       | Unário Mais | `i = +1` |
| `-`       | Unário Menos| `j = -i` |

</div>

---
### 🔢 Operadores Aritméticos Binários


| Operador  | Nome          | Exenplo |
|-----------|---------------|---------|
| `+`       | Adição        | `y + z` |
| `-`       | Subtracção    | `x - y` |
| `*`       | Multiplicação | `x * y` |
| `/`       | Divisão       | `x / y` |
| `%`       | Módulo        | `x % y` |

---

#### 🔢 Precedência e Associatividade  

* 📌 **Regras para resolver ambiguidades em expressões com múltiplos operadores.**  
* 📌 **Ordem de Precedência:**

<div data-marpit-fragment>

| Precedência    |     |     |    |         | Associatividade | 
|---------------|-----|-----|----|---------| -----------|
| Mais alta 1️⃣: | `+` | `-` |    |(unário) | dir → esq |
| Média 2️⃣: | `*` | `/` | `%`|         | esq → dir |
| Mais baixa 3️⃣: | `+` | `-` |    |(binário)| esq → dir |

</div>

* 📌 Operadores na mesma linha têm precedência igual

---

<div class='grid'>
<div>

* ✅ **Exemplos de precedências diferentes:**  

* `i + j * k`  → equivale a `i + (j * k)`
* `-i * -j` → equivale a `(-i) * (-j)`
* `+i + j / k` → equivale a `(+i) + (j/k)`

</div>
<div>

* ✅ **Exemplos de precedências iguais:**  

* 📌**Associativdade à esquerda** (resolvem-se da esquerda → direita):

* `i - j - k` → equivale a `(i - j) - k`
* `i * j / k` → equivale a `(i * j) / k`

* 📌**Associativdade à direita** (resolvem-se da direita → equerda):

* `- + i` →  equivale a `- (+i)`
* `+ - i` →  equivale a `+ (-i)`

</div>
</div>

---

#### 🛠️ Modificadores de Precedência  
* 📌 **Parênteses `()` aumentam a precedência de uma operação.**  
* 📌 **Exemplo:**  
* `int x = (1 + 2) * 3; // x = 9`

* 📌 **Uso correcto evita ambiguidades em expressões matemáticas.**  

---


## 🎯 Operadores de Atribuição 🎯  

---

### 📝 O que é um Operador de Atribuição?  
* 📌 **O operador de atribuição** (`=`) é utilizado para armazenar **valores em variáveis**.
* 📌 **Forma geral:**  
* `variável = expressão;`

* 📌 **Exemplos:**  
* `int i = 5;   // 🟢 i recebe 5`
* `float f = 3.14; // 🟢 f recebe 3.14`

* 📌 **Atribuições podem envolver expressões:**  

<div data-marpit-fragment>

```c
int x = 10, y = 20;
int z = x + y;  // 🟢 z recebe 30
```

</div>

---

### 🔄 Conversão Implícita na Atribuição  
* 📌 A conversão ocorre automaticamente.

* 📌 **Exemplos:**  

<div data-marpit-fragment>

```c
int i;
float f;
```
</div>
<div data-marpit-fragment>

```c
i = 72.99f; // ⚠️ i recebe 72 (parte decimal truncada)
f = 136; // 🟢 f recebe 136.0
```
</div>

* 📌 **Atenção à perda de precisão!**  

---

### 🎭 Efeito Colateral da Atribuição  
* 📌 A atribuição **modifica** a variável do lado esquerdo do operador - efeito colateral.  
* 📌 **Exemplo:**  
* `int i = 0; // 🔄 Modificação direta`

* 📌 No entanto, a atribuição continua a ser um operador, por isso a sua avaliação **retorna o valor da variável após a atribuição.**  

<div data-marpit-fragment>

```c
int x;
int y = (x = 10); // 🟢 y recebe 10
```
</div>

---
### 🔗 Atribuições Encadeadas  

<div class='grid'>
<div>

* 📌 Podemos encadear várias atribuições. 

<div data-marpit-fragment>

```c
int i, j, k;
i = j = k = 0;  // 🔄 Todas as variáveis recebem 0
```

</div>

* 📌 O operador de **atribuição** (`=`) é **associativo à direita.**  
* 📌 **Equivalente a:**  

* `i = (j = (k = 0));`

</div>
<div>

* 📌*A execução ocorre da **direita** para a **esquerda:**  
* 🔄 `k` recebe `0`
* 🔄 `j` recebe o valor de `k`
* 🔄 `i` recebe o valor de `j`

</div>
</div>

---

### 🏷️ Lvalue 

* ✅ Operando do lado esquerdo do operador.  
* ✅ Em C é **obrigatório** ser um **objeto armazenado na memória**, i.e. uma variável.  

<div data-marpit-fragment>

```c
int a;
a = 10; // 🟢 'a' é um lvalue válido
```

</div>

<div data-marpit-fragment>

```c
int a;
10 = a; // ❌ 10 é um lvalue inválido
```

</div>

---

### 🛠️ Operadores de Atribuição Composta  
* 📌 **Atribuições compostas permitem simplificar expressões.**  
* 📌 **Forma geral:**  
* `variável operador= expressão;`

* 📌 **Equivalente a:**  
* `variável = variável operador expressão;`

* 📌 **Exemplo:**  

<div data-marpit-fragment>

```c
int x = 10;
x += 5; // 🟢 Equivalente a x = x + 5;
```

</div>

---

#### 🔥 Principais Operadores de Atribuição Composta  
* 📌 **Lista dos operadores mais comuns:**  
* ✅ `+=` (Soma e atribuição)
* ✅ `-=` (Subtração e atribuição) 
* ✅ `*=` (Multiplicação e atribuição)  
* ✅ `/=` (Divisão e atribuição)  
* ✅ `%=` (Módulo e atribuição)  

* 📌 **Exemplos:**  

<div data-marpit-fragment>

```c
int x = 10;
x *= 2; // 🟢 x agora é 20
x /= 4; // 🟢 x agora é 5
```

</div>

---

## 📈 Operadores de Incremento e Decremento 📉  

---

### 🔄 O que são os operadores `++` e `--`?  
* 📌 **Operadores unários utilizados para aumentar ou diminuir o valor de uma variável.**  
* 📌 **Forma geral:**  

<div data-marpit-fragment>

```c
variável++; // Pós-incremento (incrementa depois)
variável--; // Pós-decremento (decrementa depois)
```

</div>
<div data-marpit-fragment>

```c
++variável; // Pré-incremento (incrementa antes)
--variável; // Pré-decremento (decrementa antes)
```

</div>


---

### 🎭 Diferença entre Pré e Pós  
* 📌 **Pré-Incremento (`++x`) e Pré-Decremento (`--x`)**
* ✅ A variável é modificada **antes** de ser usada na expressão.  

<div data-marpit-fragment>

```c
int x = 5;
int y = ++x; // 🟢 x agora é 6, y também recebe 6
```

</div>

* 📌 **Pós-Incremento (`x++`) e Pós-Decremento (`x--`)**
* ✅ A variável é usada na expressão e só **depois** é modificada. 

<div data-marpit-fragment>

```c
int x = 5;
int y = x++; // 🟢 y recebe 5, x agora é 6
```

</div>

---

### 🔄 Exemplo de Uso  

```c
int i = 1;
printf("i = %d\n", ++i); // 🟢 Imprime "i = 2"
printf("i = %d\n", i++); // 🟢 Imprime "i = 2", mas i agora é 3
```
* 📌 O pré-incremento altera `i` **antes** da impressão.
* 📌 O pós-incremento altera `i` **depois** da impressão.

---

### 🔢 Precedência e Associatividade  
* 📌 **O `++` e `--` têm precedência maior que operadores aritméticos.**  
* 📌 **O pré-incremento tem associatividade da direita para a esquerda.**  
* 📌 **O pós-incremento tem associatividade da esquerda para a direita.**  

<div data-marpit-fragment>

```c
int a = 2, b = 3, c;
c = ++a + b++; // 🟢 a = 3, b = 4, c = 6
```

</div>

---

### 📝 Exercício: Qual será a saída?  
```c
int i = 1, j = 2, k;
k = ++i + j++;
printf("i = %d, j = %d, k = %d\n", i, j, k);
```
📌 **O que será impresso?**  
(A) `i = 1, j = 3, k = 3`  
(B) `i = 2, j = 3, k = 4`  
(C) `i = 2, j = 2, k = 4`  
(D) `i = 2, j = 3, k = 5`  

🔎 **Tenta resolver e depois experimenta o código!**  

---

## 🔍 Operadores Relacionais 
* 📌 **Usados para comparar valores e determinar relações entre eles.**  
* 📌 **Retornam `1` (verdadeiro) ou `0` (falso).**  

<div class='grid'>
<div>

<div data-marpit-fragment>

| Operador | Significado |
|----------|-------------|
| `<`  | Menor que |
| `>`  | Maior que |
| `<=` | Menor ou igual |
| `>=` | Maior ou igual |

</div>

</div>
<div>

<div data-marpit-fragment>

```c
int a = 5, b = 10;
if (a < b) {
    printf("a é menor que b\n");
}
```
</div>


</div>
</div>

---

## ⚖️ Operadores de Igualdade  
* 📌 **Usados para verificar igualdade ou diferença entre valores.**  
* 📌 **Diferentes dos operadores de atribuição!**  

<div class='grid'>
<div>

<div data-marpit-fragment>

| Operador | Significado |
|----------|-------------|
| `==` | Igual a |
| `!=` | Diferente de |

</div>

</div>
<div>

```c
int x = 5, y = 10;
if (x != y) {
    printf("x é diferente de y\n");
}
```

</div>
</div>
</div>

<div data-marpit-fragment>

⚠️ **Erro comum:** Usar `=` no lugar de `==`!  
```c
if (x = y) { // ❌ ERRO: Atribuição em vez de comparação
    printf("Isso sempre será verdadeiro!");
}
```

</div>

---

## 🧠 Operadores Lógicos  
* 📌 **Usados para combinar expressões booleanas.**  
* 📌 **Retornam `1` (verdadeiro) ou `0` (falso).**  
* 📌 **Tabela de Operadores:**  

<div class='grid'>
<div>

<div data-marpit-fragment>

| Operador | Significado |
|----------|-------------|
| `!`  | Negação lógica |
| `&&` | E lógico |
| `\|\|`  | Ou lógico |

</div>
</div>
<div>

<div data-marpit-fragment>

```c
int idade = 20;
if (idade > 18 && idade < 65) {
    printf("Idade está na faixa adulta\n");
}
```

</div>
</div>
</div>

---

### ⚡ Avaliação Curta-Circuito  
* 📌 **Nos operadores `&&` e `||`, o segundo operando só é avaliado se necessário.**  

```c
int x = 0, y = 10;
if (x != 0 && y / x > 2) {  // ❌ ERRO: Divisão por zero
    printf("Expressão válida");
}
```

✅ **Solução:**  
```c
if (x != 0 && (y / x > 2)) {
    printf("Expressão válida");
}
```

---

# 📝 Exercício  
📌 O que será impresso no código abaixo?  
```c
int a = 5, b = 10, c = 15;
if (a < b && b < c) {
    printf("Ordem correta\n");
} else {
    printf("Ordem incorreta\n");
}
```
✅ **Tenta responder antes de executar o código!** 


---

# ❓ Q&A  

💬 **Dúvidas?**  
