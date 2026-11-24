# Esteira de Aprendizado de Máquina – Car Evaluation

## 1. Sobre o projeto

Este projeto tem como objetivo desenvolver uma esteira de aprendizado de máquina utilizando Python, contemplando desde a preparação e transformação dos dados até o treinamento, a avaliação e a realização de previsões individuais.

Foi desenvolvido um modelo de classificação multiclasse capaz de identificar a categoria de aceitabilidade de um veículo com base em suas características, utilizando o algoritmo **Random Forest**.

O projeto foi desenvolvido como atividade acadêmica individual, visando à aplicação prática dos conceitos de aprendizado de máquina, análise de dados e classificação.

Link do vídeo explicativo: https://www.youtube.com/watch?v=oxlboz0Lduk

## 2. Dataset utilizado

Foi utilizado o conjunto de dados **Car Evaluation**, disponibilizado pela Universidade da Califórnia em Irvine (UCI Machine Learning Repository).

- **Nome:** Car Evaluation
- **Fonte:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/19/car+evaluation)
- **Arquivo utilizado:** `car.data`
- **Quantidade de registros:** 1.728
- **Atributos de entrada:** 6
- **Quantidade total de colunas:** 7
- **Quantidade de classes:** 4
- **Tipo de problema:** Classificação multiclasse

### 2.1. Atributos do dataset

| Atributo | Descrição |
|---|---|
| `buying` | Preço de aquisição |
| `maint` | Custo de manutenção |
| `doors` | Quantidade de portas |
| `persons` | Capacidade de passageiros |
| `lug_boot` | Tamanho do porta-malas |
| `safety` | Nível estimado de segurança |
| `class` | Classificação de aceitabilidade do veículo |

### 2.2. Variável-alvo

A variável `class` representa a classificação de aceitabilidade do veículo. Para o desenvolvimento do projeto, suas categorias foram transformadas em valores numéricos.

| Classe original | Valor numérico | Descrição |
|---|---:|---|
| `unacc` | 0 | Inaceitável |
| `acc` | 1 | Aceitável |
| `good` | 2 | Bom |
| `vgood` | 3 | Muito bom |

### 2.3. Distribuição das classes

| Classe | Quantidade | Percentual |
|---|---:|---:|
| Inaceitável | 1.210 | 70,02% |
| Aceitável | 384 | 22,22% |
| Bom | 69 | 3,99% |
| Muito bom | 65 | 3,76% |
| **Total** | **1.728** | **100%** |

A análise exploratória identificou um desbalanceamento entre as classes, considerando a predominância da categoria `unacc`.

Não foram identificados valores ausentes ou registros duplicados.

## 3. Tecnologias e bibliotecas utilizadas

O projeto foi desenvolvido em Python, utilizando o Google Colab como ambiente de desenvolvimento e execução.

| Tecnologia | Finalidade |
|---|---|
| Python | Linguagem de programação |
| Google Colab | Ambiente de desenvolvimento e execução |
| Pandas | Carregamento, manipulação e análise dos dados |
| NumPy | Operações numéricas e validação dos resultados |
| Scikit-learn | Pré-processamento, divisão dos dados, treinamento e avaliação |
| Matplotlib | Visualização gráfica dos resultados |
| Zipfile e OS | Extração e localização dos arquivos |

## 4. Etapas da esteira de aprendizado de máquina

A esteira foi organizada em 11 etapas:

