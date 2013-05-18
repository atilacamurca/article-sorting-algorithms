# Introdução

Ordenar objetos, de uma maneira geral, é bastante útil pois ajuda a organizar, buscar de forma
rápida, verificar existência, entre outros aspectos. Em computação isso não é diferente. A
ordenação é utilizada em várias áreas, por exemplo Bancos de Dados. Com isso precisamos sempre
de algoritmos de ordenação que façam o trabalho em menos tempo, consumindo menos recursos.

# Métodos de Ordenação

Para ordenar dados computacionais precisamos de métodos, que consistem em procedimentos
que dado um conjunto geram uma saída com o próximo elemento sempre menor ou igual ao anterior,
ou vice versa.

Veremos a implementação e estatísticas dos seguintes métodos de ordenação:

* Bubble Sort
* Selection Sort
* Insertion Sort
* Quick Sort
* Counting Sort
* Bigger Smaller Sort

## Bubble Sort

Método de ordenação bastante simples de implementar e entender. A ideia é percorrer
um vetor de dados, normalmente números, e verificar de dois em dois qual o maior. Em
caso positivo trocar um com o outro.

### Complexidade

Para cada elemento é preciso percorrer o vetor, mesmo que o mesmo já esteja ordenado. Por
isso dizemos que o algoritmo é $O(n^2)$.

### Pseudo-código

Esse método é caracterizado pelo uso de variável auxiliar para fazer o *swap* ou troca.

~~~
void bubble_sort(V[], n)
begin
	k = n - 1
	for i = 1 to n do
		for j = 0 to k do
			if V[j] > V[j + 1] do
				aux = V[j]
				V[j] = V[j + 1]
				V[j + 1] = aux
			endif
		endfor
	endfor
end
~~~

## Selection Sort

O algoritmo inicia buscando o valor mínimo e o coloca na primeira posição. Depois
busca o segundo menor valor e o coloca na segunda posição. Assim por diante.

### Complexidade

Selecionar o menor elemento requer verificar todos os $n$ elementos (sendo $n - 1$ comparações)
e então colocá-lo na posição correta. Encontrar o próximo requer uma busca em $n - 1$
elementos. Daí temos:

\begin{equation}
(n - 1) + (n - 2) + \cdots + 2 + 1 = \frac{n (n - 1)}{2} \in \Theta(n^2)
\end{equation}

### Pseudo-código

Também possui o *swap*, entretanto pode ser que o elemento já esteja na posição correta,
e deverá ser ignorado.

~~~
void selection_sort(V[], n)
begin
	for i = 0 to n - 1 do
		min = i
		for j = i + 1 to n do
			if V[j] < V[min] do
				min = j
			endif
		endfor
		if min != i do
			aux = V[i]
			V[i] = V[min]
			V[min] = aux
		endif
	endfor
end
~~~

## Insertion Sort

A ideia é, se os primeiros elementos já estão ordenados, um elemento não ordenado
pode ser inserido no conjunto ordenado no lugar adequado.

### Complexidade

Para inserir o último elemento precisamos de pelo menos $n - 1$ comparações e $n - 1$ movimentos.
Para inserir o penúltimo elemento precisamos de $n - 2$ comparações e $n - 2$ movimentos. E assim
por diante. Daí podemos concluir que teremos:

\begin{equation}
2 \cdot (1 + 2 + 3 + \dots + (n - 1)) = \frac{2 \cdot (n - 1) \cdot n}{2} = (n - 1) \cdot n \in \Theta(n^2)
\end{equation}

### Pseudo-código

~~~
void insertion_sort(V[], n)
begin
	for i = 1 to n do
		j = i
		while j != 0
				&& V[j] < V[j - 1] do
			aux = V[j]
			V[j - 1] = V[j]
			V[j] = aux
			j = j - 1
		endwhile
	endfor
end
~~~

<!--
http://w3.ualg.pt/~hshah/ped/Aula%2014/Quick_final.html

