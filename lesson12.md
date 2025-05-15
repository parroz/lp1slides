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
int aula = 11;
printf("\aAula #%d\n", aula + (aula & 1 ? 2 : 1));
```

</div>


---

## ❓  Quizz

<br>
<br>

![w:200 center](socrative.png)



---

# O Pré-Processador em C 🛠️

Antes de compilar o código, o **pré-processador** realiza várias transformações:
- Inclui ficheiros
- Substitui macros
- Condiciona blocos de código

Estas transformações **não são C**, mas instruções para o pré-processador!

---

# Diretivas mais comuns 📋

| Diretiva      | Função                                 |
|---------------|-----------------------------------------|
| `#include`    | Insere o conteúdo de outro ficheiro     |
| `#define`     | Define uma macro                        |
| `#undef`      | Anula uma macro                         |
| `#ifdef`      | Se a macro estiver definida             |
| `#ifndef`     | Se a macro **não** estiver definida     |
| `#endif`      | Fecha `#if`, `#ifdef`, `#ifndef`        |

---

# Exemplo com `#include` 📥

~~~c
#include <stdio.h>   // Biblioteca do sistema
#include "minha.h"   // Ficheiro criado por nós
~~~

- Aspas `"` → procura no diretório atual
- Sinais `<>` → procura nas bibliotecas do sistema

---

# Evitar inclusões duplicadas 🔁

Usamos **guardas de inclusão**:

~~~c
#ifndef __MINHA_H__
#define __MINHA_H__

// conteúdo do header

#endif
~~~

✅ Garante que o código só é incluído **uma vez**, mesmo que `#include` seja repetido

---

# Organizar código em vários ficheiros 🧩

Separar o código ajuda a:
- Reutilizar funções
- Dividir responsabilidades
- Compilar partes separadas

---

# Organização típica de ficheiros 📁

```
main.c         → função principal
funcoes.h      → declarações de funções
funcoes.c      → implementações das funções
```

---

# Exemplo `funcoes.h` 📘

~~~c
#ifndef FUNCOES_H
#define FUNCOES_H

void ola();
int soma(int a, int b);

#endif
~~~

---

# Exemplo `funcoes.c` ⚙️

~~~c
#include <stdio.h>
#include "funcoes.h"

void ola() {
    printf("Olá mundo!\n");
}

int soma(int a, int b) {
    return a + b;
}
~~~

---

# Exemplo `main.c` 🧠

~~~c
#include <stdio.h>
#include "funcoes.h"

int main() {
    ola();
    printf("3 + 4 = %d\n", soma(3, 4));
    return 0;
}
~~~

---

# Compilar vários ficheiros 🧱

Usar o `gcc` com todos os `.c`:

```bash
gcc main.c funcoes.c -o programa
```

🎯 Compila e junta tudo num único executável

---

# Compilação em duas fases ⚙️➡️🔗

1. Compilar separadamente:
```bash
gcc -c funcoes.c -o funcoes.o
gcc -c main.c -o main.o
```

2. Ligar:
```bash
gcc main.o funcoes.o -o programa
```

💡 Permite recompilar apenas ficheiros modificados

---

# Makefile (bónus) 🧩

Um `Makefile` automatiza a compilação:

~~~make
programa: main.o funcoes.o
	gcc main.o funcoes.o -o programa

main.o: main.c funcoes.h
	gcc -c main.c

funcoes.o: funcoes.c funcoes.h
	gcc -c funcoes.c

clean:
	rm -f *.o programa
~~~

🔁 Usa `make` para compilar tudo, e `make clean` para limpar

---

# Exercício 🧪

1. Cria os ficheiros:
   - `main.c`
   - `matematica.c`
   - `matematica.h`

2. Em `matematica.h`, declara:
   - `int quadrado(int x);`

3. Em `matematica.c`, implementa a função:
   - retorna o quadrado de um número

4. Em `main.c`, usa a função com `printf`

5. Compila e testa!

---

# Conclusão 📦

✅ O pré-processador é essencial no pipeline de compilação  
✅ Permite usar macros, condicionar código e importar headers  
✅ Organizar código em vários ficheiros melhora a clareza e manutenção  
✅ Usa `make` para automatizar tudo 🔄

---

## ❓  Quizz - Macros

<br>

![w:200 center](socrative.png)


<br>


- No campo nome devem colocar o **número de aluno** 2XXXXXXX.

---

# ❓ Q&A  

💬 **Dúvidas?**  
