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

<div data-marpit-fragment>

```c
int aula = 4;
printf("\aAula #%d\n", aula++ * 2 / 2);
```

</div>

### 💬 Message of the Day 
_“Anyone who attempts to generate random numbers by deterministic means is, of course, living in a state of sin.”_
— John von Neumann

---

# John von Neumann (1903–1957)

* Inventor da arquitectura Von-Neumann que se tornou standard em processadores modernos. Tinha apenas uma memória tanto para dados como para código. 
* Contribuiu para a teoria dos jogos.
* Teve um papel importante no projecto Manhattan (bomba atómica)


---


# 🥊 Conteúdo

## 🛠️ O que vamos ver hoje?
- **Vectores**: Como guardar vários valores do mesmo tipo
- **Strings**: Cadeias de caracteres terminadas em `\0`
- **Matrizes**: Tabelas de valores (vectores de vectores)

---
<div class='grid'>
<div>

# 🎯 Vectores (Arrays)

* Um vector é um conjunto de elementos do **mesmo tipo**.
* Ocupam **posições contíguas** na memória.
* Índices começam em **0**! 🚨

<div data-marpit-fragment>

```c
char socos[5] = {100, 120, 90, 130, 110};
printf("Soco mais forte: %d\n", socos[3]); // 130
```
</div>

* 📌 A tabela exemplifica o modelo de memória. Os Endereços são definidos no momento em que o programa corre.


</div>
<div>

<div data-marpit-fragment>

<sub>Modelo da memória RAM:</sub>

<small>

| Endereço | Conteudo | Identificador |
|------|------|-----------|
| 1024 | 100  |`socos[0]` |
| 1025 | 120  |`socos[1]` |
| 1026 | 90   |`socos[2]` |
| 1027 | 130  |`socos[3]` |
| 1028 | 110  |`socos[4]` |
|      | 1024 |`socos`    |
|...   |      |           |

</small>

</div>

* <small>📌 a variável `socos` contém o endereço de memória do elemento `socos[0]` (primeiro elemento do vector) 🤔🤔🤔🤔</small>

</div>
</div>



---
# 🧮 Vectores (Arrays)

* 📍 **Declaração de vectores**

* `tipo nome_do_vector[nr_de_elementos];`

* 🖌️ o tipo pode ser qualquer um dos tipos que já conhecemos: `char`, `int`, `float`, `double`, `enum`.
* 🖍️ pode ainda ser precedido dos qualificadores: `long`, `short`, `signed`, `unsigned`.
* 🖋️ Também podem ser de tipos criados por nós (vamos ver mais à frente)

* **Exemplos:**

<div class='grid'>
<div>

<div data-marpit-fragment>

```c
int players[50];
double energy[50];
```

</div>

</div>
<div>

<div data-marpit-fragment>

```c
#define DIM 100
char letters[DIM];
unsigned short ids[2*DIM+2];
```

</div>

</div>
</div>

---

# 🧮 Inicialização automática de vectores


* **Apenas** pode ser feita no momento da **declaração**. É possível inicializar automaticamente todos os elementos de um vector

* `int var[5] = {10, 15, 18, 20, 25};`


* **Apenas** no momento da declaração, o número de elementos pode ser omitido:

* `int var[] = {10, 15, 18, 20, 25};`

* O compilador percebe qual o tamanho necessário para o vector, neste caso 5.

---

# 🧮 Inicialização automática de vectores


* 💡 Se indicarmos o **número de elementos**, mas **não inicializarmos todos**, os restantes são inicializados automaticamente com o valor **0**.

<div class='grid'><div>

* `int var[5] = {10, 15};`

</div><div>

<div data-marpit-fragment>

<small>

| indice | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| `var` | 10 | 15 | 0 | 0| 0 |

</small>

</div>

</div></div>

<br>


* 💡 **Dica**: Para inicializar tudo com `0`, faz `int golpes[10] = {0};`

---

# 🔄 Percorrer um Vector

<div class='grid'>
<div>

```c
#define DIM 5
int golpes[DIM] = {50, 100, 20, 80, 15};
```

<div data-marpit-fragment>

<small>

