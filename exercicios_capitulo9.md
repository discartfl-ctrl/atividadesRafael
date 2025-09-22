# Exercícios – Capítulo 9: Subprogramas

## Exercício 1 – Passagem de Parâmetros por Valor e por Referência
Considere o seguinte pseudocódigo de uma função que tenta dobrar o valor de um número:

```text
procedure dobrar(x)
    x := x * 2
end
```

**Tarefas:**
1. Implemente esse subprograma em **C** duas vezes:
   - A primeira versão recebendo o parâmetro **por valor**.

```c
#include <stdio.h>

void dobrarPorValor(int x) {
    x = x * 2;
}

int main() {
    int numero = 10;
    printf("Antes por valor: %d\n", numero);
    dobrarPorValor(numero);
    printf("Depois por valor: %d\n", numero);
    return 0;
}
```

   - A segunda versão recebendo o parâmetro **por referência** (usando ponteiros).

```c
#include <stdio.h>

void dobrarPorReferencia(int *x) {
    *x = (*x) * 2;
}

int main() {
    int numero = 10;
    printf("Antes por referencia: %d\n", numero);
    dobrarPorReferencia(&numero);
    printf("Depois por referencia: %d\n", numero);
    return 0;
}
```

2. Escreva um programa principal que:
   - Crie uma variável inteira com valor inicial 10.
   - Chame a função `dobrar` por valor e exiba o resultado.
   - Chame a função `dobrar` por referência e exiba o resultado.

**(Resultados já incluídos nos códigos acima)**  
- Por valor: Antes 10, Depois 10.  
- Por referência: Antes 10, Depois 20.

**Questões:**
- Qual a diferença observada entre as duas versões?
  - **Resposta:** Na versão por valor, o valor original (10) não muda, pois uma cópia é usada. Na versão por referência, o valor original muda para 20, pois o ponteiro altera a variável original.
- Por que o valor da variável só se altera na versão por referência?
  - **Resposta:** Porque por valor cria uma cópia local que não afeta a original, enquanto por referência usa o endereço da variável, modificando-a diretamente.
- Relacione essa diferença com as estratégias de passagem de parâmetros discutidas no Capítulo 9.
  - **Resposta:** Isso reflete a passagem por valor (cópia independente) versus passagem por referência (acesso direto à memória), como explicado no Capítulo 9, onde a escolha afeta o comportamento e a eficiência do programa.

---

## Exercício 2 – Corrotinas em GoLang (primeiro contato)
As **corrotinas** permitem a execução concorrente de rotinas dentro de um programa. Em Go, isso é feito com a palavra-chave `go`.

**Tarefas:**
1. Crie um arquivo chamado `main.go`.
2. Implemente o seguinte programa simples:

```go
package main

import (
    "fmt"
    "time"
)

func escrever(texto string) {
    for i := 0; i < 5; i++ {
        fmt.Println(texto, i)
        time.Sleep(time.Millisecond * 500)
    }
}

func main() {
    go escrever("Corrotina")  // executa em paralelo
    escrever("Função normal") // executa no fluxo principal
}
```

3. Compile e execute o programa com:
   ```bash
   go run main.go
   ```

**Questões:**
- O que acontece com a ordem das mensagens exibidas?
  - **Resposta:** As mensagens se misturam, com "Função normal" aparecendo em sequência e "Corrotina" aparecendo entre elas, dependendo do agendamento do sistema.
- Por que as mensagens da corrotina e da função normal se intercalam?
  - **Resposta:** Porque a corrotina roda em paralelo com a função principal, e o agendador de Go alterna entre elas, afetado pelo Sleep de 500ms.
- Relacione esse comportamento com a definição de **corrotinas** estudada no Capítulo 9.
  - **Resposta:** Isso ilustra corrotinas como rotinas leves que rodam concorrentemente, compartilhando tempo de CPU, conforme definido no Capítulo 9, diferentemente de threads pesadas.
