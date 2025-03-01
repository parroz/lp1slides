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
- **Funções úteis** para manipular tudo isso

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

```c
int players[50];
double energy[50];
```
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

* `int var[5] = {10, 15};`

<small>

| indice | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| conteudo | 10 | 15 | 0 | 0| 0 |

</small>

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

<div class='grid'>
<div>

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

</div>
<div>

* 🤔🤔Então, como é que sabemos o tamanho do vector dentro da função?

* **R: temos** de passar um argumento extra com o tamanho do vector:

<div data-marpit-fragment>

```c
void mostrar(int golpes[], int tamanho) {...}
```

</div>


⛔ **Problema**: `sizeof(golpes)` dentro da função NÃO devolve o tamanho correto! 😱


</div>


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

# 📝 Strings: Cadeias de Caracteres

- Uma string é um **vector de `char`** terminado com `\0`.
- Algumas formas de declarar strings:

```c
char nome[10] = "Rocky";
char nome[] = { 'R', 'o', 'c', 'k', 'y', '\0' };
char *nome = "Rocky"; // Ponteiro para string
```

💡 **Lembra-te**: Se não houver `\0`, **o C não sabe** onde a string termina! 🚨

---

# ⛔ Problemas comuns com Strings

### ❌ Erro 1: Atribuição inválida
```c
char nome[10];
nome = "Bruce Lee"; // ❌ NÃO PODES FAZER ISTO!
```
Usa `strcpy`:
```c
strcpy(nome, "Bruce Lee"); // ✅ Correto!
```

### ❌ Erro 2: Comparação errada
```c
if (nome == "Bruce Lee") // ❌ NÃO FAZ O QUE PENSA!
```
Usa `strcmp`:
```c
if (strcmp(nome, "Bruce Lee") == 0) // ✅ Correto!
```

---

# 🔥 Funções úteis para Strings (`string.h`)

```c
strcpy(destino, origem);  // Copia strings
strcat(nome, apelido);    // Concatena strings
strlen(nome);             // Retorna o tamanho
strcmp(a, b);             // Compara strings
```

📌 **Dica**: Usa `strncmp(a, b, n)` para comparar apenas `n` caracteres!

---

# 📊 Matrizes: Vectores de Vectores

- Uma matriz é um **vector de vectores**.
- Em C, declaramos assim:

```c
int socos[2][3] = { 
    {100, 120, 110}, // Linha 0
    {90,  130, 105}  // Linha 1
};
```

📌 **Dica**: A primeira dimensão é **linhas**, a segunda é **colunas**.

---

# 🔄 Percorrer Matrizes

```c
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        printf("Soco[%d][%d]: %d\n", i, j, socos[i][j]);
    }
}
```

💡 **Dica**: Para melhor eficiência, percorre **linha a linha**!

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

# 🚀 Exercício Rápido

Qual é a saída do seguinte código?
```c
char s[] = "Use_the_force_Luke";
s[11] = '\0';
printf("%s\n", s);
```

a) `Use_the_force_Luke`
b) `Use_the_for`
c) `Use_the_fo`
d) `Use_the_force`

e) Nenhuma das anteriores

_(Resposta no próximo slide!)_

---

# ✅ Resposta

A saída é **b) `Use_the_for`** 🎯

Explicação:
- `s[11] = '\0';` corta a string após **`Use_the_for`**.
- O resto da memória **ainda contém os caracteres antigos**, mas a string **termina no `\0`!**

---

# 🎯 Recapitulando

✅ Vectores são **listas de elementos** do mesmo tipo.
✅ Strings são **vectores de `char`** terminados em `\0`.
✅ Matrizes são **vectores de vectores**.
✅ `string.h` tem funções úteis como `strcpy`, `strlen`, `strcmp`.
✅ Cuidado com comparações (`==` NÃO funciona com strings!).

🎉 **Parabéns, chegaste ao fim!** 🚀




---

## ❓  Quizz

<br>
<br>

![w:200 center](socrative.png)




---

# ❓ Q&A  

💬 **Dúvidas?**  
