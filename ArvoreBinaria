#include <stdio.h>
#include <stdlib.h>

// Estrutura de um nó da árvore
typedef struct no {
    int conteudo;
    struct no *esquerda, *direita;
} No;

// Estrutura da árvore binária
typedef struct {
    No* raiz;
} ArvoreBinaria;

// Função para criar uma árvore vazia
void criarArvore(ArvoreBinaria *arv) {
    arv->raiz = NULL;
}

// Função para inserir um elemento na árvore (sem permitir repetição)
void inserir(No **raiz, int valor) {
    if (*raiz == NULL) {
        // Se a posição estiver vazia, cria um novo nó
        No *novo = (No*)malloc(sizeof(No));
        novo->conteudo = valor;
        novo->esquerda = NULL;
        novo->direita = NULL;
        *raiz = novo;
    } else {
        if (valor == (*raiz)->conteudo) {
            // Caso o valor já exista, não permite a inserção
            printf("Ops... esse valor já está incluído!\n");
            return;
        }
        if (valor < (*raiz)->conteudo)
            inserir(&(*raiz)->esquerda, valor);
        else
            inserir(&(*raiz)->direita, valor);
    }
}

// Função auxiliar para encontrar o menor valor da subárvore direita
No* menorValor(No* no) {
    while (no->esquerda != NULL) {
        no = no->esquerda;
    }
    return no;
}

// Função para remover um elemento da árvore
No* remover(No* raiz, int valor) {
    if (raiz == NULL) {
        printf("Valor não encontrado na árvore!\n");
        return NULL;
    }

    if (valor < raiz->conteudo) {
        // O valor está na subárvore esquerda
        raiz->esquerda = remover(raiz->esquerda, valor);
    } else if (valor > raiz->conteudo) {
        // O valor está na subárvore direita
        raiz->direita = remover(raiz->direita, valor);
    } else {
        // Caso tenha encontrado o valor
        if (raiz->esquerda == NULL) {
            No* temp = raiz->direita;
            free(raiz);
            return temp;
        } else if (raiz->direita == NULL) {
            No* temp = raiz->esquerda;
            free(raiz);
            return temp;
        } else {
            // Nó com dois filhos: substitui pelo menor da subárvore direita
            No* temp = menorValor(raiz->direita);
            raiz->conteudo = temp->conteudo;
            raiz->direita = remover(raiz->direita, temp->conteudo);
        }
    }
    return raiz;
}

// Função para imprimir a árvore em ordem crescente
void imprimirEmOrdem(No *raiz) {
    if (raiz != NULL) {
        imprimirEmOrdem(raiz->esquerda);
        printf("%d ", raiz->conteudo);
        imprimirEmOrdem(raiz->direita);
    }
}

// Função para contar o total de nós da árvore
int contarNos(No* raiz) {
    if (raiz == NULL) return 0;
    return 1 + contarNos(raiz->esquerda) + contarNos(raiz->direita);
}

// Função para contar o total de folhas da árvore
int contarFolhas(No* raiz) {
    if (raiz == NULL) return 0;
    if (raiz->esquerda == NULL && raiz->direita == NULL) return 1;
    return contarFolhas(raiz->esquerda) + contarFolhas(raiz->direita);
}

// Função para calcular a altura da árvore (começando em 0)
int alturaArvore(No* raiz) {
    if (raiz == NULL) return -1; // Árvore vazia tem altura -1 para começar em 0
    int alturaEsquerda = alturaArvore(raiz->esquerda);
    int alturaDireita = alturaArvore(raiz->direita);
    return (alturaEsquerda > alturaDireita ? alturaEsquerda : alturaDireita) + 1;
}

// Função para verificar se a árvore é própria (todo nó tem 0 ou 2 filhos)
int ePropria(No* raiz) {
    if (raiz == NULL) return 1;
    if ((raiz->esquerda == NULL && raiz->direita != NULL) ||
        (raiz->esquerda != NULL && raiz->direita == NULL)) {
        return 0; // Se um nó tem apenas um filho, a árvore é imprópria
    }
    return ePropria(raiz->esquerda) && ePropria(raiz->direita);
}

// Função principal com menu interativo
int main() {
    int op, valor;
    ArvoreBinaria arv;
    criarArvore(&arv);

    do {
        printf("\n0 - Sair\n1 - Inserir\n2 - Imprimir\n3 - Remover\n");
        printf("4 - Contar Nós\n5 - Contar Folhas\n6 - Altura da Árvore\n7 - Verificar se é Própria\n");
        printf("Escolha uma opção: ");
        scanf("%d", &op);

        switch (op) {
            case 0:
                printf("\nSaindo...\n");
                break;
            case 1:
                printf("Digite um valor: ");
                scanf("%d", &valor);
                inserir(&arv.raiz, valor);
                break;
            case 2:
                printf("\nÁrvore em ordem:\n");
                imprimirEmOrdem(arv.raiz);
                printf("\n");
                break;
            case 3:
                printf("Digite o valor a ser removido: ");
                scanf("%d", &valor);
                arv.raiz = remover(arv.raiz, valor);
                break;
            case 4:
                printf("Total de nós: %d\n", contarNos(arv.raiz));
                break;
            case 5:
                printf("Total de folhas: %d\n", contarFolhas(arv.raiz));
                break;
            case 6:
                printf("Altura da árvore: %d\n", alturaArvore(arv.raiz));
                break;
            case 7:
                if (ePropria(arv.raiz))
                    printf("A árvore é própria.\n");
                else
                    printf("A árvore é imprópria.\n");
                break;
            default:
                printf("\nOpção inválida!\n");
        }
    } while (op != 0);

    return 0;
}
