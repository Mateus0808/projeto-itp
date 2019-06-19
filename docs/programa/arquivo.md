```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include "funcoes.h"  
```
--------------------------------------------------------------------------------
    //funcao pixelImagem() recebe como parametro o objeto IMAGEM que foi criado
    //na funcao abrirArquivo() e os valores de X e Y que informa o endereco do
    //pixel atual que sera criado.    

```
struct Pixel* pixelImagem(Imagem* imagem, int y, int x) {  
        return &(imagem->pixels[y * imagem->larg + x]);  
}
```
--------------------------------------------------------------------------------  

    //Aloca espaco dinamicamente da imagem para o seu total de pixels.  
```
Imagem* novaImagem(int larg, int alt, int maxCor) {  
    Imagem *imagem = (Imagem *) malloc(sizeof(Imagem));  
    imagem->pixels = (struct Pixel *) malloc(larg * alt * sizeof(struct Pixel));  
    imagem->larg = larg;  
    imagem->alt = alt;  
    imagem->maxCor = maxCor;  
    return imagem;  
}
```

--------------------------------------------------------------------------------

    //recebe por parametro ARQUIVO que eh o nome do arquivo que sera
    //aberto verifica se ele existe e se eh do tipo P3 cria a
    //estrutura da nova imagem que sera tratada e copia cada valor
    //rgb de toda a imagem para dentro de cada pixel, no final retorna  
```
Imagem* abrirArquivo(char *arquivo) {

    FILE *arq = fopen(arquivo, "r");
    char formato[6];
    fgets(formato, 6, arq);

    if (arq == NULL) {
        printf("O arquivo nao foi encontrado ou nao existe.\n");
        return NULL;
    }

    int larg, alt, maxCor, x, y;
    Imagem *imagem = NULL;

    if (strcmp("P3\n", formato) == 0) {
        fscanf(arq, "%d %d \n %d \n", &larg, &alt, &maxCor);
        printf("\nArquivo '%s' foi carregado com sucesso.\nTipo: %sLarg: %d\nAlt: %d\nMaxCor: %d\n", arquivo, formato, larg, alt, maxCor);
        imagem = novaImagem(larg, alt, maxCor);
        for (y = 0; y < alt; y++) {
            for (x = 0; x < larg; x++) {
                struct Pixel *p = pixelImagem(imagem, y, x);
                fscanf(arq, "%d %d %d", &(p->r), &(p->g), &(p->b));
            }            
        }
    } else {
        printf("Lamentamos, atualmente so trabalhamos com PPM tipo P3. Tente Novamente!\n");
        return NULL;
    }
    fclose(arq);

    return imagem;
}
```
--------------------------------------------------------------------------------
    //funcao para salvar o novo arquivo  
```
void salvarArquivo(Imagem *imagem, char *nome_arquivo) {

    FILE *arq = fopen(strcat(nome_arquivo, ".ppm"), "wb");
    int x, y;
    printf("\nLarg:%d \nAlt:%d\nmaxCor:%d\nSalvando ...", imagem->larg, imagem->alt, imagem->maxCor);
    fprintf(arq, "P3\n%d %d\n%d", imagem->larg, imagem->alt, imagem->maxCor);
        for (y = 0; y < imagem->alt; y++) {
            for (x = 0; x < imagem->larg; x++) {                
            struct Pixel *p = pixelImagem(imagem, y, x);
            fprintf(arq, "\n%d\n%d\n%d", p->r, p->g, p->b);
        }
    }
    printf("\n");
    fprintf(arq, "\n ");
    fclose(arq);
}
```
