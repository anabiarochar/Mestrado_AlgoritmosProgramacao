# Relatório de Análise de Desempenho de Algoritmos de Ordenação

## i) Metodologia

**Equipamento Utilizado:**

* **Plataforma:** Google Colab (Ambiente de Nuvem).
* **Processador:** Intel(R) Xeon(R) CPU @ 2.20GHz (Padrão da VM do Colab).
* **Memória RAM:** 13GB.
* **Sistema Operativo:** Ubuntu (Linux).

**Massa de Dados** ([Link](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/tree/main/Projeto1/Vetores#:~:text=Vetores))**:** 

* **Tamanhos dos Vetores:** 1.000, 10.000 e 100.000 elementos
* **Tipos de Entrada:**
    * **Aleatória:** Elementos distribuídos aleatóriamente.
    * **Crescente:** Vetor já ordenado em ordem crescente.
    * **Decrescente:** Vetor já ordenado em ordem inversa, decrescente.

**Algoritmos e Tecnologia:**

* **Linguagem:** Python 3.
* **Algoritmos Implementados:** Bolha (Bubble Sort), Seleção (Selection Sort), Inserção (Insertion Sort), Quick Sort e Merge Sort. Todos os códigos utilizados se encontram [neste repositório](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/tree/main/Projeto1#:~:text=Projeto1)
* **Bibliotecas de Análise:** `Requests` que permite o código acesse a internet para acessar os links com as bases de dados, `Time` que funciona como o cronômetro oficial para execução dos métodos, `Random` para geração de números randômicos, `Pandas` para estruturação de dados e `Seaborn`/`Matplotlib` para a visualização desses dados.

---

## ii) Gráficos de Comparação de Tempos

Foram gerados alguns gráficos para comparação entre os tempos de execução dos diferentes métodos quem mostram a discrepância entre métodos quadráticos e log-lineares. Os códigos usados para gerar os gráficos foram gerados com IA através de um prompt descritivo. Os códigos e gráficos gerados se encontram [neste notebook](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/blob/main/Projeto1/Gráficos.ipynb#:~:text=Gráficos.ipynb).
O gráfico abaixo utiliza os dados reais da sua tabela (N=100.000) com escala logarítmica para permitir a comparação visual entre métodos rápidos e lentos.

**Gráfico de Desempenho de Algoritmos por tipo de vetor**

Esta análise foca em como os algoritmos se comportam conforme o volume de dados cresce, utilizando os três gráficos gerados (Aleatório, Crescente e Decrescente). O uso da escala logarítmica no eixo Y nos permite ver, no mesmo quadro, algoritmos que levam milissegundos e algoritmos que levam quase 15 minutos. E mostra claramente a surpresa de ter o algorítmo inserção como mais eficiente do que os log-lineares Merge Sort e Quick Sort.

![Gráfico de Desempenho de Algoritmos por tipo de vetor](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/blob/4d0761ab275ce3c13e04b93353a04ea377f94504/Projeto1/Imagens/Desempenho%20de%20Algoritmos%20por%20tipo%20de%20vetor.png)

**Gráfico de Algoritmos Eficientes x Quadraticos**

Esta análise foca na comparação visual entre as duas categorias de algoritmos apresentadas nos gráficos: os de alta performance (O(n log n)) e os de força bruta (O(n²)).
A principal conclusão ao observar os dois gráficos lado a lado é a diferença muito grande de escala no eixo Y (tempo), o que demonstra por que a escolha do algoritmo é mais importante do que o hardware.

![Gráfico de Algoritmos Eficientes x Quadraticos](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/blob/4d0761ab275ce3c13e04b93353a04ea377f94504/Projeto1/Imagens/Algoritmos%20Eficientes%20x%20Quadraticos.png)

**Gráfico de Comparação de Performance**

Esta análise foca no gráfico de barras gerado para a carga de 100.000 elementos, utilizando uma escala logarítmica. O uso dessa escala é necessário para que seja possível visualizar, no mesmo quadro, a grande diferença de performance entre os métodos mais simples e os mais avançados. No gráfico é possível visualizar como o método bolha é o menos eficiente para grandes massas de dados e também que os métodos Merge Sort e Quick Sort são bem estáveis independente da ordenação inicial dos dados.

![Gráfico de Comparação de Performance](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/blob/4d0761ab275ce3c13e04b93353a04ea377f94504/Projeto1/Imagens/Comparac%CC%A7a%CC%83o%20de%20Performance.png)


---

## iii) Análise Crítica sobre a Eficiência

A análise dos dados revela uma divisão clara entre dois grupos de algoritmos:

1. **Algoritmos Quadráticos ( $O(n^2)$ ):** Ao olhar para os resultados, percebemos que os algoritmos Bolha, Seleção e Inserção apesar de funcionarem bem para listas pequenas, são inviáveis para grandes volumes de dados (100.000). O método Bolha foi o menos eficiente, atingindo 859 segundos (~14 minutos) no pior caso. O método Seleção é o mais estável entre os lentos, variando pouco entre os casos aleatórios e ordenados. Porém observa-se que o método Inserção apresentou o melhor desempenho de todo o experimento quando a lista estava já ordenada de forma crescente (0,091s). Isso mostra que, para listas ordenadas ou quase ordenadas, um algoritmo simples pode superar métodos complexos como Merge Sort ou Quick Sort.
2. **Algoritmos Log-Lineares ( $O(n \log n)$ ):** Os métodos Merge Sort e Quick Sort se mostraram muito eficientes com tempos inferiores à 1 segundo mesmo com 100.000 elementos. A eficiência do Quick Sort foi maior, chegando a ser aproximadamente 3.000 vezes mais rápido que o Bolha no caso aleatório. Os dois métodos foram bem constantes, levando aproximadamente o mesmo tempo independente se a lista está pré-ordenada ou não.



---

## iv) Análise Assintótica X Tempos Obtidos

A teoria assintótica prevê como o tempo cresce conforme $N$ aumenta, e os dados obtidos validam estas previsões com precisão:

* **Padrão Quadrático:** No método Bolha (Aleatório), ao passar de 10.000 para 100.000 elementos (um aumento de 10x no tamanho), o tempo saltou de 6,87s para 763,78s. Isso representa um aumento de aproximadamente 111 vezes, o que é condizente com a previsão $O(n^2)$, onde $10^2 = 100$.
* **Padrão Log-Linear:** No Merge Sort, o aumento de 10x no tamanho (10k para 100k) resultou num aumento de tempo de 0,032s para 0,512s (aprox. 16 vezes). Este crescimento muito mais suave é o que a teoria define como eficiência $O(n \log n)$.
* **Melhor Caso vs. Teoria:** A teoria indica que o Inserção tem melhor caso $O(n)$. Os dados confirmam: o tempo para 100.000 elementos no caso Crescente (0,091s) é ordens de magnitude menor que no caso Aleatório (428,03s), provando que a estrutura inicial dos dados pode alterar a classe de complexidade na prática.
* **Conclusão:** Os resultados práticos alinham-se com a hierarquia de funções da análise assintótica, demonstrando que a escolha do algoritmo é mais impactante do que o poder do hardware para grandes massas de dados.
