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

# 🎯 Vectores (Arrays)

- Um vector é um conjunto de elementos do **mesmo tipo**.
- Ocupam **posições contíguas** na memória.
- Índices começam em **0**! 🚨

```c
int socos[5] = {100, 120, 90, 130, 110};
printf("Soco mais forte: %d\n", socos[3]); // 130
```

💡 **Dica**: Para inicializar tudo com `0`, faz `int golpes[10] = {0};`!

---

# 🔄 Percorrer um Vector

Usamos um **ciclo `for`** para iterar pelos elementos:

```c
for (int i = 0; i < 5; i++) {
    printf("Soco %d: %d\n", i + 1, socos[i]);
}
```

📌 **Curiosidade**: Como os elementos são **contíguos**, podes usar **aritmética de ponteiros** para percorrer o array!

---

# 🚀 Funções com Vectores

Passamos vectores para funções **sem precisar de especificar o tamanho**:

```c
void mostrar(int golpes[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        printf("Golpe %d: %d\n", i, golpes[i]);
    }
}
```

**Chamada**:
```c
int socos[5] = {80, 95, 110, 120, 100};
mostrar(socos, 5);
```

⛔ **Problema**: `sizeof(golpes)` dentro da função NÃO devolve o tamanho correto! 😱

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
