# Relatório de Análise de Desempenho de Algoritmos de Ordenação

## i) Metodologia

**Equipamento Utilizado:**

* **Plataforma:** Google Colab (Ambiente de Nuvem).
* **Processador:** Intel(R) Xeon(R) CPU @ 2.20GHz (Padrão da VM do Colab).
* **Memória RAM:** 13GB.
* **Sistema Operativo:** Ubuntu (Linux).

**Massa de Dados ([Link](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/tree/main/Projeto1/Vetores#:~:text=Vetores)):** 

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

Como alguns métodos são muito lentos e outros muito rápidos, foi usado um gráfico especial (escala logarítmica) para conseguir permitir a comparação visual entre métodos rápidos e lentos. No gráfico abaixo, as barras mais baixas indicam os métodos melhores e mais rápidos.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Dados extraídos da sua tabela
data = {
    'Metodo': ['Bolha', 'Bolha', 'Bolha', 'Seleção', 'Seleção', 'Seleção', 
               'Inserção', 'Inserção', 'Inserção', 'Quick Sort', 'Quick Sort', 'Quick Sort', 
               'Merge Sort', 'Merge Sort', 'Merge Sort'],
    'Caso': ['Aleatório', 'Crescente', 'Decrescente'] * 5,
    'Tamanho': [100000] * 15, # Focando no cenário mais crítico de 100k
    'Tempo': [763.785, 233.165, 859.368,  # Bolha
              350.004, 287.933, 296.649,  # Seleção
              428.039, 0.091, 609.920,    # Inserção
              0.449, 0.283, 0.271,        # Quick Sort
              0.512, 0.272, 0.272]        # Merge Sort
}

df_100k = pd.DataFrame(data)

# 2. Configuração do gráfico
plt.figure(figsize=(14, 7))
sns.set_theme(style="whitegrid")

# Criando o gráfico de barras
plot = sns.barplot(data=df_100k, x='Metodo', y='Tempo', hue='Caso', palette='viridis')

# 3. APLICANDO ESCALA LOGARÍTMICA
plot.set_yscale("log")

# Customização de títulos e labels
plt.title('Comparação de Performance (N = 100.000) - Escala Logarítmica', fontsize=16, fontweight='bold')
plt.ylabel('Tempo de Execução (segundos) - [LOG]', fontsize=12)
plt.xlabel('Método de Ordenação', fontsize=12)

# Adicionando os valores em cima das barras para facilitar a leitura
for p in plot.patches:
    if p.get_height() > 0:
        plot.annotate(format(p.get_height(), '.3f'), 
                      (p.get_x() + p.get_width() / 2., p.get_height()), 
                      ha = 'center', va = 'center', 
                      xytext = (0, 9), 
                      textcoords = 'offset points',
                      fontsize=9, fontweight='bold')

plt.legend(title='Estado Inicial do Vetor', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()

```
**Gráfico de comparação de desempenho dos métodos utilizando dados aleatórios**
![Gráfico de comparação de desempenho dos métodos utilizando dados aleatórios](https://github.com/anabiarochar/Mestrado_AlgoritmosProgramacao/blob/f05afe1d867582bb4105a1c14317c5ba5fc3821f/Projeto1/Imagens/Comparacao%20Desempenho_Aleatorios.png)

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
