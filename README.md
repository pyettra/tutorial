# Colheita Miserável 

Implementação de um jogo interativo em linguagem C com aplicação dos conteúdos estudados ao longo do semestre

## Instruções do projeto

O objetivo deste trabalho é desenvolver as diversas competências aprendidas durante esse semestre no curso de Algoritmos e Estrutura de Dados II. Dentre elas, temos a implementação de estruturas de dados como pilhas e filas, alocação dinâmica de memória, leitura de arquivos, ordenação das estruturas e conhecimento das structs necessárias para construir o jogo. Além dessas competências, alguns aspectos da própria linguagem C foram trabalhados: a leitura de dados, a estruturação de matrizes e vetores e as decisões de projetos que otimizam a usabilidade do jogo.

## Tecnologias utilizadas

O trabalho foi implementado em linguagem C, com apoio do editor de texto Sublime.

## Estrtutura do projeto

O projeto foi dividido em 3 arquivos para melhorar gerenciarmos suas funcionalidades: main.c, jogo.h e jogo.c. O arquivo main.c inicializa todas as partes importantes da aplicação, como a chamada de inicialização do mapa, de personagem, chamada de opções que podem ser escolhidas pelo usuário e o laço de repetição que controla a visualização dessas opções. Já o arquivo jogo.h define todas as estruturas de dados utilizadas ao longo da aplicação. Veremos essa divisão a seguir. Além das estruturas, temos também as chamadas de funções utilizadas. O arquivo jogo.c é a implementação das funções declaradas nos arquivos anteriores. É a parte do código que realiza todas os comandos necessários para que o jogo aconteça: movimentação do personagem, impressão do mapa, retirada de elementos da fila e da pilha, além das adições.

## Structs utilizadas

Dividimos o projeto pelas structs necessárias para o jogo acontecer. Elas são as seguintes e possuem os determinados dados:

### Semente
Possui um nome que a identifica (string), um tempo de crescimento (int), a variável 'ready' que diz quanto tempo já passou até a semente estar pronta (int) e as variáveis linha e coluna (int) que indicam a posição que essa semente se encontra no mapa. 

### Jogador
Possui nome (string), indicador de fome (int), indicador de saúde (int), variáveis de linha e coluna que indicam a posição do jogador no mapa (int) e um vetor chamado mochila, de 50 posições, do tipo semente. 

### Mapa
Possui um ponteiro do tipo char que chamaremos de mapa (e que receberá o arquivo de texto a ser lido), as variáveis de linha (lin) e coluna (col) do tipo inteiro, um vetor chamado "chao", de 300 posições, do tipo semente e que cuidará das sementes que estão no chão do mapa. A última variável se chama "plantado", de 300 posições, também do tipo semente e que indica as sementes que já foram plantadas no terreno.

###Observa
Estrutura criada para atualizar os dados dentro do mapa. Toda vez que a função observa é chamada, temos uma atualização sobre as sementes do terreno e qual o estado delas. Fazemos isso ataravés de 3 variáveis: uma variável fruta do tipo semente (que indica a primeira semente a ser observada), uma variável que indica o estado que essa semente está (se está pronta ou não para ser colhida, se já está podre) e chamamos de estado (int). Por último, a variável prox, que é um ponteiro do tipo observa e que mostrará as informações referentes à próxima semente.

## Funções utilizadas

Para realizar a implementação das funções, inicialmente mapeamos todas as funcionalidades do jogo e as instruções que o usuário poderia seguir. Podemos separar os tipos de função em dois grandes grupos: as funções que estão relacionadas com as ações do usuário e as funções de controle do fluxo do jogo. Comecemos pelas funções de controle:

  ## Funções de controle 

-> map random_semente(map terreno): essa função faz o controle dos tipos de semente que estarão dentro do mapa quando o jogo for inicializado e gerará susas posições de modo randômico. Para isso, passamos o terreno, que é do tipo Map, como argumento da função. O retorno da função será uma estrutura do tipo Map, atualizada com as sementes em posições randômicas. Nessa função, fazemos o controle do tipo de semente que será colocada nas posições do mapa e também as inicializamos com os respectivos nomes, variável de crescimento e a variável "ready", que é incrementada até a semente estar pronta para ser colhida ou apodrecer. Aqui, criamos 4 tipos de sementes disponíveis no mapa:

  ### SEMENTES
  
  ### 1
  Nome: Amor
  Crescimento: 3
  
  ### 2
  Nome: Abóbora
  Crescimento: 7
  
  ### 3
  Nome: Fruto do Conde
  Crescimento: 10
  
  ### 4
  Nome: Discórdia
  Crescimento: 12

O controle dessa função é feito através de um laço de while, que randomiza a posição da semente e, conforme o mapa passado como argumento, identifica se essa posição randômica criada é uma posição de plantio. Assim, a semente é plantada e temos algumas sementes colocadas no mapa antes do usuário se locomover pelo cenário.

-> int valor(map M1): essa função faz o controle do número de sementes plantadas no mapa. Para isso, fazemos um laço de while que verifica todas as posições do vetor "plantado" e incrementa uma variável "i" toda vez que o nome da semente plantada não for nulo. Assim, temos um controle de todas as sementes já plantadas no mapa. 

