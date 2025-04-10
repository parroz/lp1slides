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
printf("Aula #8\n");
```

---

# 📚 Conteúdo da Aula

## 🧩 Estruturas

* O que são estruturas em C
* `typedef` e simplificação de tipos
* Passagem por valor e referência
* Apontadores para estruturas

## 📂 Ficheiros em C

* Entrada e saída baseadas em **streams** 💧

---

# 🧱 Estruturas em C

* Tipo de dados agregado
* Permite agrupar vários elementos de tipos diferentes 👥
* Cada elemento é chamado **campo**
* Cada campo tem um **nome único** dentro da estrutura

---

# 🧩 Definir uma estrutura

```c
struct player {
    int id;
    char firstname[64];
    char lastname[64];
    float height;
    float weight;
    int score;
};
```

* Definida geralmente **fora das funções**, no topo do ficheiro

---

# 🧍 Declaração de variáveis

```c
struct player player_1, player_2;
struct player players[100];
struct player *ptr_player;
```

* `player_1`, `player_2` são variáveis do tipo `struct player`
* `players` é um vetor de 100 jogadores
* `ptr_player` é um apontador para `struct player`

---

# 🛠️ Declaração direta

```c
struct player {
    int id;
    char firstname[64];
    char lastname[64];
    float height;
    float weight;
    int score;
} player_1, player_2;
```

* Variáveis podem ser criadas **na definição da estrutura**

---

# 🗂️ Onde declarar uma estrutura?

<div class='grid'><div>

* Declara-se geralmente **fora de qualquer função** 🧾
* Normalmente no topo do ficheiro `.c` ou `.h`
* Isso permite que **várias funções** usem o tipo definido ✅

</div><div>

```c
// no topo do ficheiro
struct pessoa {
    char nome[50];
    int idade;
};

int main() {
    struct pessoa p;
    ...
}
```

* Pode-se declarar dentro de uma função, mas o tipo fica **local** a essa função 🚫

</div></div>

---

# 🔍 Acesso aos campos

```c
struct data {
    int dia;
    int mes;
    int ano;
};

struct data fim_de_aulas;
fim_de_aulas.dia = 15;
fim_de_aulas.mes = 6;
fim_de_aulas.ano = 2020;
```

* Usa-se o operador `.` para aceder aos campos

---

# 🧾 Inicialização direta

```c
struct data fim_de_aulas = {15, 6, 2020};
```

* Semelhante à inicialização de vetores
* Segue a **ordem dos campos**

---

# 📏 Tamanho de uma estrutura

* Determinado pela **soma dos tamanhos** dos seus campos
* Pode incluir **preenchimento (padding)** para alinhamento de memória

```c
struct exemplo {
    char letra;    // 1 byte
    int numero;    // 4 bytes
};
```

* Tamanho esperado: 5 bytes
* Tamanho real: geralmente **8 bytes** (3 de padding) 🧠

📌 Usa `sizeof(struct exemplo)` para saber o tamanho real

---

# 🧠 Exemplo

Declare uma estrutura para representar um mês:

📅 Nome, abreviatura, dias e número do mês

<div data-marpit-fragment>

```c
struct mes {
    char nome[16];
    char abreviatura[4];
    unsigned int num_dias;
    unsigned int num_mes;
};
```

</div>

---

# 🏷️ `typedef`

* Permite criar **nomes novos** para tipos existentes

```c
typedef int INTEIRO;
typedef void* PVOID;
typedef struct data DATA;
typedef unsigned char byte;
typedef char bool;
```

---

# 🧪 Exemplo com typedef

```c
DATA natal = {24, 12, 2019};
INTEIRO a = 5;
natal.dia++;
```

* Define-se `DATA` como nome alternativo a `struct data`
* Pode ser feito fora de qualquer função

---

# ✨ `typedef` sem nome da struct

```c
typedef struct {
    int dia;
    int mes;
    int ano;
} DATA;
```

* Ou com nome interno:

```c
typedef struct _data {
    int dia;
    int mes;
    int ano;
} DATA;
```

---

# ⚠️ Erro comum com typedef

```c
typedef struct {
    int dia;
    int mes;
    int ano;
} DATA fim_de_aulas; // ERRO ❌
```

* Não se podem declarar variáveis no `typedef`
* Variáveis têm de ser declaradas **depois**

---

# 🧪 Exemplo correto com typedef

```c
typedef struct {
    int dia;
    int mes;
    int ano;
} DATA;

