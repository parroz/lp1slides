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
printf("\aAula #4 - Instruções de Controlo\n");
```

</div>

### 💬 Message of the Day 
*“Talk is cheap. Show me the code.”*
*“Software is like sex: it’s better when it’s free.”*
*“A computer is like air conditioning - it becomes useless when you open Windows.”*
*“Excusing bad programming is a shooting offence, no matter what the circumstances.”*
— Linus Torvalds

---

# 🎓 Linus Torvalds (1969–)
* Criador do Linux, o sistema operativo open source mais usado no mundo
* Criou o Git, sistema de versionamento que revolucionou o desenvolvimento de software

---

## 🎯 Conteúdo

* Instruções de Selecção
* 1. `if`, `else`, `else if` ✅
* 2. `switch` 🔄
* 3. Operador ternário ❓

* Estruturas de Repetição
* 1. `while`, `do while`, `for` 🔁
* 2. `break` e `continue` ⏭️

* Funções e scope de variáveis 🌀

---

## 🔀 Instruções de Controlo de Fluxo
* Alteram a execução sequencial de um programa
* Instruções condicionais (`if`, `else`, `switch`)
* Ciclos (`while`, `for`, `do-while`)

---


## 🔍 Instrução `if`

Permite executar um bloco de código apenas se uma condição for verdadeira. ✅

<div class='grid'>
<div>

```c
int x = 10;

if (x <= 10) {
    printf("X é menor ou igual a 10\n");
}
```

</div>
<div>

```c
desconto = 0;

if (idade >= 16 && idade <= 25) // desconto jovem
    desconto += 10;

desconto += 5; // desconto para todos

printf("O seu desconto e: %d\n", desconto);
```

</div>
</div>

---

### 🧐 Uso opcional de `{}`
* Em C, se um bloco de código contém apenas uma instrução, as `{}` podem ser omitidas!

<div class='grid'>
<div>

<div data-marpit-fragment>

```c
int x = 10;
if (x > 5)
    printf("X é maior que 5\n"); // Sem chaves!
```

</div>

* 📌 **Isso vale para:**
* `if`, `else`, `else if`
* `while`, `for`, `do while`

</div>
<div>

* 🚨 **Mas cuidado!**
* _Se adicionar uma segunda instrução, o comportamento pode mudar inesperadamente:_

<div data-marpit-fragment>

```c
if (x > 5)
    printf("X é maior que 5\n");
    printf("Esta linha será sempre executada!\n"); // Fora do if!
```

</div>

</div>
</div>

* 💡 **Melhor prática:** Sempre usar `{}` para evitar ambiguidades!


---


## 🔀 Instrução `if-else`
* A cláusula `else` é opcional e executada se a condição for falsa. ❌

<div data-marpit-fragment>

```c
int nota = 5;
if (nota >= 10) {
    printf("Aprovado\n");
} else {
    printf("Reprovado\n"); // executa este bloco se a condição for falsa
}
```

</div>

---

## 🔂 Instrução `if-else if`
* Permite testar múltiplas condições. 📊

<div class='grid'>
<div>


```c
int idade = 18;

if (idade < 5) {
    printf("Isento\n");
} else if (idade < 18) {
    printf("Tarifa criança\n");
} else if (idade < 65) {
    printf("Tarifa normal\n");
} else {
    printf("Tarifa sénior\n");
}
```

</div>
<div>

<div data-marpit-fragment>

❓**Qual será a saída se `idade = 65`?**
- (A) "Tarifa criança"
- (B) "Tarifa normal"
- (C) "Tarifa sénior"
- (D) Nenhuma saída


</div>

</div>
</div>

---
## 🔗 Instruções `if` Aninhadas
* Como funciona um `if` dentro de outro `if`?

<div data-marpit-fragment>

```c
if (condição1) {
    if (condição2) {
        // código executado se ambas forem verdadeiras
    }
}
```

</div>

* ✅ Pode ser substituído por um `&&`:

<div data-marpit-fragment>


```c
if (condição1 && condição2) {
    // código executado se ambas forem verdadeiras
}
```

</div>

* 🛠️ **Usar `&&` pode tornar o código mais limpo e direto!**


---

## ❔ Operador Ternário
* Uma alternativa curta ao `if-else`. ✨

<div data-marpit-fragment>

```c
exp1 ? exp2 : exp3
```

</div>

* 1. `exp1` é avaliada
* 2. se for verdadeira, devolve `exp2`
* 3. se for falsa, devolve `exp3`

<div data-marpit-fragment>

```c
int a = 5, b = 10;
int maior = (a > b) ? a : b;
printf("Maior: %d\n", maior);
```

</div>

* ✅ Simples e eficaz para expressões curtas.


---

## ❔ Operador Ternário (exemplos)

<div class='grid'>
<div>
<div data-marpit-fragment>

```c
int x = 5, y;