1. **Importação das bibliotecas:** carregamento das bibliotecas necessárias para o desenvolvimento do projeto.
2. **Extração e carregamento dos dados:** extração do arquivo ZIP, leitura do arquivo `car.data` e definição dos nomes das colunas.
3. **Análise exploratória:** apresentação das estatísticas descritivas, identificação das categorias, verificação de valores ausentes, duplicidades e distribuição das classes.
4. **Transformação e limpeza:** conversão da variável-alvo em valores numéricos, embaralhamento das linhas e redefinição dos índices, preservando os registros originais.
5. **Divisão dos dados:** separação dos registros em conjuntos de treinamento, validação e teste, utilizando estratificação para preservar a proporção das classes.
6. **Pré-processamento:** configuração do `OneHotEncoder` e do `ColumnTransformer` para transformação dos atributos categóricos.
7. **Treinamento:** configuração e treinamento do algoritmo Random Forest, utilizando 300 árvores de decisão e balanceamento dos pesos das classes.
8. **Avaliação com dados de validação:** análise da acurácia, relatório de classificação e comparação com uma classificação de referência baseada na classe majoritária.
9. **Avaliação com dados de teste:** avaliação final do modelo utilizando registros que não participaram do treinamento ou da validação.
10. **Matriz de confusão:** apresentação gráfica dos acertos e erros de classificação entre as quatro categorias.
11. **Predição individual:** demonstração de uma classificação utilizando um registro do conjunto de teste e realização de uma nova predição com atributos informados manualmente.

O pré-processamento e o classificador foram integrados em uma única estrutura utilizando `Pipeline` e `ColumnTransformer`.

Essa abordagem permite que as transformações sejam aprendidas exclusivamente a partir dos dados de treinamento, evitando o vazamento de informações dos conjuntos de validação e teste.

### 4.1. Divisão dos dados

| Conjunto | Proporção aproximada | Registros |
|---|---:|---:|
| Treinamento | 70% | 1.209 |
| Validação | 15% | 259 |
| Teste | 15% | 260 |
| **Total** | **100%** | **1.728** |

### 4.2. Configuração do modelo

O algoritmo Random Forest foi configurado com os seguintes parâmetros:

| Parâmetro | Valor |
|---|---|
| `n_estimators` | 300 |
| `random_state` | 42 |
| `class_weight` | balanced |
| `n_jobs` | -1 |

A utilização de `class_weight="balanced"` busca compensar o desbalanceamento identificado entre as classes.

Após a aplicação do `OneHotEncoder`, os seis atributos categóricos foram representados por 21 atributos binários.

## 5. Resultados obtidos

Após o treinamento e a avaliação do modelo, foram obtidos os seguintes resultados:

| Indicador | Validação | Teste |
|---|---:|---:|
| Quantidade de registros | 259 | 260 |
| Classificações corretas | 251 | 251 |
| Classificações incorretas | 8 | 9 |
| Acurácia | 96,91% | 96,54% |
| F1-score macro | 0,9161 | 0,9114 |

### 5.1. Comparação com a classificação de referência

Foi utilizada uma classificação de referência que atribui a todos os registros a classe majoritária identificada no conjunto de treinamento.

| Modelo | Acurácia na validação |
|---|---:|
| Classificação de referência | 69,88% |
| Random Forest | 96,91% |

O Random Forest apresentou um desempenho superior à classificação de referência em 27,03 pontos percentuais.

A diferença de aproximadamente 0,37 ponto percentual entre as acurácias de validação e teste indica consistência no desempenho do modelo sobre registros não utilizados durante o treinamento.

### 5.2. Matriz de confusão

| Classificação real / prevista | Inaceitável | Aceitável | Bom | Muito bom |
|---|---:|---:|---:|---:|
| Inaceitável | 177 | 4 | 1 | 0 |
| Aceitável | 0 | 56 | 1 | 1 |
| Bom | 0 | 1 | 9 | 0 |
| Muito bom | 0 | 0 | 1 | 9 |

A matriz de confusão demonstra que o modelo classificou corretamente 251 dos 260 registros do conjunto de teste.

Foram obtidos 177 acertos na classe Inaceitável, 56 na classe Aceitável, nove na classe Bom e nove na classe Muito bom.

### 5.3. Desempenho por classe

| Classe | Registros | Acertos | Recall |
|---|---:|---:|---:|
| Inaceitável | 182 | 177 | 97,25% |
| Aceitável | 58 | 56 | 96,55% |
| Bom | 10 | 9 | 90,00% |
| Muito bom | 10 | 9 | 90,00% |

O modelo apresentou recall igual ou superior a 90% em todas as classes. Entretanto, a menor quantidade de registros das classes minoritárias deve ser considerada na interpretação dos resultados.

### 5.4. Predição individual

Foi realizada uma predição utilizando um registro individual do conjunto de teste.