-> int sort(observa *ponteiro*, observa *auxiliar*, int n): essa função realizará o controle da fila de sementes presentes no mapa, verificando o estado de uma semente x e organizando sua posição na fila conforme a comparação do seu estado com o estado da próxima semente. Essa função é utilizada dentro da função de organização da fila de sementes no mapa.

-> map fila(map M1, int acao): essa função organiza a fila de sementes presentes no mapa e das sementes que o jogador pode colher do mapa conforme a lotação de sua mochila. A organização das sementes na mochila é realizada através de um controle do número de sementes já presentes na mochila e o número máximo suportado por ela (50). Para isso, percorremos o vetor mochila, que é do tipo semente, até encontrarmos a posição em que o nome da semente é vazio. Essa posição está dentro dos limites de posições da mochila, pois fazemos um laço de for que vai até 50. Assim, encontramos a primeira posição vazia do vetor e inserimos a semente, retirando-a do mapa.

-> map inicializa_map(char *arquivo*): a função que realiza a alocação de memória de todos os espaços necessários para imprimirmos o mapa passado por um arquito txt, recebido pela variável *arquivo* parâmetro dessa função. Percorremos as linhas e colunas dadas pelo arquivo e imprimimos o mapa.

-> map inicializa_personagem(map M1): a função responsável pela inicialização de todos os atributos do persongame no jogo. Para isso, passamos como parâmetro da função a variável M1 do tipo map, que possui em sua estrutura o atributo P1, do tipo jogador. Assim, os atributos do jogador são iniciados: a fome é setada para 50, a saúde para 100 e a posição incial do jogador é randomizada. Aqui, também chamamos a função que inicia a mochila do jogador.

-> map inicializa_mochila(map M1): esta é a função que inicializa a mochila do jogador. Nela, passamos novamente o parâmetro M1 do tipo map, que possui no seu jogador a propriedade mochila. As sementes que a mochila possui inicialmente são randomizadas. 

-> int print_ajuda(): função que mostra todas as opções que podem ser executadas pelo usuário ao longo do jogo. A seguir, temos essas opções, que serão explicadas dentro de cada função relacionada a alguma ação do jogo:

    ESCOLHA UMA DAS OPCOES VALIDAS
    "1 - ANDAR"
      "a - ESQUERDA"
      "d - DIREITA"
      "s - BAIXO"
      "w - CIMA"
    "2 - OBSERVAR"
    "3 - COLHER"
    "4 - PLANTAR"
    "5 - COMER"
    "6 - RECOLHER"
  
 -> map opcoes(map M1): função que chama a impressão de mapa e a função de ajuda (print_ajuda()). É responsável pelo controle das ações que serão realizadas quando o usuário escolhe alguma opção. Chama a atualização de fila de sementes no momento que o usuário escolhe a opção de observação do mapa, função de plantar para a opção 4, de colher para 3, comer para 5 e andar para 1.
 
-> void imprimeMapa(map M1): função responsável pela impressão do mapa no terminal do usuário. Percorre todas as linhas e colunas da matriz e realiza a impressão de caracteres. Consideramos que:
  
  define paredeCimaBaixo '-'
  define paredeEsquerdaDireita '|'
  define andar '.'
  define plantar '*' 
  
 Nosso mapa foi definido pelo arquivo txt transcrito abaixo:
 
   5 24
  ------------------------
  |......................|
  |..***....****....***..|
  |..***....****....***..|
  ------------------------


-> map fim_de_turno(map M1): define o modo como o tempo passa dentro do jogo. Escolhemos controlar o tempo do jogo através da fome do jogador, que aumenta conforme o passar de turno e diminui quando o personagem come alguma fruta. Esse número depende do quanto a fruta produz saciedade no jogador.


   ## Funções de ação

-> map personagem_plantar(map M1): a função responsável pelo controle da ação de plantio do jogador. Inicialmente, fazemos a verificação se o terreno escolhido (linha e coluna) é apropriado para plantio. Isso é deifinido pelo caracter que ocupa essa posição no mapa. Se for um asterisco, temos uma opção válida de terreno de plantio. Verificamos também se há ou não sementes disponíveis na mochila. Fazemos também a verificação se há ou não sementes prontas para serem comidas. Caso exista alguma semente pronta para ser plantada dentro da mochila, colocamo-a no terreno e tiramos da mochila.

-> map personagem_movimentacao(map M1, char C): essa função é reponsável pela movimentação do personagem dentro do mapa. As restrições de terreno estão relacionadas aos limites de bordas (esquerda, direita, em cima, embaixo). No resto, podemos movimentar o jogador pelo mapa inteiro. Quando escolhida a opção de movimentação, o usuário pode escolher entre 4 opções: a (esquerda), d (direita), w (para cima) e s (para baixo). Realizamos essa movimentação aumentando ou diminuindo posições de linha ou coluna, dependendo do tipo de movimento escolhido pelo usuário.

-> map personagem_comer(map M1): o personagem só poderá comer se na mochila dele houver sementes que estejam prontas para serem comidas. Aqui também fazemos controle da quantidade de fome que será diminuída quando o jogador comer algo, conforme a semente escolhida (esse controle é feito pela variável de crescimento da semente).

