# Grafos
## Conjunto de vértices (pontos) conectados por arestas (linhas)
Todas as Estruturas de Dados podem ser representadas por Grafos

Grafo não representa uma distribuição visual da realidade

___

## Terminologia dos Grafos:
- Grau: quantidade de arestas que saem de um vértice
- Caminho: Sequência de vértices conectados por arestas
- Ciclo: Caminho cujos primeiros e últimos vértices são os mesmos (caminho fechado)

Grafos podem estar "quebrados" em alguns pontos, por isso temos redundâncias.

___
## Problemas nos Grafos:
- Caminho entre start e final
	- existe um caminho entre start e final?
	
- Caminho mais curto
	- qual o menor caminho entre start e final? (dijkstra algorithm)

- Detecção de Ciclos
	- existe um ciclo no grafo?

- Ciclo de Hamilton
	- ciclo que usa cada vértice exatamente uma vez

- Ciclo de Euler
	- ciclo que usa cada aresta exatamente uma vez

<img src="https://sumantmath.wordpress.com/wp-content/uploads/2020/07/eulerian-v-shamiltonian-circuits.png" alt="drawing" width="500"/>

- Conectividade
	- existe uma forma de conectar todos os vértices?

- Biconectividade
	- se uma conexão é removida e o vértice ainda é acessível, ele é Biconexo

- Planaridade
	- grafo pode ser desenhado sem cruzamento de arestas?

- Isomorfismo
	- grafos com conexões iguais, porém de formas diferentes
	
___
	
## Problema da Ponte de Königsberg
- se um vértice tem grau ímpar, não podemos partir dele e chegar nele ao usar todas as arestas
- apenas os graus dos vértices de start e final podem ser ímpares

___

## Grafos Dirigidos (possui arestas de direção)
Só pode ir em uma direção específica

**Outdegree** = quantidade de graus (arestas) de saída

**Indegree** = quantidade de graus (arestas) de chegada

___

## Funções Grafos:
- Graph()				--> cria um grafo vazio
- Graph(filename) 		--> cria um grafo a partir de um arquivo de entrada
- addEdge(v, w) 			--> adiciona uma aresta v-w
- string[] getAdj(v)		--> vertices adjacentes (vizinhos) a v
- totalV() 				--> numero de vértices
- totalE()				--> numero de arestas
- string[] getVerts()	--> lista de vértices


**Complexidade O(v) (vértices) é melhor que O(a) (arestas)**

___


# Estrutura mais eficiente para representar Grafos: 
## LISTA DE ADJACÊNCIAS
- funciona de forma similar ao hashing
- a complexidade é O (grau de v) (vértices)
- vai ter redundância