y = x > 6 ? 7 : 8;
```

</div>


<div data-marpit-fragment>

```c
int x = 9, y;

y = x > 6 ? 7 : 8
```

</div>

</div>
<div>

<div data-marpit-fragment>

```c
x = (a == b) ? 0 : (a > b) ? a : b;
```

</div>

* **Qual o valor de `x` quando:**
* 1. `a = 5` e `b = 10`
* 2. `a = 7` e `b = 7`
* 3. `a = -4` e `b = -10`

* R: `10`, `0`, `-4`

</div>
</div>




---

## 🔄 Instrução `switch`

*Avalia uma expressão e compara com os `case` disponíveis. ⚖️

<div class='grid'>
<div>

<div data-marpit-fragment>

```c
int x = 2;
switch (x) {
    case 0:
        printf("Zero\n");
        break;
    case 1:
        printf("Um\n");
        break;
    case 2:
        printf("Dois\n");
        break;
    default: // default funciona como o else
        printf("Outro valor\n");
}
```

</div>

</div>
<div>

* ✅ Apenas valores inteiros (`int`, `char`) podem ser testados.
* 🚨 **Sem `break`, a execução continua para o próximo `case`!**



---

## 🔄 Instrução `switch` (cont)

* Escreva uma função que recebe um character e retorna 0 se for consoante, 1 se for vogal

<div class='grid'>
<div>

<div data-marpit-fragment>

```c
#include <ctype.h>
// para podermos usar a funcao tolower()

int isVowel(char c) {
    switch(tolower(c)) {
        case 'a':
        case 'e':
        case 'i':
        case 'o':
        case 'u':
            return 1;
    }
    return 0;
}
```

</div>

</div>
<div>

<div data-marpit-fragment>

```c
int isVowel(char c) {
    char lower_c = tolower(c);
    if (lower_c == 'a' || lower_c == 'e' || 
        lower_c == 'i' || lower_c == 'o' || 
        lower_c == 'u')
        return 1;
		 
		 
    return 0;
}
```

</div>

</div>
</div>


---

## ❓  Quizz Instruções de Seleccão

<br>
<br>

![w:200 center](socrative.png)


---


## 🔁 Estruturas de Repetição: `while`
* Executa enquanto a condição for verdadeira.

<div data-marpit-fragment>

```c
int num = 0;
while (num < 5) {
    printf("%d\n", num);
    num++;
}
```
</div>

✅ Útil quando o número de iterações não é conhecido previamente.

---

## 🔄 Estruturas de Repetição: `do-while`
* Garante pelo menos uma execução antes da condição ser verificada.

<div class='grid'>
<div>

<div data-marpit-fragment>

```c
int num, r = 0;

do {
    puts("insira um numero inteiro positivo");
    r = scanf ("%d", &num);
} while (r != 1 || num < 0);

printf("Valor valido lido: %d\n", num);
```
</div>

* ✅ Útil para validação de inputs do utilizador.

</div>
<div>

* neste exemplo, o ciclo só repete se o utilizador não introduzir um número inteiro, ou se introduzir um número negativo.

<div data-marpit-fragment>

```bash
insira um numero inteiro positivo
-10
insira um numero inteiro positivo
5
Valor valido lido: 5
```

</div>
</div>
</div>




---

## 🔂 Estruturas de Repetição: `for`
* Ideal para loops com contagem definida.

<div data-marpit-fragment>

```c
for (i = 0; i < 5; i++) {
    printf("%d\n", i);
}
```

</div>

* ✅ Possui inicialização, condição e atualização no cabeçalho.


---

* A inicialização e atualização podem ter várias instruções, desde que separadas por `,`.

<div data-marpit-fragment>

```c
int notas[10], i, j;
double media;