http://faculty.simpson.edu/lydia.sinapova/www/cmsc250/LN250_Weiss/L16-QuickSort.htm
-->

## Quick Sort

Método caracterizado pelo uso da técnica de divisão e conquista, ou seja, dividir
o problema inicial em subproblemas e resolver um problema menor utilizando
recursividade.

Consiste em dividir o vetor em dois subvetores, dependendo de um elemento denominado
pivô, normalmente o primeiro elemento do vetor. Um dos subvetores contém os elementos
menores que o pivô enquanto o outro contém os maiores. O pivô é colocado entre ambos,
 ficando na posição correta. Os subvetores são ordenados da mesma forma, até que
 se chegue a um vetor com um só elemento.

### Complexidade

Em média o algoritmo é da ordem $O(n \cdot \log n)$, ou seja, há $\log n$ partições,
e para obter cada partição fazemos $n$ comparações (e não mais que $\dfrac{n}{2}$ trocas).

No pior caso temos $O(n^2)$

### Pseudo-código

~~~
void quick_sort(V[], initial, final)
begin
	i = initial
	j = final
	pivot = V[(initial + final) / 2]
	while i < j do
		while V[i] < pivot do
			i = i + 1
		endwhile
		
		while V[j] > pivot do
			j = j + 1
		endwhile
		
		if i <= j do
			aux = V[i]
			V[i] = V[j]
			V[j] = aux
			i = i + 1
			j = j + 1
		endif
	endwhile
	
	if j > initial do
		quick_sort(V, initial, j)
	endif
	
	if i < final do
		quick_sort(V, i, final)
	endif
end
~~~

<!--
referencias counting
http://rosettacode.org/wiki/Sorting_algorithms/Counting_sort#Java

http://www.shannarasite.org/kb/kbsu32.html
-->

## Counting Sort

Diferente de todos os algoritmos vistos até aqui, esse algoritmo não usa comparações.
Para a ordenação é preciso contar quantos elementos existem e colocá-los num array
temporário onde o índice do mesmo é o valor e cada índice representa o número de vezes
que aquele valor aparece.

### Complexidade temporal

O algoritmo tem tempo de execução de $\Theta(n + k)$, onde $n$ é o número de elementos
a serem ordenados e $k$ é a variação dos tais números. Se $k = O(n)$, este algoritmo
tem performance $\Theta(n)$.

### Complexidade espacial

A complexidade espacial é $\Theta(n)$, onde $n$ é o tamanho do vetor que conta os
valores. Nenhuma operação de troca é necessária durante o processo.

### Pseudo-código

~~~
void counting_sort(V[], n, maxValue)
begin
	count[] = [maxValue + 1]
	for i = 0 to n do
		count[i] = count[i] + 1
	endfor
	
	z = 0
	for i = 0 to maxValue do
		while count[i] > 0 do
			V[z] = i
			z = z + 1
			count[i] = count[i] - 1
		endwhile
	endfor
end
~~~

## Algoritmo Proposto - Busca do maior e menor

Inicialmente definimos onde o maior e o menor elementos serão colocados, usando as variáveis
`ordEsq` e `ordDir` como visto na figura \ref{fig:passo1}.

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo1.png}
   \caption{definir posicionamento inicial}
   \label{fig:passo1}
\end{figure}

Logo em seguida fazemos uma busca procurando o maior e o menor elementos (Ver figura \ref{fig:passo2}).

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo2.png}
   \caption{busca do maior e menor elementos}
   \label{fig:passo2}
\end{figure}

Ao encontrar devemos trocar o `menor` com `ordEsq` e `maior` com `ordDir`. Logo
em seguida incrementar o valor de `ordEsq` e decrementar o valor de `ordDir`
(Ver figura \ref{fig:passo3}).

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo3.png}
   \caption{tamanho do vetor torna-se $n - 2$}
   \label{fig:passo3}
