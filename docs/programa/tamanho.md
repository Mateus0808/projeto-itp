```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include "funcoes.h"  
```
--------------------------------------------------------------------------------
    //funcao para aumentar escala da imagem, pegando um pixel e
    //aumentando o mesmo para quatro pixel  
```
Imagem* aumentar(Imagem *original) {
    printf("Aplicando a mascara...\n");
    int x, y, x1, y1, x2, y2, x3, y3, x4, y4;
    int h = original->alt , w = original->larg;

    Imagem *imgBig = novaImagem(w*2, h*2, original->maxCor);
    for (y = 0; y < h; y++) {
        for (x = 0; x < w; x++) {
            struct Pixel *p1 = pixelImagem(original, y, x);

            y1 = y*2;   x1 = x*2;
            y2 = y*2+1; x2 = x*2;
            y3 = y*2;   x3 = x*2+1;
            y4 = y*2+1; x4 = x*2+1;

            struct Pixel *p2_1 = pixelImagem(imgBig, y1, x1);
            struct Pixel *p2_2 = pixelImagem(imgBig, y2, x2);
            struct Pixel *p2_3 = pixelImagem(imgBig, y3, x3);
            struct Pixel *p2_4 = pixelImagem(imgBig, y4, x4);

            p2_1->r = p2_2->r = p2_3->r = p2_4->r = p1->r;
            p2_1->g = p2_2->g = p2_3->g = p2_4->g = p1->g;
            p2_1->b = p2_2->b = p2_3->b = p2_4->b = p1->b;  

        }

    }
    return imgBig;
}
```
--------------------------------------------------------------------------------
    //funcao para aumentar escala da imagem, pegando um pixel e
    //aumentando o mesmo para quatro pixel  
```
Imagem* reduzir(Imagem *original) {
    printf("Aplicando a mascara...\n");
    int x, y, i=0, j=0;
    int h = original->alt , w = original->larg;
    int width = ceil((float)w/2), height = ceil((float)h/2);
    Imagem *imgSmall = novaImagem(width, height, original->maxCor);
    for (y = 0; y < h; y+=2) {
        i = 0;
        for (x = 0; x < w; x+=2) {
            struct Pixel *p1 = pixelImagem(original, y, x);
            struct Pixel *p2 = pixelImagem(imgSmall, j, i);

            p2->r = p1->r;
            p2->g = p1->g;
            p2->b = p1->b;  
            i+=1;
        }
        j+=1;
    }
    return imgSmall;
}
```
