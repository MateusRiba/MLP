# Implementação de MLP - Introdução a Deep Learning - Grupo 3
Pedro Augusto
Thiago Felipe
Bruno Henrique
Mateus Ribeiro
Áriston Aragão 

Este repositório contém a atividade prática de implementação de uma rede neural Multilayer Perceptron (MLP) utilizando **PyTorch**. O objetivo principal é consolidar os conhecimentos básicos de redes neurais, arquitetura de camadas e otimização de hiperparâmetros.

A base de dados utilizada foi a **Iris dataset** (Scikit-Learn). Para cumprir o desafio bônus da fronteira de decisão, o modelo foi treinado utilizando apenas 2 características (comprimento e largura da sépala).

## Funcionalidades e Requisitos Atendidos
* **Construção Dinâmica:** O modelo permite ao usuário definir a quantidade de camadas ocultas e o número de neurônios por camada.
* **Entrada de Hiperparâmetros:** Definição personalizada de Taxa de Aprendizado, Momentum e Épocas.
* **Escolha do Otimizador:** Suporte para alternar entre **SGD** e **Adam**.
* **Desafio Opcional:** Plotagem gráfica da fronteira de decisão (função discriminativa) em 2D.

---

## Análise de Desempenho e Resultados

Como solicitado na atividade, a escolha dos hiperparâmetros foi feita no modelo de "tentativa e erro". Durante os testes, observamos três cenários distintos que ilustram bem o funcionamento da rede:

### 1. Teste com Otimizador SGD (Taxa de Aprendizado: 0.05 | 300 Épocas)
O modelo obteve um excelente aprendizado inicial. A acurácia subiu rapidamente para cerca de 90% nas primeiras 50 épocas. No entanto, por deixarmos o treinamento rodar por 300 épocas, o modelo começou a apresentar um leve **Overfitting** na reta final, onde a perda (loss) continuava caindo no treino, mas a acurácia nos dados de teste começou a oscilar e cair um pouco.

### 2. Teste com Otimizador Adam (Taxa de Aprendizado: 0.05 | 300 Épocas)
Ao trocar para o otimizador Adam mantendo a mesma taxa de aprendizado alta (0.05), a rede se desestabilizou completamente. O gráfico de acurácia parecia um sismógrafo, oscilando drasticamente. Isso comprovou que o Adam, por ter um passo adaptativo, requer uma taxa de aprendizado base consideravelmente menor, caso contrário ele "pula" o ponto de mínimo global. A fronteira de decisão também gerou divisões confusas.

### 3. Cenário Ideal: Otimizador Adam (Taxa de Aprendizado: 0.001 | 100 Épocas)
Ajustando a taxa de aprendizado para o padrão do Adam (0.001) e reduzindo as épocas, obtivemos o resultado perfeito:
* A curva de perda desceu de forma lisa e constante.
* A acurácia subiu em degraus suaves até estabilizar em excelentes **93.33%**.
* **A Fronteira de Decisão:** O modelo conseguiu generalizar perfeitamente as áreas de classificação, separando muito bem a classe linearmente separável (Setosa) e criando uma fronteira lógica para as outras duas espécies (Versicolor e Virginica), que se sobrepõem no espaço 2D escolhido.

---

## Como executar
1. Clone este repositório.
2. Certifique-se de ter instalado: `torch`, `numpy`, `matplotlib`, `scikit-learn`.
3. Abra e execute o arquivo `.ipynb` no Jupyter Notebook ou Google Colab.
