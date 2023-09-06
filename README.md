# Crivo de Eratóstenes 🥨
Projeto feito para obtenção de nota para a disciplina de Programação Concorrente.

### Problema 🧩
Eratóstenes foi um dos bibliotecários-chefe da Biblioteca de Alexandria que desenvolveu um algoritmo para encontrar números primos até um dado número n, tal algoritmo ficou conhecido como Crivo de Eratóstenes.

### Algoritmo ⚙️
Dada um número inteiro n, o algoritmo cria uma lista com todos os valores de 1 até o valor limite n, remove da lista todos os números múltiplos de 2, procura o próximo valor primo e remove todos os múltiplos dele que estão presentes na lista e repete o processo até sobrar somente valores primos.

### Solução Proposta 💡
Neste algoritmo, utilizamos três métodos para encontrar a solução do problema das 8 rainhas: a solução sequencial, solução usando programação paralela usando OpenMp e a solução também com programação paralela, mas usando a biblioteca OpenMPI.

#### Solução Sequencial ⛰️
Método usual já descrito anteriormente.

#### Método Paralelizado usando OpenMP 🚥
* Chamamos a função crivo, que aloca um vetor, fazendo um tratamento, apenas deixando os primos que serão usados para remover seus múltiplos, cujo tamanho será a raiz de n + 1;
* Criamos um vetor de tamanho n, e chamamos a função eh_primo para cada um;
* Na função eh_primo, temos um loop que checará se o número é primo e remove os múltiplos de acordo com o números resultantes do vetor do item 1. Esta etapa está paralelizada usando threads;
* Por fim, temos um vetor de tamanho n com valores de 0, caso o número tenha sido removido no loop do passo 3, ou 1, se ele for primo.

#### Método Paralelizado usando OpenMPI 🚦
* Dividimos a lista de números em partes iguais e cada parte é atribuída a um processo;
* O primeiro processo descobre o primeiro fator primo e o enviará para os próximos processos através de um broadcast;
* Os próximos processos marcam os múltiplos desse fator primo;
* Isso se repete para todos os fatores primos que forem descobertos durante a execução;
* E quando encerrar os fatores primos possíveis, um processo contará quantos números primos foram encontrados;


### Conteúdo 📖
Arquivo   | Conteúdo
:---------: | :------:
crivoSERIAL.c | Algoritmo que usa o método sequencial
crivoPARALELO.c | Algoritmo paralelizado usando threads e a biblioteca MP
crivoMPI.c | Algoritmo paralelizado usando MPI

### Autores 👥
* Gardênia Estevam
* Pedro Henrique Lopes

### Hardware e Software 💻
#### Máquina 1 🖥️
Hardware/Software   | Modelo
:---------: | :------:
CPU | Intel(R) Core(TM) i5-8265U CPU @ 1.60GHz, 1800 Mhz, 4 Núcleo(s), 8 Processador(es) Lógico(s)
RAM | 16GB DDR4
Sistema Operacional | Microsoft Windows 10 Home
Linguagem de Programação | C
Compilador | MinGW-W64-builds-4.3.5
MPI | MPI 4.1.1 https://www.microsoft.com/en-us/download/details.aspx?id=54607

#### Máquina 2 🖥️
Hardware/Software   | Modelo
:---------: | :------:
CPU | Intel(R) Core(TM) i7-8565U CPU @ 1.80GHz, 1992 Mhz, 4 Núcleo(s), 8 Processador(es) Lógico(s)
RAM | 8 GB DDR4
Sistema Operacional | Microsoft Windows 10 Home
Linguagem de Programação | C
Compilador | MinGW-W64-builds-4.3.5
MPI | MPI 4.1.1 https://www.microsoft.com/en-us/download/details.aspx?id=54607

### Análise de Desempenho 📈
#### Máquina 1 🖥️
Método | Nº de elementos | Tempo(segundos) | Speedup | Comentários
:----: | :-------------: | :-------------: | :-----: | :----------:
Sequencial | 10.000.000 | 1,606 | - | Existem 664579 números primos menores que 10000000 
Sequencial | 100.000.000 | 35,616 | - | Existem 5761455 números primos menores que 100000000
OpenMP | 10.000.000 | 0,498 | 3,22x | Existem 664579 números primos menores que 10000000
OpenMP | 100.000.000 | 11,534 | 3,08x | Existem 5761455 números primos menores que 100000000
MPI | 10.000.000 | 0,049 | 32,77x | Existem 664579 números primos menores que 10000000
MPI | 100.000.000 | 0,818 | 43,54x | Existem 5761455 números primos menores que 100000000

#### Máquina 2 🖥️
Método | Nº de elementos | Tempo(segundos) | Speedup | Comentários
:----: | :-------------: | :-------------: | :-----: | :----------:
Sequencial | 10.000.000 | 1,70 | - | Existem 664579 números primos menores que 10000000 
Sequencial | 100.000.000 | 35,27 | - | Existem 5761455 números primos menores que 100000000
OpenMP | 10.000.000 | 1,06 | 1,6x | Existem 664579 números primos menores que 10000000
OpenMP | 100.000.000 | 22,74 | 1,55x | Existem 5761455 números primos menores que 100000000
MPI | 10.000.000 | 0,089 | 11,91x | Existem 664579 números primos menores que 10000000
MPI | 100.000.000 | 1,027 | 22,14x | Existem 5761455 números primos menores que 100000000

### Dificuldades Encontradas 👾
Na época, usávamos o Windows e não tínhamos dual boot, portanto tivemos que usar o WSL, que é uma maneira de usar o terminal do Linux no Windows, de forma semelhante à uma máquina virtual. 
Outra dificuldade encontrada foi a primeira maneira que estávamos tentando contruir o algoritmo com o MPI estava um pouco difícil de implementar, assim tivemos que mudar para uma mais fácil e conseguimos construir o algoritmo.