| indice | conteúdo | variável |
|---|---|---|
| 0 | 50 | `golpes[0]` |
| 1 | 100 | `golpes[1]`|
| 2 | 20 | `golpes[2]`|
| 3 | 80 | `golpes[3]`|
| 4 | 15 | `golpes[4]`|

</small>

</div>

* <small>São indexados a partir da posição 0, até à posição n-1 (sendo n o número de elementos).</small>

</div>
<div>

* Usamos um **ciclo `for`** para iterar pelos elementos:

<div data-marpit-fragment>

```c
for (int i = 0; i < DIM; i++)
{
    printf("Golpes[%d]: %d\n", i, golpes[i]);
}
```

</div>
</div>

---
# 🚀 Funções com Vectores

* 📌 Em C **não interessa** a **dimensão** do vector que é passado como argumento de uma função. Apenas o seu tipo de dados.

<div class='grid'><div>

<div data-marpit-fragment>

```c
void mostrar(int golpes[10]) {...}
```
</div>

* equivale a:

<div data-marpit-fragment>

```c
void mostrar(int golpes[20]) {...}
```

</div>

* equivale a:

<div data-marpit-fragment>

```c
void mostrar(int golpes[]) {...}
```

</div>

</div><div>

* 🤔🤔Então, como é que sabemos o tamanho do vector dentro da função?

* **R: temos** de passar um argumento extra com o tamanho do vector:

<div data-marpit-fragment>

```c
void mostrar(int golpes[], int tamanho) {...}
```

</div>


* ⛔ **Problema**: `sizeof(golpes)` dentro da função NÃO devolve o tamanho correto! 😱


</div></div>

---

# 🚀 Funções com Vectores (exemplo)

<div data-marpit-fragment>

```c
#include <stdio.h>
#define DIM 5

void mostrar(int golpes[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        printf("Golpe %d: %d\n", i, golpes[i]);
    }
}
```

</div>

<div data-marpit-fragment>

```c
int main()
{
  int golpes[DIM] = {80, 95, 110, 120, 100};
  mostrar(socos, DIM);
  return 0;
}
```

</div>

---

# 🔄 Vetores como Parâmetros de Função

* 📌 **Em C, os vetores são passados por referência para funções.**
* 📌 **Isso significa que qualquer alteração dentro da função afeta o vetor original.**

* ✅ **Exemplo: Modificando um vetor dentro de uma função**

<div class='grid'><div>

<div data-marpit-fragment>

```c
#include <stdio.h>

void modificar(int v[], int tamanho) {
  for (int i = 0; i < tamanho; i++) {
    v[i] *= 2; // Dobra cada elemento
  }
}
```

</div>

</div><div>

<div data-marpit-fragment>

```c
int main() {
  int valores[] = {1, 2, 3, 4, 5};
  int n = 5;

  modificar(valores, n);

  for (int i = 0; i < n; i++) {
    printf("%d ", valores[i]); // Imprime: 2 4 6 8 10
  }
  return 0;
}
```

</div>

</div></div>

✅ **O vetor `valores` foi modificado dentro da função `modificar()`!**

---

# ⚠️ Vetores vs. Variáveis Comuns

* 📌 **Comparação entre variáveis comuns e vetores passados para funções:**

<div class='grid'><div>


* ✅ **Variável comum (cópia, não afeta a original):**
   
<div data-marpit-fragment>

```c
void alterar(int x) {
  x = 10;
}

int main() {
  int a = 5;
  alterar(a);
  printf("%d\n", a); // Imprime 5 (valor não alterado)
}
```

</div>

</div><div>

* ✅ **Vetor (modifica o original, pois é passado por referência):**

```c
void alterarVetor(int v[]) {
  v[0] = 99;
}

int main() {
  int arr[] = {1, 2, 3};
  alterarVetor(arr);
  printf("%d\n", arr[0]); // Imprime 99 (valor foi alterado)
}
```

</div>

</div></div>

* ⚠️ **Vetores são sempre passados como referência, enquanto variáveis comuns são passadas por valor.**  

---

## 📏 **VLAs (Variable Length Arrays) em C**

* São **vectores com tamanho variável determinado em tempo de execução**.
* Introduzidos no **C99**, mas **removidos no C++ e desaconselhados no C11**.

* ⛔️⛔️ **A sua utilização é proíbida nesta disciplina**