for (i = 0, media = 0, j = 1 ; i < 10 ; i++, j++)
{
    media += notas[i];
}

media /= i;
```

</div>

* Inicializacao, condição e actualização do `for` são opcionais:
<div class='grid'>
<div>

<div data-marpit-fragment>

```c
for (; i < 10 ;)
    media += notas[i++];
```

</div>

</div>
<div>

<div data-marpit-fragment>

```c
for (;;) // ciclo infinito
    printf("EU VOU APRENDER A USAR O FOR\n");
```

</div>

</div>
</div>

---
## Instruções de Controlo de Ciclo ⏹️ ⏭️ 
* ✅ Úteis para controlo avançado de loops.

* `break`: Sai imediatamente do loop/switch. ⏹️

<div data-marpit-fragment>

```c
for (int i = 1; i <= 5; i++) {
    if (i == 3) break; // imprime os números até encontrar o 3
    printf("%d\n", i);
}
```

</div>

* `continue`: Salta para a próxima iteração. ⏭️

<div data-marpit-fragment>

```c
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue; // imprime os números até 5, mas não imprime o 3
    printf("%d\n", i);
}
```

</div>

---

## ❓  Quizz Estruturas de Repetição

<br>
<br>

![w:200 center](socrative.png)


---
# Funções e Scope de Variáveis

## 🏗️ Invocação de Funções
* Chamamos a função pelo seu nome, passando argumentos.

<div data-marpit-fragment>

```c
int maior = max(10, 20);
printf("Maior: %d\n", maior);
```

</div>

* 📌 O programa **pausa** a execução da função chamadora e só continua após o `return` da função invocada!

---

## 🔁 Passagem de Parâmetros
* ✅ Parâmetros podem ser **passados por valor**, ou seja, cópias dos valores originais.

<div data-marpit-fragment>

```c
void altera(int x) {
    x = 50;
}
    
int main() {
    int num = 10;
    altera(num);
    printf("Num: %d\n", num); // Saída: 10
    return 0;
}
```

</div>

* 🚨 **Atenção:** O valor de `num` **não é alterado** na função `altera`!

---

## 🌍 Escopo de Variáveis
### Variáveis Globais
* Definidas **fora** de qualquer função, acessíveis por todo o programa.

<div data-marpit-fragment>

```c
int global = 10;
void funcao() {
    printf("Global: %d\n", global);
}
```

</div>

* ✅ São úteis, mas devem ser **evitadas** para manter o código modular!
* ⛔️ Nesta UC não serão permitidas variáveis globais

---

### Variáveis Locais
* Definidas **dentro** de uma função, existem apenas no seu scope. A variável existe e é visível **apenas** dentro da **função** depois de ser declarada e só **enquanto** a função estiver a **ser executada**.

<div data-marpit-fragment>


```c
void funcao() {
    int local = 20;
    printf("Local: %d\n", local);
}
```
</div>


* 🚨 **Fora da função, a variável `local` não existe!**

---

### 🔎 Variáveis Locais (cont.)

* os parâmetros de uma função são também variáveis locais

<div data-marpit-fragment>


```c
int mediana(int a, int b, int c) 
{
    // a, b, c são variáveis locais
    return (a > b) ? ((b > c) ? b : (a > c) ? c : a)
                   : ((a > c) ? a : (b > c) ? c : b);
}
```


</div>

---

## 🔍 Variáveis Estáticas
* ✅ **Variáveis `static`** mantêm o valor entre chamadas da função.

```c
void contador() {
    static int count = 0;
    count++;
    printf("Contagem: %d\n", count);
}
    
int main() {
    contador(); // Contagem: 1
    contador(); // Contagem: 2
    return 0;
}
```

* 🚀 **`static` é útil para preservar estado dentro de funções!**


---

## ❓  Quizz - Funções e Variáveis

<br>
<br>

![w:200 center](socrative.png)



---

# ❓ Q&A  

💬 **Dúvidas?**  
