# Atividades para Casa – Capítulo 8

## Atividade 1 – Reescrevendo código sem `goto`
Você recebeu o seguinte pseudocódigo, escrito de forma semelhante ao estilo das primeiras versões do Fortran, utilizando `goto`:

```text
i := 1
goto check

loop:
    print(i)
    i := i + 1

check:
    if (i <= 10) then
        goto loop
```

**Tarefas:**
1. Reescreva o código acima utilizando um laço de repetição pré-teste (`while`) em uma linguagem de sua escolha (C, Java, Python, etc.).

```c
#include <stdio.h>

int main() {
    int i = 1;
    while (i <= 10) {
        printf("%d\n", i);
        i = i + 1;
    }
    return 0;
}
```

2. Reescreva novamente utilizando um laço de repetição controlado por contador (`for`).

```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 10; i++) {
        printf("%d\n", i);
    }
    return 0;
}
```

3. Compare os três códigos (original com `goto`, versão com `while` e versão com `for`) e escreva um pequeno parágrafo discutindo qual forma é mais legível e por quê.

- **Resposta:** O código com goto funciona, mas é confuso porque a gente precisa ficar acompanhando os saltos. O while já mostra melhor que a repetição acontece enquanto a condição for verdadeira. O for é o mais simples nesse caso, porque mostra de cara onde a variável começa, até onde vai e como aumenta. Por isso, o for é o mais fácil de entender e ler.

---

## Atividade 2 – Seleção múltipla em diferentes linguagens
Muitos programas oferecem menus interativos. Suponha que você precisa implementar um menu com as seguintes opções:

1. Calcular o quadrado de um número.
2. Calcular o fatorial de um número.
3. Sair do programa.

**Tarefas:**
1. Implemente esse menu em **C** utilizando `switch/case`.

```c
#include <stdio.h>

int main() {
    int opcao, numero;
    printf("Escolha: 1 - Quadrado, 2 - Fatorial, 3 - Sair\n");
    scanf("%d", &opcao);
    switch (opcao) {
        case 1:
            printf("Digite um numero: ");
            scanf("%d", &numero);
            printf("Quadrado: %d\n", numero * numero);
            break;
        case 2:
            printf("Digite um numero: ");
            scanf("%d", &numero);
            long long fat = 1;
            for (int i = 1; i <= numero; i++) {
                fat *= i;
            }
            printf("Fatorial: %lld\n", fat);
            break;
        case 3:
            printf("Saindo...\n");
            break;
        default:
            printf("Opcao invalida!\n");
    }
    return 0;
}
```

2. Implemente o mesmo menu em **Python**, utilizando apenas `if/elif/else`.

```python
opcao = int(input("Escolha: 1 - Quadrado, 2 - Fatorial, 3 - Sair\n"))
if opcao == 1:
    numero = int(input("Digite um numero: "))
    print(f"Quadrado: {numero * numero}")
elif opcao == 2:
    numero = int(input("Digite um numero: "))
    fat = 1
    for i in range(1, numero + 1):
        fat *= i
    print(f"Fatorial: {fat}")
elif opcao == 3:
    print("Saindo...")
else:
    print("Opcao invalida!")
```

3. Execute os dois programas e compare as soluções em relação à clareza e quantidade de código.

- **Resposta:** Ambos funcionam bem. O C com switch é mais direto para opções numéricas e tem menos linhas condicionais. O Python com if/elif é mais simples de ler, mas pode ficar longo com mais opções. O C é mais claro para menus, com menos código repetido.

4. Escreva um comentário final destacando em qual linguagem foi mais simples de implementar e justificar o motivo.

- **Resposta:** Mais simples em Python, porque a sintaxe é limpa e não precisa de includes ou breaks, facilitando protótipos rápidos.

---

## Atividade 3 – Explorando alternativas ao `goto`
Historicamente, o `goto` foi usado para resolver diferentes tipos de desvio. Hoje, a maioria das linguagens fornece alternativas como `break`, `continue` e `return`.

**Tarefas:**
1. Escreva um programa que percorra uma lista de números inteiros e:
   - Pare imediatamente a execução ao encontrar o número 0 (`break`).
   - Pule os números negativos sem processá-los (`continue`).
   - Retorne o dobro do primeiro número par encontrado (`return`).

```python
def processar_lista(lista):
    for num in lista:
        if num == 0:
            print("Encontrado 0 - Parando.")
            break
        if num < 0:
            print(f"Pulando negativo: {num}")
            continue
        print(f"Processando: {num}")
        if num % 2 == 0:
            return num * 2
    return None

numeros = [1, -2, 4, -5, 6, 0, 8]
resultado = processar_lista(numeros)
print(f"Resultado: {resultado}")
```

2. Comente sobre como seria a implementação desse mesmo programa utilizando apenas `goto` e rótulos, destacando as vantagens da abordagem moderna.

- **Resposta:** Com goto, usaria rótulos para loop, checks e saltos, tornando o código bagunçado e duro de seguir. A moderna é melhor porque é estruturada, fácil de depurar e evita erros com fluxos claros.