* ✅ **Exemplo de um VLA:**

<div class='grid'><div>

<div data-marpit-fragment>

```c
#include <stdio.h>

void criarVetor(int n) {
  int v[n];  // VLA (tamanho definido em tempo de execução)
  for (int i = 0; i < n; i++) {
    v[i] = i * 2;
    printf("%d ", v[i]);
  }
}
```

</div>

<small>

⚠️ **O tamanho do vetor `v[n]` só é conhecido em tempo de execução.**

</small>

</div><div>

<div data-marpit-fragment>

```c
int main() {
  int tamanho;
  printf("Digite um tamanho: ");
  scanf("%d", &tamanho);

  criarVetor(tamanho);
  return 0;
}
```

</div>

</div></div>



---

# ❌ **Por que evitar VLAs?**

* ❌ **Sem alocação dinâmica eficiente:** Usa **stack**, o que pode causar **stack overflow**.  
❌ **Baixa portabilidade:** Não é suportado por todos os compiladores C.  
❌ **C11 tornou o suporte opcional:** Muitos compiladores como **MSVC** não aceitam VLAs.  
❌ **Impossível verificar o tamanho em tempo de compilação**.

✅ Veremos **Alternativas** mais à frente.

---

## ⚠️ Retorno de Vectores em Funções ⚠️

* 📌 **Vectores criados dentro de uma função não podem ser retornados.**
* 📌 **A memória do vector local é desalocada ao sair da função!**

```c
int* criarArray()
{
  int asneira_suprema[5] = {1, 2, 3, 4, 5};

  return asneira_suprema; // ❌ ERRO: Retorna memória inválida
}
```


✅ **Solução:** existe, mas vamos ver mais à frente...

---

## 📏 O Operador `sizeof`

* 📌 **Usado para obter o tamanho (em bytes) de um tipo ou variável.**
* 📌 **Retorna um valor do tipo `size_t`.** (basicamente é um inteiro)
* 📌 **Sintaxe:**

<div data-marpit-fragment>

```c
sizeof(tipo)
sizeof(variável)
```

</div>

---

### 📏 O Operador `sizeof`: Como Funciona?

<div data-marpit-fragment>

```c
   int a;
   printf("Tamanho de int: %lu bytes\n", sizeof(int));
   printf("Tamanho de a: %lu bytes\n", sizeof(a));
```

</div>

* ✅ Ambas as chamadas retornam o tamanho de um `int`, mas a primeira usa o nome do tipo e a segunda usa uma variável.

---

### 📊 Tamanhos Comuns de Tipos Primitivos

| Tipo        | Tamanho (pode variar) |
|------------|---------------------|
| `char`     | 1 byte               |
| `int`      | 4 bytes              |
| `float`    | 4 bytes              |
| `double`   | 8 bytes              |
| `long`     | 4 ou 8 bytes         |
| `short`    | 2 bytes              |

⚠️ **Os tamanhos podem variar dependendo do sistema e compilador!**

---

### 🔄 `sizeof` com Vectores

```c
int vector[10];

printf("Tamanho do vector: %lu bytes\n", sizeof(vector));

printf("Tamanho de um elemento: %lu bytes\n", sizeof(vector[0]));

printf("Número de elementos: %lu\n", sizeof(vector) / sizeof(vector[0]));
```

* ✅ `sizeof(vector)` retorna o tamanho total do array em bytes.  
* ✅ Para obter o número de elementos, dividimos pelo tamanho de um único elemento.

---

### ⚠️ `sizeof` em Vectores dentro de Funções

<small>

* 📌 **Não é possível obter o tamanho real do vetor passado como argumento para uma função.** ❌



```c
void tamanhoArray(int v[]) {
  printf("Tamanho dentro da função: %lu bytes\n", sizeof(v));
}

int main() {
  int arr[10];
  printf("Tamanho no main: %lu bytes\n", sizeof(arr));
  tamanhoArray(arr);
  return 0;
}
```



* ✅ No `main()`, `sizeof(arr)` retorna o tamanho correto.  
* ❌ Dentro da função, `sizeof(arr)` retorna o tamanho de um ponteiro, **não do vector** 😱😱😭.

</small>

---

## ❓  Quizz - Vectores

