...



```
#ifndef ESTRUTURA_H_INCLUDED
#define ESTRUTURA_H_INCLUDED  

--------------------------------------------------------------------------------  
    //Realce do contraste por transformação linear.  
    //Estrutura de um Pixel contendo seu RGB.  
--------------------------------------------------------------------------------  


struct Pixel {
    unsigned int r;  
    unsigned int g;  
    unsigned int b;  
};


--------------------------------------------------------------------------------  
    //Estrutura da Imagem contendo suas propriedades, especialmente o vetor dos pixels    
--------------------------------------------------------------------------------  

typedef struct {  
    int larg;  
    int alt;  
    int maxCor;    
    struct Pixel *pixels;  
} Imagem;


struct Pixel* pixelImagem(Imagem* imagem, int y, int x);

Imagem* novaImagem(int larg, int alt, int maxCor);

Imagem* sharp(Imagem *original);

Imagem* blur(Imagem *original);

Imagem* aumentar(Imagem *original);

Imagem* reduzir(Imagem *original);

Imagem* binarizar(Imagem *original, int limiar);

Imagem* escalaCinza(Imagem *original);

Imagem* rotacionar(Imagem *original, char* direcao);

Imagem* inverterHorizontalmente(Imagem *original) ;

Imagem* inverterVerticalmente(Imagem *original);

Imagem* abrirArquivo(char *arquivo);

void salvarArquivo(Imagem *imagem, char *nome_arquivo);  

#endif  // ESTRUTURA_H_INCLUDED
```
