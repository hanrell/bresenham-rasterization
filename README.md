# Breseham's line algorithm
---
Algorítimos de Rasterização

## Menu

* [Introdução](#introdução)
* [Points Rasterization](#points-rasterization)
* [Digital Differential Analyzer](#digital-differential-analyzer)
* [Bresenham Algorithm](#bresenham-algorithm)
* [Drawing Triangles](#drawing-triangles)
* [Conclusion](#conclusion)
* [References](#references)
* [Build Instructions](#build-instructions)

---

### Introdução
Este trabalho foi desenvolvido para a disciplina de Introdução à Computação Gŕafica, ministrada pelo Prof. Dr. Christian Azambuja Pagot, na Universidade Federal da Paraíba.

O trabalho trata da implementação do algorítmo de Bresenham para a rasterização de primitivas geométricas nas linguagens C/C++.
A compilação exige que os cabeçalhos do OpenGL e a GLUT (The OpenGL Toolkit) estejam instalados. Após instalá-los:

$ make

$ ./cgprog

Com a evolução das tecnologias, e por questões de segurança, os sistemas operacionais atuais impedem o acesso direto a memória à memória de vídeo. Por esse motivo, será usado um framework desenvolvido pelo professor que simula esse acesso à memória.

---

### Pixels

Os monitores da atualidade são compostos por uma malha de pixels, com X pixels de largura por Y pixels de altura, formando um espaço bidimensional. Entretanto, a disposição desses pixels na memória de vídeo se dá de forma linear, onde todos os pixels são armazenados de forma contínua no que chamamos de *colour buffer*. Este fato deve ser levado em consideração quando se trabalha com a manipulação de pixels.

A maioria dos monitores no mercado utilizam o padrão RGBA, onde cada pixel possui 4 componentes de cor: R para vermelho (RED), G para verde (GREEN), B para azul (BLUE) e A para transparência (ALPHA). Cada componente ocupa 1 byte do *colour buffer*, totalizando 4 bytes por pixel. Para facilitar o entendimento, vejamos o seguinte esquema:



<p align="center">
	<br>
	<img src="./prints/matrix.png"/ width=600px height=400px>
	<h5 align="center">Figure 1 - Rasterization representation</h5>
	<br>
</p>

Now let's look more close the function destined to execute the point rasterization.
```C++
void putPixel(int xWidth, int yHeight, std::vector<int>& myRGBA) {
	for (size_t i = 0; i < 4; i++) {
	FBptr[xWidth*4+i + yHeight*4*IMAGE_WIDTH] = myRGBA.at(i);
	}
}