int main() {
    DATA fim_de_aulas;
    return 0;
}
```

✅ Simples e limpo

---

# 🔁 Retornar estrutura por valor

```c
DATA ask_data(char desc[]) {
    DATA d;
    printf("Data para %s\n", desc);
    scanf("%d %d %d", &d.dia, &d.mes, &d.ano);
    return d;
}
```

```c
int main() {
    DATA hoje = ask_data("hoje");
    DATA fim = ask_data("fim de aulas");
    return 0;
}
```

* A estrutura é **copiada** no retorno
* Muito comum e eficiente em C

---


# ❌ Comparar estruturas diretamente

<div class='grid'><div>

* Não é possível usar `==`, `!=`, `<`, `>` entre estruturas:

```c
DATA d1 = {1,1,2024};
DATA d2 = {1,1,2024};

if (d1 == d2) { // ERRO ❌
    ...
}
```

* O compilador não sabe **como comparar estruturas**

</div><div>

✅ Mas é possível fazer **atribuições**:

```c
DATA d3;
d3 = d1; // OK ✅
```

* Atribuição copia **todos os campos** da estrutura

</div></div>

---

# 🔍 Comparar datas

```c
int compare_dates(DATA a, DATA b) {
    int r = b.ano - a.ano;
    if (r != 0) return r;
    r = b.mes - a.mes;
    if (r != 0) return r;
    return b.dia - a.dia;
}
```

* Passa estruturas **por valor**

---

# 👉 Apontadores para estruturas

```c
DATA hoje;
DATA *d_ptr = &hoje;
```

<div class='grid'><div>

* Forma cássica com o operador desreferencia

```c
(*d_ptr).dia = 1;
(*d_ptr).mes = 1;
(*d_ptr).ano = 2000;
```

</div><div>

* Forma compacta com o operador desreferencia para estruturas `->`

```c
d_ptr->dia = 1;
d_ptr->mes = 1;
d_ptr->ano = 2000;
```


* Usa-se `->` para aceder a campos via ponteiro

</div></div>


---

# 📤 Passar estrutura por referência

```c
void ask_data(DATA *d, char desc[]) {
    printf("Data para %s\n", desc);
    scanf("%d %d %d", &d->dia, &d->mes, &d->ano);
}
```

```c
int main() {
    DATA fim, hoje;
    ask_data(&hoje, "hoje");
    ask_data(&fim, "fim de aulas");
    return 0;
}
```

* Usa apontador como argumento ➡️ sem cópia
* Modifica diretamente as variáveis passadas

---


# 🚫 Retorno inválido de estrutura local

* **Não é seguro** retornar o endereço de uma variável local!

```c
DATA* erro() {
    DATA d = {1, 1, 2024};
    return &d; // ERRO ❌
}
```

* A variável `d` deixa de existir após o fim da função ⚠️
* O ponteiro retornado aponta para uma área de memória **inválida** 🧨

✅ Soluções corretas:
* Retornar por valor

---

## ❓  Quizz - Estruturas

<br>

![w:200 center](socrative.png)


<br>


- No campo nome devem colocar o **número de aluno** 2XXXXXXX.


---

# 📂 Ficheiros em C

---

# 💡 O que é um stream?

* Um fluxo contínuo de bytes
* Comunicação entre programa e:
  * Ficheiros
  * Dispositivos
  * Processos
* Independente do dispositivo (device-independent)

---

# 📥 Streams por omissão

* `stdin` → entrada padrão (teclado)
* `stdout` → saída padrão (ecrã)
* `stderr` → saída de erro padrão

```c
printf("Olá mundo!\n");
fprintf(stdout, "Olá mundo!\n");
scanf("%d", &x);
fscanf(stdin, "%d", &x);
```

---

# 📑 Operações com ficheiros

* Abertura do ficheiro 📂
* Leitura / escrita ✍️
* Fecho do ficheiro 🔒

```c
FILE *fp;
fp = fopen("dados.txt", "r");
if (fp == NULL) {
    fprintf(stderr, "Erro ao abrir o ficheiro\n");
}
```

---

# 🔓 Modos de abertura (texto)

| Modo | Significado | Comportamento |
|------|-------------|----------------|
| "r"   | Read        | Abre para leitura. Erro se não existir. |
| "w"   | Write       | Cria novo ficheiro ou apaga existente. |
| "a"   | Append      | Abre para escrever no fim. Cria se não existir. |
| "r+"  | Read+Write  | Abre para leitura e escrita. Erro se não existir. |
| "w+"  | Write+Read  | Cria novo para leitura e escrita. Apaga se existir. |
| "a+"  | Append+Read | Lê e escreve no fim. Cria se não existir. |

📦 Acrescentar `b` → modo binário: "rb", "wb+", etc.

---

# 📦 Modos de abertura (binário)

| Modo   | Significado              | Comportamento |
|--------|--------------------------|----------------|
| "rb"   | Ler binário              | Erro se ficheiro não existir |
| "wb"   | Escrever binário         | Cria novo ou apaga ficheiro existente |
| "ab"   | Acrescentar binário      | Cria se não existir, escreve no fim |
| "rb+"  | Ler/Escrever binário     | Abre para leitura e escrita |
| "wb+"  | Escrever/Ler binário     | Cria novo, apaga se existir |
| "ab+"  | Acrescentar/Ler binário  | Cria se não existir, lê e escreve no fim |

🧠 Para ficheiros binários usamos `fread` e `fwrite`

---

# 📝 Escrever ficheiros de texto

```c
FILE *fp = fopen("exemplo.txt", "w");
if (fp != NULL) {
    fprintf(fp, "Olá mundo!\n");
    fclose(fp);
}
```

* `fprintf`, `fputs`, `fputc`

---

# 📖 Ler ficheiros de texto

```c
FILE *fp = fopen("exemplo.txt", "r");
char linha[100];