___
## BUSCA EM PROFUNDIDADE (DFS)
[Animação DFS](https://algs4.cs.princeton.edu/lectures/demo/41DemoDepthFirstSearch.mov)

- **objetivo**: passar por todo o grafo
	+ **aplicação**: encontrar um caminho entre dois vértices / encontrar todos os vértices conectados a um determinado vértice
- marca um vértice como visitado, e recursivamente visita o vértice adjacente (vizinho) não marcado (UM POR VEZ) até ficar 'done'
- para procuramos a origem, começamos no vértice de destino, e vemos a coluna EdgeTo() que diz de qual vértice viemos
> estruturas usadas: **marked[]** e **edgeTo[]**
___

## BUSCA EM LARGURA (BFS)

[Animação BFS](https://algs4.cs.princeton.edu/lectures/demo/41DemoBreadthFirstSearch.mov)
- adiciona o vértice em uma **FILA**
- remove o vértice visitado da fila
- colocamos os vizinhos do vertice visitado no momento na fila.
- atualiza o edgeTo[] e distTo[] dos vértices vizinhos.
- Para cada vértice visitado, removemos o mesmo da fila.
- A ordem de visitação é do vértice mais próximo ao vértice mais distante.
- distTo[] é a distância até a origem (primeiro vértice visitado)
- não há repetições
- BFS se preocupa com o caminho com menos vértices (não necessariamente o mais curto)!!
> estruturas usadas: marked, **edgeTo[]**, **distTo[]** e **queue**
- exemplo de BFS: grafo do Kevin Bacon
___

## Ordenação Topológica
[Animação Ordenação Topológica](https://algs4.cs.princeton.edu/lectures/demo/42DemoTopologicalSort.mov)

**PROIBIDO FORMAR CICLO!!!**

- usa apenas DFS

- grafo **dirigido** com ordem de **precedência**
	- ex: disciplinas de um curso 

- **<ins>Pré Ordem:<ins>** ordem de ida da DFS

- **<ins>Pós Ordem:<ins>** ordem de retorno da DFS

- mesmo não tendo caminho, devemos visitar todos os vértices (for externo)

- **<ins>Ordem Topológica<ins>** é o **reverso** do pós ordem. Fazemos o caminho inverso e descobrimos qual a ordem de precedência das arestas.
	- não há problema haver mais de um final
>estruturas usadas: marked[]
___

## Como Saber se um Grafo é Fortemente Conexo? ߷

Primeiramente...

- **<ins>Grafo Conexo:<ins>** grafo NÃO dirigido em que todos os vértices são acessíveis a partir de qualquer vértice
- **<ins>Grafo Fortemente Conexo<ins>**: grafo dirigido em que todos os vértices são acessíveis a partir de qualquer vértice

Visto isso, usamos o **Algoritmo de Kosaraju**:
 
- fazemos uma **DFS** e anotamos a **Pós Ordem**
- invertemos as arestas
- fazemos novamente a **DFS**, agora na **ordem topológica**
- se todos os vértices na segunda DFS forem alcançados a partir do primeiro vértice, é **fortemente conexo**!
	
___

## Árvore Geradora Mínima (MST)

**PROIBIDO FORMAR CICLO!!!**

- Tenta gerar um grafo com os caminhos **mais baratos** para conectar **TODOS** os vértices
	- cada aresta possui um **peso (custo)**

- Características:
	- sub-grafo (mesma quantidade de vértices, mas menos arestas)
	- conectado
	- acíclico
	- deve incluir todos os vértices 


### Algoritmo de Kruskal
[Animacao Kruskal](https://drive.google.com/file/d/1cigZzmfqAQFTZGKSZmRe-YcqtvMioWda/view?usp=sharing)

- colocamos todos as arestas com seus respectivos vertices e pesos em **ordem crescente de peso**
- construimos a MST a partir da aresta de menor peso
- **a construção é desconexa** (várias areastas são criadas em diferentes pontos do grafo)	
	- do menor ao maior peso
- lembrando que **não podem haver ciclos!!**

Exemplo de Algoritmo de Kruskal:
<img src="https://raw.githubusercontent.com/eduardo-de-bastiani/Grafos/main/Images/MST.jpeg" width=900>

### Algoritmo de Prim
- começa pela aresta menos custosa
- verifica qual a aresta mais barata entre os vertices conectados e a conecta
- **a construção é conectada** (só podemos criar arestas a partir de vértices que já foram conectados)

#### Como encontrar um ciclo?? ⭕ 
- usamos uma estrutura similar ao union-find, onde os elementos tem um **marcador da raiz/conjunto**
- se, antes de colocarmos uma aresta entre dois vértices, eles possuírem a mesma raíz (fazem parte do mesmo conjunto), <ins>temos um ciclo!!<ins>

___

## Caminho Mínimo
- menor custo (distancia) de um ponto a todos os outros
	- diferente do BFS (busca caminho com menos vértices)

Tipos:
- **<ins>Single source:<ins>** de um vértice *s* para todos os demais (origem fixa)
- **<ins>Single sink:<ins>** de cada vértice para um vértice específico *t* (destino fixo)
- **<ins>Source-sink:<ins>** de um vértice *s* para outro *t* (origem e destino fixos)
- **<ins>All pairs:<ins>** entre todos os pares de vértices

GPS usam Single sink (pode haver recálculo de rota)

- SEM CICLOS!

### Algoritmo de Dijkstra 💠

1. inicializa todas as distTo[] de todos os vértices com infinito positivo

2. escolhe um vértice source

3. verifica todos os caminhos para os vizinhos

4. atualiza os caminhos somados ao distTo[]

5. atualiza os edgeTo[]

6. seleciona o menor caminho de qualquer vértice

7. repete os passos 3 a 6 (faz isso para todos os caminhos possíveis)

> Para grafos densos (muitas arestas), o Floyd Warshall é melhor, mesmo sendo O(n³)

### Relaxamento (➿ --> ➰)

Relaxamento é o **coração** do Algoritmo de Dijkstra:

- quando um caminho mais barato (menor) é encontrado, ele troca o distTo[], o edgeTo[] e altera a fila de prioridade do novo caminho até o vértice


___

## Caminho Crítico

[vídeo caminho crítico](https://www.youtube.com/watch?v=t6KVR80B7Dc)

- maior caminho (caminho crítico) determina o menor tempo necessário para completar as tarefas

- **Forward** irá calcular o menor tempo de finalização das tarefas

**Regra 1 Forward:**
- propaga o tempo de uma tarefa para as demais

<img src="https://raw.githubusercontent.com/eduardo-de-bastiani/Grafos/main/Images/ForwardRule1.png" width= 500>

**Regra 2 Forward:**
- propaga o **maior** numero para a proxima tarefa

<img src="https://raw.githubusercontent.com/eduardo-de-bastiani/Grafos/main/Images/ForwardRule2.png" width= 500>

**Regra 1 Backward:**
- propaga o tempo de uma tarefa para as demais
<img src="https://raw.githubusercontent.com/eduardo-de-bastiani/Grafos/main/Images/BackwardRule1.png" width= 500>

**Regra 2 Backward:**
- propaga o **menor** numero para a proxima tarefa
<img src="https://raw.githubusercontent.com/eduardo-de-bastiani/Grafos/main/Images/BackwardRule2.png" width= 500>

>Se a diferença entre o *start time* e o *finish time* for == 0, a tarefa é **crítica**. Se a diferença for != 0, a tarefa é não crítica.

**Exemplo:**

<img src="https://raw.githubusercontent.com/eduardo-de-bastiani/Grafos/main/Images/CriticalPath.png" width=600>

___

# Fluxo em Redes 

- fluxo máximo em um grafo
- source-sink (de um ponto *'s'* a um ponto *'t'*)
- usa DFS

## Ford-Fulkerson

Para um caminho existir, as arestas devem ser:

- não completas em **forward**

- não vazias em **backward** (podemos remover de arestas backward se estiverem no caminho)

Passos para o Ford-Fulkerson:

1. encontrar um caminho
2. descobrir o gargalo (fluxo máximo de todas as arestas do caminho)
3. computar o caminho

> O **fluxo máximo** será a **soma das arestas que chegam no ponto *'t'*** (terminal)