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

<!-- definir algoritmos restantes... -->

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
		j = 1
		while j <= k do
			if V[j] > V[j + 1] do
				aux = V[j]
				V[j] = V[j + 1]
				V[j + 1] = aux
			endif
			j = j + 1
		endwhile
	endfor
end
~~~

## Selection Sort

<!-- TODO: falar sobre selection sort ... -->