<br>

![w:200 center](socrative.png)


<br>


- No campo nome devem colocar o **número de aluno** 2XXXXXXX.


---



# 🗞️ Strings - cadeias de caracteres

---

# 📜 Cadeias de Caracteres (Strings) em C

* Strings em C são **vetores de caracteres** terminados pelo caractere especial `\0` (caractere nulo).
* Devemos sempre reservar espaço para o caractere `\0` ao declarar uma string.

```c
char nome[10]; // Permite até 9 caracteres + '\0'
```

---

# 📌 Declaração e Inicialização de Strings

```c
char nome[20] = "oscar";
  
char nome[20] = {'o','s','c','a','r', '\0'};
  
char nome[] = "oscar";  // O compilador define o tamanho automaticamente. Incluindo espaço para o \0
  
char *nome = "oscar";
```

⚠️ O `\0` deve ser sempre considerado, pois indica o fim da string.

---

# ❌ O que **não** podemos fazer com strings em C

```c
char nome[10];
nome = "Alberto Caeiro";  // ❌ ERRO! Strings não podem ser atribuídas diretamente
```

```c
if (nome == "Alberto Caeiro") {  // ❌ ERRO! Não se pode comparar strings com ==
  puts("asneira suprema");
}
```

* ✅ **Correção:** Use funções da biblioteca `<string.h>`.

---

# 📦 Operações com Strings (`<string.h>`)

* **Cópia de Strings**

```c
strcpy(nome, "Alberto");
```

* **Concatenação de Strings**

```c
strcat(nome, " Caeiro");
```

* **Comparação de Strings**

```c
if (strcmp(nome, "Alberto Caeiro") == 0)
  puts("sou um guardador de rebanhos");
```

* `strcpy` retorna 0 se as strings forem iguais

---

# 🏷️ Comprimento de uma String

```c
int n = strlen(nome);

printf("A string tem %d caracteres", n);
```

* ⚠️ `strlen()` retorna apenas o número de caracteres **antes** do `\0`.

---

# ⚙️ Implementação de `strcat`

```c
char *strcat(char s1[], char s2[]) {
  int ls1 = strlen(s1);
  int ls2 = strlen(s2);

  for (int i = ls1, j = 0; j <= ls2; i++, j++)
    s1[i] = s2[j];

  return s1;
}
```

* ✅ Concatena `s2` ao final de `s1`.
* ✅ O `\0` da `s2` é copiado para `s1`.

---

# 📢 Exercícios - Válido ou Inválido?

```c
char palavra[100];
palavra = "TRUE"; // ❌ Inválido! Use strcpy()

if (palavra == "TRUE") // ❌ Inválido! Use strcmp()
  puts("It is TRUE!");
```

✅ **Correção:**

```c
strcpy(palavra, "TRUE");

if (strcmp(palavra, "TRUE") == 0)
  puts("It is TRUE!");
```

---

# 📢 Exercício - O que será impresso?

<div class='grid'>
<div>


```c
#include <stdio.h>
#define MAX 64
void func(char s[], int n) {
  puts(s);
  s[n] = '\0';
  puts(s);
}

int main(void) {
  char s[MAX] = "Use_the_force_Luke";
  func(s, 11);
  return 0;
}
```

</div>
<div>

<small>

(A) `Use_the_force_Luke\n`  `Use_the_for\n`  
(B) `Use_the_force_Luke\n`  `Use_the_fo\n`  
(C) `Use_the_force_Luke\n`  `Use_the_forc\n`  
(D) `Use_the_force_Luke\n`  `rce_Luke\n`  
(E) Nenhuma das anteriores

Nota: a função `puts()` imprime a string recebida como parâmetro seguida de um `\n`

</small>

</div>
</div>

---

# ✅ Resposta

A saída é **b) `Use_the_for`** 🎯

Explicação:
- `s[11] = '\0';` corta a string após **`Use_the_for`**.
- O resto da memória **ainda contém os caracteres antigos**, mas a string **termina no `\0`!**


---

# 📌 `printf()` com Strings

```c
printf("%s\n", var);  // Imprime a string normalmente

printf("%10s\n", var); // Alinha à direita com espaço mínimo de 10 caracteres

printf("%-10s\n", var); // Alinha à esquerda

puts(var); // Similar ao printf("%s\n", var)
```