if (fp != NULL) {
    while (fgets(linha, 100, fp)) {
        printf("%s", linha);
    }
    fclose(fp);
}
```

* `fscanf`, `fgets`, `fgetc`

---

# 📦 Ficheiros binários: escrita

```c
int v[5] = {1,2,3,4,5};
FILE *fp = fopen("dados.bin", "wb");

if (fp != NULL) {
    fwrite(v, sizeof(int), 5, fp);
    fclose(fp);
}
```

* Usa-se `fwrite`

---

# 📦 Ficheiros binários: leitura

```c
int v[5];
FILE *fp = fopen("dados.bin", "rb");

if (fp != NULL) {
    fread(v, sizeof(int), 5, fp);
    fclose(fp);
}
```

* Usa-se `fread`

---

# 🧹 Fechar ficheiros

```c
fclose(fp);
```

* Garante que os dados são escritos fisicamente em disco
* Liberta o ficheiro para outros programas

---

# 🔧 Outras funções úteis

```c
int feof(FILE *fp);     // fim do ficheiro
int ferror(FILE *fp);   // erro no ficheiro
int fflush(FILE *fp);   // forçar escrita do buffer
void rewind(FILE *fp);  // cursor para o início
long ftell(FILE *fp);   // posição atual
int fseek(FILE *fp, long offset, int origem); // reposicionar
```

---

# 📊 Exemplo completo

```c
FILE *fp = fopen("input.txt", "r");
char palavra[64];
int n_palavras = 0, max_len = 0;

while (fscanf(fp, "%s", palavra) != EOF) {
    int len = strlen(palavra);
    if (len > 0) {
        n_palavras++;
        if (len > max_len) max_len = len;
    }
}

fclose(fp);
printf("Total: %d, Maior: %d\n", n_palavras, max_len);
```

---

# 🧠 Conclusão

* Usa `fopen` para abrir ficheiros
* Lê com `fgets`, `fscanf`, `fread`
* Escreve com `fprintf`, `fputs`, `fwrite`
* Fecha sempre com `fclose`

📁 Trabalhar com ficheiros permite guardar e reutilizar dados de forma persistente!


---
# 🧠 Conclusão

* Estruturas permitem agrupar dados
* `typedef` simplifica o uso
* Podem ser passadas por valor ou por referência
* Suportam inicialização, cópia e comparação

🚀 Usa estruturas para organizar melhor o teu código!




---

# ❓ Q&A  

💬 **Dúvidas?**  
