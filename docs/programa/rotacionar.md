```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include "funcoes.h"  
```
--------------------------------------------------------------------------------
    //funcao para rotacionar a direita e a esquerda  
```
Imagem* rotacionar(Imagem *original, char* direcao) {
    printf("Aplicando a mascara...\n");
    int x, y, i, j;
    int h = original->alt, w = original->larg;

    Imagem *imgRotacionada = novaImagem(h, w, original->maxCor);
    for (x = 0; x < w; x++) {
        for (y = 0; y < h; y++) {
            struct Pixel *p1 = pixelImagem(original, y, x);
            if(!strcmp(direcao, "dir")) {
                i = x; j = h-y-1;
            } else {
                i = w-x-1; j = y;
            }
            struct Pixel *p2 = pixelImagem(imgRotacionada, i, j);

            p2->r = p1->r;
            p2->g = p1->g;
            p2->b = p1->b;
        }
    }
    return imgRotacionada;
}
```
--------------------------------------------------------------------------------
    //funcao para inverter horizontalmente  
```
Imagem* inverterHorizontalmente(Imagem *original) {
    printf("Aplicando a mascara...\n");
    int x, y;
    int h = original->alt, w = original->larg;
    Imagem *imgInvertidaHorizontal = novaImagem(w, h, original->maxCor);
    for (y = h-1; y >= 0; y--) {
        for (x = 0; x < w; x++) {
            struct Pixel *p1 = pixelImagem(original, y, x);
            struct Pixel *p2 = pixelImagem(imgInvertidaHorizontal, h-y-1, x);
            p2->r = p1->r;
            p2->g = p1->g;
            p2->b = p1->b;
        }
    }
    return imgInvertidaHorizontal;
}
```
--------------------------------------------------------------------------------
    //funcao para inverter verticalmente  
```
Imagem* inverterVerticalmente(Imagem *original) {
    printf("Aplicando a mascara...\n");
    int x, y;
    int h = original->alt, w = original->larg;
    Imagem *imgInvertidaVertical = novaImagem(w, h, original->maxCor);
    for (x = 0; x < w; x++) {
        for (y = 0; y < h; y++) {
            struct Pixel *p1 = pixelImagem(original, y, x);
            struct Pixel *p2 = pixelImagem(imgInvertidaVertical, y, w-x-1);
            p2->r = p1->r;
            p2->g = p1->g;
            p2->b = p1->b;
        }
    }
    return imgInvertidaVertical;
}
```