\end{figure}

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo4.png}
\end{figure}

Notamos que a medida que estamos ordenando, o caminho a percorrer vai ficando
cada vez menor (Ver figura \ref{fig:passo5}).

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo5.png}
   \caption{tamanho torna-se $n - 4$}
   \label{fig:passo5}
\end{figure}

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo6.png}
\end{figure}

\begin{figure}[h]
   \includegraphics[scale=0.6]{img/maior.menor.algoritmo/passo7.png}
   \caption{vetor ordenado}
   \label{fig:passo7}
\end{figure}

Finalmente, para um *array* ímpar temos que o valor de `ordEsq` e `ordDir`
são iguais. Nessa condição não restam elementos a serem comparados (Ver figura
\ref{fig:passo7}).

### Complexidade

Podemos notar que o algoritmo faz $n$ comparações iniciais. Depois faz $n - 2$
comparações. Em seguida $n - 4$. E assim por diante.

Podemos criar um conjunto $S = \{2, 4, 6, \dots, n\}$. Dessa forma podemos dizer que:

\begin{eqnarray*}
T(n) = \sum_{i = 1}^{\frac{n}{2}} S_i
\end{eqnarray*}

### Pseudo-código

~~~
void maior_menor_sort(V[], n)
begin
	ordEsq = 0, ordDir = n - 1
	for i = ordEsq to (n / 2) do
		maior = i
		menor = i
		for j = i + 1 to ordDir + 1 do
			if V[j] > V[maior] do
				maior = j
			endif
			
			if V[j] < V[menor]
				menor = j
			endif
		endfor
		
		if maior != i do
			aux = V[ordDir]
			V[ordDir] = V[maior]
			V[maior] = aux
		endif
		
		if menor != i do
			aux = V[ordEsq]
			V[ordEsq] = V[menor]
			V[menor] = aux
		endif
		
		ordEsq = ordEsq + 1
		ordDir = ordDir - 1
		
		if ordLeft == ordDir do
			break
		endif
	endfor
end
~~~

# Metodologia

## Como os vetores foram gerados

Os valores do vetor foram gerados usando algoritmo pseudo-randômico em *python*
no seguinte formato:

* **1° linha**: tamanho do vetor a ser gerado.
* **restante das linhas**: valores do vetor.

O código pode ser encontrado em <https://github.com/atilacamurca/sorty/blob/master/files/gen.py>.

## Máquina utilizada

Vejamos a tabela \ref{tab:machine} mostrando detalhes da máquina utilizada para ordenar os vetores.

-----------------------------------------------------------
Classe     Descrição
---------  ------------------------------------------------
system     `6078AA7`

bus        `LENOVO`

memory     `2GiB System Memory`

           `1GiB DIMM DDR2 Synchronous 800 MHz`

           `DIMM DDR2 Synchronous 800 MHz`

processor  `Intel(R) Core(TM)2 Duo CPU E6550 @ 2.33GHz`

memory     `16KiB L1 cache`

           `4MiB L2 cache`
-----------------------------------------------------------

Table: dados obtidos pelo comando `lshw` no Linux.\label{tab:machine}

## Estatísticas

As tabelas abaixo descrevem os algoritmos com seus respectivos tamanhos dos vetores,
médias, valores máximos e mínimos.

----------------------------------------------------
Algoritmo              Média        Máx.        Mín.
----------------  ----------  ----------  ----------
Bubble                 0.072        0.09        0.09

Insertion              0.072        0.09        0.09

Selection              0.072        0.09        0.09

Quick                  0.072        0.09        0.09

Counting               0.072        0.09        0.09

Bigger Smaller         0.072        0.09        0.09
----------------------------------------------------

Table: Vetor de 10 posições.

----------------------------------------------------
Algoritmo              Média        Máx.        Mín.
----------------  ----------  ----------  ----------
Bubble                 0.072        0.09        0.09

Insertion              0.072        0.09        0.09

Selection              0.072        0.09        0.09

