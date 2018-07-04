1. Quais as diferenças entre os barramentos de dados e de endereços?

**Através do barramento de dados a CPU consegue realizar escrita e leitura da 
memória, já o barramento de endereço é somente para leitura.**

2. Quais são as diferenças entre as memórias RAM e ROM?

**RAM: volátil, perde o conteúdo quando é retirada a alimentação.**
**ROM: não-volátil, mantém o conteúdo após a alimentação ser retirada. Possui
escrita lenta comparada a memória RAM.**

3. Considere o código abaixo:

```C
#include <stdio.h>
int main(void)
{
	int i;
	printf("Insira um número inteiro: ");
	scanf("%d", &i);
	if(i%2)
		printf("%d eh impar.\n");
	else
		printf("%d eh par.\n");
	return 0;
}
```

Para este código, responda: 
(a) A variável `i` é armazenada na memória RAM ou ROM? Por quê? 

**A variável é armazenada na memória RAM, pois o tempo de acesso é mais rápido, 
dessa forma, o programa em C executa mais rapidamente.**

(b) O programa compilado a partir deste código é armazenado na memória RAM ou ROM?
Por quê?
    
**O programa é armazenado na ROM, por ser uma memória não-volátil o armazenamento
nela possibilita que o programa seja executado novamente.**

4. Quais são as diferenças, vantagens e desvantagens das arquiteturas Harvard e 
Von Neumann?

**Arquitetura tipo Harvard: Caminhos de dados e de instrução distintos, 
dessa forma, seus componentes internos também estão dispostos em lugares 
distintos, o que a torna mais rápida porém mais complexa.
Von Neumann: é processada uma única informação por vez, visto que nessa tecnologia, 
execução e dados percorrem o mesmo barramento, o que torna a arquitetura mais 
simples porém torna o processo lento em relação à arquitetura Harvard.**

**Desta forma a principal diferença entre as duas arquiteturas é que a 
arquitetura de Harvard separa o armazenamento e o trafego das instruções da CPU 
e dos dados em duas unidades distintas de memória, enquanto a Von Neumann utiliza 
o mesmo espaço de memória para ambos.**

5. Considere a variável inteira `i`, armazenando o valor `0x8051ABCD`. Se `i` é 
armazenada na memória a partir do endereço `0x0200`, como ficam este byte e os 
seguintes, considerando que a memória é: 

(a) Little-endian: **`0xCDAB5180`**
(b) Big-endian: **`0x8051ABCD`**

6. Sabendo que o processador do MSP430 tem registradores de 16 bits, como ele 
soma duas variáveis de 32 bits?

**É necessário utilizar dois registradores para cada variável, dividindo o valor
da variável entre os dois registradores. Sendo assim para realizar a operação
serão necessários 4 registradores.**