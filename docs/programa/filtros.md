```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include "funcoes.h"  
```
--------------------------------------------------------------------------------  

    //funcao para aumentar a escala da imagem, pegando um pixel e aumentando o mesmo para quatro  
    //pixel

```
Imagem* sharp(Imagem *original) {    
        printf("Aplicando a mascara...\n");  
        int x, y;  
        int x1, y1, x2, y2, x3, y3, x4, y4, x5, y5, x6, y6, x7, y7, x8, y8, x9, y9;  
        int kernel[3][3] = {  
          { 0, -1,  0},  
          {-1,  5, -1},  
          { 0, -1,  0}  
        };

        int h = original->alt , w = original->larg;  
        Imagem *imgBlur = novaImagem(w, h, original->maxCor);  

        for (y = 1; y < h-1; y++) {  
          for (x = 1; x < w-1; x++) {  
              y1 = y-1;   x1 = x-1;  
              y2 = y-1;   x2 = x;  
              y3 = y-1;   x3 = x+1;  
              y4 = y;     x4 = x-1;  
              y5 = y;     x5 = x; // central  
              y6 = y;     x6 = x+1;  
              y7 = y+1;   x7 = x-1;  
              y8 = y+1;   x8 = x;  
              y9 = y+1;   x9 = x+1;  

            struct Pixel *p1 = pixelImagem(original, y1, x1);  
            struct Pixel *p2 = pixelImagem(original, y2, x2);  
            struct Pixel *p3 = pixelImagem(original, y3, x3);  
            struct Pixel *p4 = pixelImagem(original, y4, x4);  
            struct Pixel *p5 = pixelImagem(original, y5, x5); //central  
            struct Pixel *p6 = pixelImagem(original, y6, x6);  
            struct Pixel *p7 = pixelImagem(original, y7, x7);  
            struct Pixel *p8 = pixelImagem(original, y8, x8);  
            struct Pixel *p9 = pixelImagem(original, y9, x9);  

            struct Pixel *p = pixelImagem(imgBlur, y, x);  

            p->r =  
            p1->r * kernel[0][0] + p2->r * kernel[0][1] + p3->r * kernel[0][2] +  
            p4->r * kernel[1][0] + p5->r * kernel[1][1] + p6->r * kernel[1][2] +  
            p7->r * kernel[2][0] + p8->r * kernel[2][1] + p9->r * kernel[2][2];  

            p->g =  
            p1->g * kernel[0][0] + p2->g * kernel[0][1] + p3->g * kernel[0][2] +  
            p4->g * kernel[1][0] + p5->g * kernel[1][1] + p6->g * kernel[1][2] +  
            p7->g * kernel[2][0] + p8->g * kernel[2][1] + p9->g * kernel[2][2];  

            p->b =  
            p1->b * kernel[0][0] + p2->b * kernel[0][1] + p3->b * kernel[0][2] +  
            p4->b * kernel[1][0] + p5->b * kernel[1][1] + p6->b * kernel[1][2] +  
            p7->b * kernel[2][0] + p8->b * kernel[2][1] + p9->b * kernel[2][2];  
          }
      }
      return imgBlur;
}
```
--------------------------------------------------------------------------------  

    //funcao para aumentar escala da imagem, pegando um pixel e
    //aumentando o mesmo para quatro pixel  