O resultado apresentado pelo modelo foi:

- **Classificação real:** Inaceitável.
- **Classificação prevista:** Inaceitável.
- **Probabilidade estimada da classe prevista:** 71,33%.
- **Resultado da predição:** Correto.

Também foi implementada uma predição utilizando características de um veículo informadas manualmente, demonstrando a possibilidade de utilização da esteira com novos dados de entrada.

## 6. Como reproduzir a execução

Para reproduzir a execução apresentada no vídeo, siga os passos abaixo.

### Pré-requisitos

- Uma conta Google para acessar o Google Colab.
- O notebook Python (`.ipynb`) disponibilizado neste repositório.
- Conexão com a internet para acessar o dataset.

### Passo 1 – Acessar o Google Colab

Acesse [Google Colab](https://colab.research.google.com/) e faça login com sua conta Google.

### Passo 2 – Abrir o notebook

No Google Colab, selecione a opção de upload e envie o arquivo `.ipynb` disponibilizado neste repositório.

### Passo 3 – Baixar o dataset

Acesse o [UCI Machine Learning Repository – Car Evaluation](https://archive.ics.uci.edu/dataset/19/car+evaluation) e faça o download do conjunto de dados.

Utilize o arquivo ZIP disponibilizado pela plataforma, mantendo seu nome como `car+evaluation.zip`.

### Passo 4 – Enviar o dataset para o Colab

No ambiente do Google Colab:

1. Abra a aba de arquivos, localizada na lateral esquerda.
2. Clique na opção de upload.
3. Envie o arquivo `car+evaluation.zip`.
4. Copie o caminho do arquivo enviado.
5. Confira se o caminho corresponde ao valor da variável `zip_path` na etapa de extração dos arquivos.

Caso necessário, ajuste a variável `zip_path` para corresponder à localização do arquivo no ambiente de execução.

### Passo 5 – Executar o notebook

Com o notebook e o dataset disponíveis, execute os blocos de código na ordem apresentada.

A execução pode ser realizada individualmente, utilizando o botão de execução de cada célula, ou por meio da opção **Executar tudo**.

### Passo 6 – Conferir os resultados

Ao finalizar a execução, serão apresentados:

- Informações gerais e estatísticas descritivas do dataset.
- Distribuição das classes.
- Transformações realizadas nos dados.
- Divisão dos conjuntos de treinamento, validação e teste.
- Configuração e treinamento do Random Forest.
- Acurácia e relatório de classificação da validação.
- Comparação com a classificação de referência.
- Acurácia e relatório de classificação do teste.
- Gráfico comparativo de desempenho.
- Matriz de confusão.
- Predição individual com probabilidades estimadas.
- Predição utilizando atributos informados manualmente.

Os resultados esperados são aproximadamente 96,91% de acurácia na validação e 96,54% no teste, considerando o mesmo conjunto de dados, as configurações utilizadas e versões compatíveis das bibliotecas.

## 7. Considerações finais

O desenvolvimento deste projeto permitiu aplicar, na prática, as principais etapas de uma esteira de aprendizado de máquina, desde a análise e preparação dos dados até o treinamento, a avaliação e a realização de previsões.

A utilização do algoritmo Random Forest apresentou resultados satisfatórios para o problema de classificação multiclasse proposto, alcançando uma acurácia de 96,54% no conjunto de teste.

A utilização da estratificação, do balanceamento dos pesos das classes e da integração do pré-processamento com o classificador contribuiu para uma abordagem organizada de desenvolvimento e avaliação do modelo.

O projeto demonstra a aplicação de técnicas de aprendizado de máquina em problemas de classificação, destacando a importância da preparação dos dados, da avaliação de desempenho e da interpretação dos resultados.

## 8. Referências

- [UCI Machine Learning Repository – Car Evaluation](https://archive.ics.uci.edu/dataset/19/car+evaluation)
- [Scikit-learn – Documentação oficial](https://scikit-learn.org/stable/)
- [Pandas – Documentação oficial](https://pandas.pydata.org/docs/)
- [Matplotlib – Documentação oficial](https://matplotlib.org/stable/)
- [Google Colab](https://colab.research.google.com/)