✅ `puts()` sempre adiciona `\n` no final.

---

# 📌 `scanf()` com Strings

```c
scanf("%s", nome);  // Lê até encontrar espaço ou \n
scanf("%5s", nome);  // Lê até 5 caracteres

scanf("%[^\n]s", nome); // Lê até \n

fgets(nome, 128, stdin); // Alternativa segura
```

⚠️ `scanf("%s", nome);` **não usa `&`**

---

# 🎭 Converter para Maiúsculas

```c
#include <ctype.h>
void str_to_upper(char str[]) {
  for (int i = 0 ; str[i] != '\0' ; i++)
    str[i] = toupper(str[i]);
}

int main() {
  char fish[100] = "halibut";
  str_to_upper(fish);
  printf("%s\n", fish); // Imprime "HALIBUT"
}
```

✅ Usa `<ctype.h>` para manipulação de caracteres.

---

# 📝 Implementação de `strcpy`

```c
void str_copy(char dest[], char src[]) {
  int i = 0;
  do {
    dest[i] = src[i];
  } while (src[i++] != '\0');
}
```

✅ Alternativa compacta:

```c
void str_copy(char dest[], char src[]) {
  while ((dest[i] = src[i++]) != '\0');
}
```



---

# 📚 Biblioteca `<string.h>`
## 🔥 Funções úteis para Strings

```c
strcpy(destino, origem);  // Copia strings
strcat(nome, apelido);    // Concatena strings
strlen(nome);             // Retorna o tamanho
strcmp(a, b);             // Compara strings
strcasecmp(s1, s2);       // Compara strings ignorando o 'case'
strncmp(a, b, n)          // comparar apenas `n` caracteres!
```

---

# 🎯 Resumo

✅ Strings em C são vetores terminados em `\0`.  
✅ Use `<string.h>` para manipular strings corretamente.  
✅ **Não** compare strings com `==`, use `strcmp()`.  
✅ `printf()` e `scanf()` têm formatos especiais para strings.  
✅ **Cuidado com buffer overflow** ao lidar com strings!


---

# 📊 Matrizes

---

## 📊 Matrizes: Vectores de Vectores

* Uma **matriz** é um **vetor multidimensional**, i.e. **vector de vectores**
* São declaradas com **duas dimensões ou mais**.

* Em C, declaramos assim:

```c
int socos[2][3] = { 
  {100, 120, 110}, // Linha 0
  {90,  130, 105}  // Linha 1
};
```

📌 **Dica**: A primeira dimensão é **linhas**, a segunda é **colunas**.

---

# 🏗️ Estrutura de Matrizes

* **Primeira dimensão** → Número de **linhas**  
* **Segunda dimensão** → Número de **colunas**  

```c
tipo nome_matriz[num_linhas][num_colunas];
```

✅ Exemplo:

```c
char Galo[3][3]; // Matriz 3x3
Galo[0][0] = 'X';
Galo[0][2] = 'O';
Galo[1][1] = 'X';
Galo[2][2] = 'O';
```

✅ `Galo[2][2]` armazena `'O'`.

---


# 🔄 Percorrer Matrizes

💡 **Dica**: percorre **linha a linha**!

```c
for (int i = 0; i < 2; i++) {
  for (int j = 0; j < 3; j++) {
    printf("Soco[%d][%d]: %d\n", i, j, socos[i][j]);
  }
}
```


---

# 🔥 Matrizes em Funções

```c
void mostrar(int socos[][3], int linhas) {
  for (int i = 0; i < linhas; i++) {
    for (int j = 0; j < 3; j++) {
      printf("%d ", socos[i][j]);
    }
    printf("\n");
  }
}
```

📌 **Dica**: TEMOS de especificar o número de colunas ao passar matrizes para funções! 🚨

---

# 🚀 Inicialização Automática

<div class='grid'>
<div>

* **Podemos inicializar uma matriz no momento da declaração**:

   ```c
   char soup[5][5] = {
       {'f', 'e', 'k', 'u', 'l'},
       {'u', 'o', 'x', 's', 'n'},
       {'t', 'n', 'r', 'e', 'r'},
       {'y', 'h', 'e', 'c', 'j'},
       {'v', 'q', 'e', 'w', 'e'}
   };
   ```

