# Relatório de Análise de Desempenho de Algoritmos de Ordenação

## i) Metodologia

**Equipamento Utilizado:**

* **Plataforma:** Google Colab (Ambiente de Nuvem).
* **Processador:** Intel(R) Xeon(R) CPU @ 2.20GHz (Padrão da VM do Colab).
* **Memória RAM:** 13GB.
* **Sistema Operativo:** Ubuntu (Linux).

**Massa de Dados:**

* **Tamanhos dos Vetores:** 1.000, 10.000 e 100.000 elementos.
* **Tipos de Entrada:** * **Aleatória:** Elementos distribuídos aleatóriamente.
* **Crescente:** Vetor já ordenado em ordem crescente.
* **Decrescente:** Vetor já ordenado em ordem inversa, decrescente.

**Algoritmos e Tecnologia:**

* **Linguagem:** Python 3.
* **Algoritmos Implementados:** Bolha (Bubble Sort), Seleção (Selection Sort), Inserção (Insertion Sort), Quick Sort e Merge Sort.
* **Bibliotecas de Análise:** `Pandas` para estruturação de dados e `Seaborn`/`Matplotlib` para visualização dos dados.

---

## ii) Gráficos de Comparação de Tempos

Como alguns métodos são muito lentos e outros muito rápidos, foi usado um gráfico especial (escala logarítmica) para conseguir permitir a comparação visual entre métodos rápidos e lentos. No gráfico abaixo, as barras mais baixas indicam os métodos melhores e mais rápidos.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = {
    'Método': ['Bolha', 'Bolha', 'Bolha', 'Seleção', 'Seleção', 'Seleção', 
               'Inserção', 'Inserção', 'Inserção', 'Quick Sort', 'Quick Sort', 'Quick Sort', 
               'Merge Sort', 'Merge Sort', 'Merge Sort'],
    'Caso': ['Aleatório', 'Crescente', 'Decrescente'] * 5,
    'Tempo (s)': [763.78, 233.16, 859.36, 350.00, 287.93, 296.64, 
                  428.03, 0.091, 609.92, 0.449, 0.283, 0.271, 0.512, 0.272, 0.272]
}

df = pd.DataFrame(data)
plt.figure(figsize=(12, 6))
sns.set_theme(style="whitegrid")
g = sns.barplot(data=df, x='Método', y='Tempo (s)', hue='Caso')
g.set_yscale("log")
plt.title('Comparação de Desempenho (N = 100.000) - Escala Logarítmica')
plt.show()

```

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