Quick                  0.072        0.09        0.09

Counting               0.072        0.09        0.09

Bigger Smaller         0.072        0.09        0.09
----------------------------------------------------

Table: Vetor de 100 posições.

----------------------------------------------------
Algoritmo              Média        Máx.        Mín.
----------------  ----------  ----------  ----------
Bubble                  0.08         0.1         0.1

Insertion              0.086        0.11         0.1

Selection               0.08         0.1         0.1

Quick                  0.072        0.09        0.09

Counting               0.072        0.09        0.09

Bigger Smaller          0.08         0.1         0.1
----------------------------------------------------

Table: Vetor de 1000 posições.

----------------------------------------------------
Algoritmo              Média        Máx.        Mín.
----------------  ----------  ----------  ----------
Bubble                 0.342        0.43        0.42

Insertion              0.142        0.19        0.16

Selection              0.226        0.29        0.28

Quick                  0.128        0.16        0.16

Counting               0.116        0.15        0.14

Bigger Smaller         0.244        0.31        0.29
----------------------------------------------------

Table: Vetor de 10000 posições.

----------------------------------------------------
Algoritmo              Média        Máx.        Mín.
----------------  ----------  ----------  ----------
Bubble                22.508       28.14       28.13

Insertion              2.384        2.98        2.98

Selection             14.128       17.66       17.66

Quick                  0.158        0.21        0.19

Counting               0.146        0.19        0.18

Bigger Smaller        10.584       13.23       13.22
----------------------------------------------------

Table: Vetor de 100000 posições.

----------------------------------------------------
Algoritmo              Média        Máx.        Mín.
----------------  ----------  ----------  ----------
Quick                  0.318         0.4        0.39

Counting               0.242        0.31         0.3
----------------------------------------------------

Table: Vetor de 1000000 posições.

## Gráficos

Vamos ver uma comparação com vetores de tamanho variando de 10 a 1000. Podemos notar
que inicialmente todos tendem a levar o mesmo tempo na média como visto na figura
\ref{fig:chart1}. Entretanto a partir do 1000 eles começam a modificar significamente
o tempo de execução médio.

\begin{figure}[b]
   \includegraphics[scale=0.47]{img/charts/chart-1.png}
   \caption{Comparação 10 a 1000}
   \label{fig:chart1}
\end{figure}

Analisando agora vetores de tamanho variando de 1000 a 10000 veremos uma mudança
mais brusca no tempo de execução dos algoritmos, exceto os algoritmos Quick Sort
e counting Sort que são logarítmicos e tendem a manter seu tempo de execução baixo
(figura \ref{fig:chart2}).

\begin{figure}[h]
   \includegraphics[scale=0.47]{img/charts/chart-2.png}
   \caption{Comparação 1000 a 10000}
   \label{fig:chart2}
\end{figure}

Chegamos a comparação de tamanhos grandes e podemos notar que a diferença de tempo
dá um salto bastante significativo para algoritmos quadráticos, mas ainda assim
Quick Sort e Counting Sort se mantém (figura \ref{fig:chart3}).

\begin{figure}[h]
   \includegraphics[scale=0.47]{img/charts/chart-3.png}
   \caption{Comparação 10000 a 100000}
   \label{fig:chart3}
\end{figure}

Vamos olhar de perto o Quick e Counting Sort mostrados na figura \ref{fig:chart4}.
Podemos notar que o Counting Sort cresce mais lento que o Quick Sort. Com isso
chegamos a conclusão que comparação de valores leva um pouco mais de tempo que outras
operações, entretanto o algoritmo Counting Sort usa um vetor adicional, que neste
caso tinha tamanho 100 (todos os vetores possuem valores variando de 0 a 99).

\begin{figure}[h]
   \includegraphics[scale=0.47]{img/charts/chart-4.png}
   \caption{Comparação 10000 a 1000000}
   \label{fig:chart4}
\end{figure}