```
Imagem* blur(Imagem *original) {  
    printf("Aplicando a mascara...\n");  
    int x, y;  
    int x1, y1, x2, y2, x3, y3, x4, y4, x5, y5, x6, y6, x7, y7, x8, y8, x9, y9;  
    double kernelBlur = 0.111111;  
    int h = original->alt , w = original->larg;  

    Imagem *imgBlur = novaImagem(w, h, original->maxCor);  

    imgBlur = original;  

    for (y = 1; y < h-1; y++) {  
        for (x = 1; x < w-1; x++) {  

            y1 = y-1;   x1 = x-1;  
            y2 = y-1;   x2 = x;  
            y3 = y-1;   x3 = x+1;
            y4 = y;     x4 = x-1;
            y5 = y;     x5 = x; // central
            y6 = y;     x6 = x+1;
            y7 = y+1;   x7 = x-1;
            y8 = y+1;   x8 = x;
            y9 = y+1;   x9 = x+1;

            struct Pixel *p1 = pixelImagem(original, y1, x1);
            struct Pixel *p2 = pixelImagem(original, y2, x2);
            struct Pixel *p3 = pixelImagem(original, y3, x3);
            struct Pixel *p4 = pixelImagem(original, y4, x4);
            struct Pixel *p5 = pixelImagem(original, y5, x5);
            struct Pixel *p6 = pixelImagem(original, y6, x6);
            struct Pixel *p7 = pixelImagem(original, y7, x7);
            struct Pixel *p8 = pixelImagem(original, y8, x8);
            struct Pixel *p9 = pixelImagem(original, y9, x9);

            struct Pixel *p = pixelImagem(imgBlur, y, x);

            p->r =
            (int)(p1->r * kernelBlur) + (int)(p2->r * kernelBlur) + (int)(p3->r * kernelBlur) +
            (int)(p4->r * kernelBlur) + (int)(p5->r * kernelBlur) + (int)(p6->r * kernelBlur) +
            (int)(p7->r * kernelBlur) + (int)(p8->r * kernelBlur) + (int)(p9->r * kernelBlur);


            p->g =
            (int)(p1->g * kernelBlur) + (int)(p2->g * kernelBlur) + (int)(p3->g * kernelBlur) +
            (int)(p4->g * kernelBlur) + (int)(p5->g * kernelBlur) + (int)(p6->g * kernelBlur) +
            (int)(p7->g * kernelBlur) + (int)(p8->g * kernelBlur) + (int)(p9->g * kernelBlur);

            p->b =
            (int)(p1->b * kernelBlur) + (int)(p2->b * kernelBlur) + (int)(p3->b * kernelBlur) +
            (int)(p4->b * kernelBlur) + (int)(p5->b * kernelBlur) + (int)(p6->b * kernelBlur) +
            (int)(p7->b * kernelBlur) + (int)(p8->b * kernelBlur) + (int)(p9->b * kernelBlur);

        }
    }
    return imgBlur;
}
```

--------------------------------------------------------------------------------
    //funcao para binarizar imagem, utilizando metodo aonde compara o valor
    //limiar com a escala de cinza, se a escala de cinza for menor que o limiar
    //o valor eh 0 (preto) se for maior eh branco (255)
```
Imagem* binarizar(Imagem *original, int limiar) {
    printf("Aplicando a mascara...\n");
    int x, y, gray;
    int h = original->alt, w = original->larg;
    Imagem *imgBinarizada = novaImagem(w, h, original->maxCor);

    for (y = 0; y < h; y++) {
        for (x = 0; x < w; x++) {
            struct Pixel *p1 = pixelImagem(original, y, x);
            struct Pixel *p2 = pixelImagem(imgBinarizada, y, x);

            gray = p1->r*0.3+p1->g*0.59+p1->b*0.11;

            if(gray < limiar) {
                p2->r = p2->g = p2->b = 0;
            } else {
                p2->r = p2->g = p2->b = 255;
            }
        }
    }
    return imgBinarizada;
}
```
--------------------------------------------------------------------------------
    //funcao para colocar em cinza, metodo soma rgb/3
--------------------------------------------------------------------------------  
```
Imagem* escalaCinza(Imagem *original) {
    printf("Aplicando a mascara...\n");
    int x, y, gray;
    int h = original->alt, w = original->larg;
    Imagem *imgCinza = novaImagem(w, h, original->maxCor);
    for (y = 0; y < h; y++) {
        for (x = 0; x < w; x++) {
            struct Pixel *p1 = pixelImagem(original, y, x);
            struct Pixel *p2 = pixelImagem(imgCinza, y, x);

            gray = (p1->r*0.3)+(p1->g*0.59)+(p1->b*0.11);

            p2->r = gray;
            p2->g = gray;
            p2->b = gray;
        }
    }
    return imgCinza;
}
```