</div>
<div>

✅ **Podemos omitir o número de linhas** (o compilador infere):

   ```c
   char soup[][5] = {
       {'e', 'e', 'k', 'u', 'l'},
       {'u', 'c', 'x', 'q', 'n'},
       {'t', 's', 'r', 'd', 'r'},
       {'y', 'h', 'e', 'o', 'j'},
       {'v', 'q', 'e', 'w', 'f'}
   };
   ```

⚠️ **Não podemos omitir o número de colunas**!

</div>
</div>

---

# 🔍 Acesso a Elementos

* Podemos **acessar e modificar** elementos da matriz:

```c
char soup[5][5];
soup[0][0] = 'e';
soup[0][1] = 'e';
soup[0][2] = 'u';
soup[0][3] = 'l';
soup[1][0] = 'u';
```

✅ Cada elemento é referenciado como `matriz[linha][coluna]`.

---

# ⚠️ Erro Comum: Dimensão Inválida

🚨 O seguinte código **não compila**:

```c
int scores[3][] = {  // ❌ ERRO: Deve especificar o número de colunas
  {'1', '2', '3'},
  {'4', '5', '6'},
  {'7', '8', '9'}
};
```

✅ **Correção:** Sempre defina o número de colunas:

```c
int scores[3][3] = {
  {'1', '2', '3'},
  {'4', '5', '6'},
  {'7', '8', '9'}
};
```

---

# 🎯 Exercício: Qual é o erro?

📌 **O código abaixo não funciona corretamente. Por quê?**

   ```c
   #include <stdio.h>

   int main() {
       int n = 3, i, j;
       int scores[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
       int acc[n]; // Vetor para armazenar a soma das linhas

       for (i = 0; i < 3; i++) {
           for (j = 0; j <= 3; j++) {  // ❌ ERRO
               acc[i] += scores[j][i]; // ❌ ERRO
           }
       }
       return 0;
   }
   ```

✅ **Pense antes de executar!**

---

# 📤 Passagem de Matrizes para Funções

* **Devemos especificar o número de colunas ao passar uma matriz para uma função**:

   ```c
   #define DIM 5
   void inic(char s[][DIM]) {
       s[0][0] = 'e';
       s[0][1] = 'e';
       s[0][2] = 'u';
       s[0][3] = 'l';
   }
   ```

✅ **No `main()`**:

   ```c
   int main(void) {
       char soup[5][5];
       inic(soup);
       return 0;
   }
   ```

---

# 🔄 Percorrendo uma Matriz

✅ **Para percorrer uma matriz, usamos dois loops aninhados**:

   ```c
   for (i = 0; i < 4; i++) {
       for (j = 0; j < 4; j++) {
           printf("%d ", matriz[i][j]);
       }
       printf("\n");
   }
   ```

🔹 **Primeiro loop** percorre as linhas.  
🔹 **Segundo loop** percorre as colunas.

---

# 🔄 Exemplo: Percorrendo e Imprimindo uma Matriz

   ```c
   int main(void) {
       char soup[][5] = {
           {'e', 'e', 'k', 'u', 'l'},
           {'u', 'c', 'x', 'q', 'n'},
           {'t', 's', 'r', 'd', 'r'},
           {'y', 'h', 'e', 'o', 'j'},
           {'v', 'q', 'e', 'w', 'f'}
       };

       for (int i = 0; i < 5; i++) {
           for (int j = 0; j < 5; j++)
               printf("'%c' ", soup[i][j]);
           putchar('\n');
       }
   }
   ```

✅ **Imprime todos os elementos da matriz `soup`**.

---

# 📚 Resumo

✅ **Matrizes são vetores multidimensionais**.  
✅ **Devemos especificar o número de colunas ao declarar uma matriz**.  
✅ **Podemos inicializar uma matriz na declaração**.  
✅ **Para percorrer uma matriz, usamos dois loops aninhados**.  
✅ **Sempre defina o número de colunas ao passar uma matriz para uma função**.

---


## ❓  Quizz

<br>
<br>

![w:200 center](socrative.png)




---

# ❓ Q&A  

💬 **Dúvidas?**  
