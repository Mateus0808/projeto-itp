```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "estrutura.h"  

int main() {
    int limiar = 127;
    char opt[5];
    char nome_arquivo[20];
    Imagem *original, *editada;

    do {

        printf("\n--- Selecione uma opcao abaixo ---\n");
        printf("• open - Abrir arquivo\n");
        printf("• save - Salvar arquivo\n");
        printf("• rot - Rotacinar\n");
        printf("• flp - Espelhar\n");
        printf("• gry - Tons de Cinza\n");
        printf("• blu - Bluring\n");
        printf("• sha - Sharpening\n");
        printf("• amp - Aumentar Escala\n");
        printf("• red - Reduzir Escala\n");
        printf("• thr - Thresholding (binarizacao - Preto e Branco)\n");
        printf("• exit - Sair do programa\n");

        scanf("%s", opt);

        opt[strcspn(opt, "\n")] = 0;

        if(!strcmp(opt,"open")) {
            printf("\n");
            printf("Qual o nome do arquivo: ");
            scanf("%s", nome_arquivo);
            original = abrirArquivo(strcat(nome_arquivo, ".ppm"));

        } else if(!strcmp(opt,"save")) {
            printf("\n");
            if(original != NULL) {
                printf("Informe o nome para salvar o arquivo: ");
                scanf("%s", nome_arquivo);
                printf("\n%d %d", editada->larg, editada->alt);
                salvarArquivo(original, nome_arquivo);
            } else {
                printf("Abra um arquivo primeiro.\n");
                continue;
            }
        } else if(!strcmp(opt, "rot")) {
        printf("\n------- ROTACIONAR -------\n");
        char direcao[4];
        printf("• esq - Esquerda\n• dir - Direita\n");
        scanf("%s", direcao);

        direcao[strcspn(direcao, "\n")] = 0;
        printf("%d %d", original->larg, original->alt);
        editada = rotacionar(original, direcao);
        original = editada;
        printf("%d %d", original->larg, original->alt);


    } else if(!strcmp(opt, "flp")) {
        printf("\n------- ESPELHAR -------\n");
        char sentido[4];
        printf("• ver - Vertical\n• hor - Horizontal\n");
        scanf("%s", sentido);
        printf("sentido: %s", sentido);

        sentido[strcspn(sentido, "\n")] = 0;

        if(!strcmp(sentido, "ver")) {
            editada = inverterVerticalmente(original);
            original = editada;
        } else if(!strcmp(sentido, "hor")) {
            editada = inverterHorizontalmente(original);
            original = editada;
        } else {
            printf("\nOpcao invalida.");
            continue;
        }    
    } else if(!strcmp(opt, "gry")) {
        printf("\n------- TONS DE CINZA -------\n");
        editada = escalaCinza(original);
        original = editada;

    } else if(!strcmp(opt, "blu")) {
        printf("\n------- BLURING -------\n");
        editada = blur(original);
        original = editada;

    } else if(!strcmp(opt, "sha")) {
        printf("\n------- SHARPENING -------\n");
        editada = sharp(original);
        original = editada;

    } else if(!strcmp(opt, "amp")) {
        printf("\n------- AUMENTAR ESCALA -------\n");
        editada = aumentar(original);
        original = editada;

    } else if(!strcmp(opt, "red")) {
        printf("\n------- REDUZIR ESCALA -------\n");
        editada = reduzir(original);
        original = editada;

    } else if(!strcmp(opt, "thr")) {
        printf("\n------- THRESHOLDING -------\n");
        int limiar = 127;
        do {
            printf("\nInforme o valor da limiar desejado (Ex: 127): ");
            scanf("%d", &limiar);
        } while (limiar < 0 && 255 > limiar);

        editada = binarizar(original, limiar);
        original = editada;

    } else {
            printf("\nOpcao invalida!\n");
        }  

    } while (strcmp(opt, "exit"));

  return 1;
}
```
