# Documentação Completa - Ciência de Dados com Python

## Índice

1. [Introdução à Ciência de Dados](#1-introdução-à-ciência-de-dados)
2. [Python para Ciência de Dados](#2-python-para-ciência-de-dados)
3. [Bibliotecas Essenciais](#3-bibliotecas-essenciais)
4. [Manipulação de Dados](#4-manipulação-de-dados)
5. [Visualização de Dados](#5-visualização-de-dados)

---

## 1. Introdução à Ciência de Dados

### 1.1 O que é Ciência de Dados?

**Definição:** Ciência de Dados é uma disciplina interdisciplinar que combina estatística, programação, matemática e conhecimento de domínio para extrair insights significativos e conhecimento acionável de dados estruturados e não estruturados.

**Componentes Fundamentais:**

1. **Estatística e Matemática**
   - Base teórica para análise de dados
   - Inferência estatística e testes de hipóteses
   - Probabilidade e distribuições
   - Álgebra linear e cálculo

2. **Programação**
   - Automação de processos
   - Manipulação eficiente de dados
   - Implementação de algoritmos
   - Criação de pipelines de dados

3. **Conhecimento de Domínio**
   - Compreensão do contexto de negócio
   - Formulação de perguntas relevantes
   - Interpretação de resultados
   - Validação de insights

4. **Visualização e Comunicação**
   - Apresentação clara de resultados
   - Storytelling com dados
   - Dashboards e relatórios
   - Tradução técnica para não-técnicos

### 1.2 Tipos de Dados

#### Dados Estruturados
**Definição:** Dados organizados em formato tabular com esquema bem definido.

**Características:**
- Organizados em linhas e colunas
- Esquema fixo e predefinido
- Fáceis de consultar com SQL
- Armazenados em bancos de dados relacionais

**Exemplos:**
- Planilhas Excel
- Tabelas de bancos de dados
- Arquivos CSV
- Dados de sensores formatados

**Quando usar:**
- Análises transacionais
- Relatórios estruturados
- Análises quantitativas
- Séries temporais regulares

#### Dados Não Estruturados
**Definição:** Dados sem formato predefinido ou esquema fixo.

**Características:**
- Formato livre
- Difíceis de processar com ferramentas tradicionais
- Requerem técnicas especializadas de processamento
- Volume geralmente maior

**Exemplos:**
- Textos e documentos
- Imagens e vídeos
- Áudios e podcasts
- Posts em redes sociais
- E-mails

**Quando usar:**
- Análise de sentimento
- Reconhecimento de padrões
- Processamento de linguagem natural
- Visão computacional

#### Dados Semi-estruturados
**Definição:** Dados com alguma organização, mas sem esquema rígido.

**Exemplos:**
- JSON
- XML
- NoSQL databases
- Logs de sistema

### 1.3 O Pipeline de Ciência de Dados

```
Definição do Problema → Coleta → Limpeza → Exploração →
Modelagem → Validação → Deploy → Monitoramento
```

#### Fase 1: Definição do Problema
**O que é:** Estabelecer objetivos claros e mensuráveis para o projeto.

**Como fazer:**
1. Identificar o problema de negócio
2. Traduzir em problema analítico
3. Definir métricas de sucesso
4. Estabelecer restrições e requisitos

**Quando fazer:**
- Antes de iniciar qualquer análise
- Ao receber nova demanda
- Quando há mudanças no escopo

**Perguntas chave:**
- Qual problema estamos tentando resolver?
- Qual o impacto esperado?
- Quais são as métricas de sucesso?
- Quais dados estão disponíveis?

#### Fase 2: Coleta de Dados
**O que é:** Obtenção de dados relevantes de diversas fontes.

**Métodos de coleta:**

1. **APIs (Application Programming Interfaces)**
   - **Definição:** Interfaces para acesso programático a dados
   - **Quando usar:** Dados atualizados frequentemente, dados de terceiros
   - **Como usar:** Requisições HTTP, autenticação, rate limits
   - **Exemplo:** API do Twitter, Google Maps, dados financeiros

2. **Web Scraping**
   - **Definição:** Extração automatizada de dados de websites
   - **Quando usar:** Dados públicos não disponíveis via API
   - **Como usar:** BeautifulSoup, Selenium, Scrapy
   - **Cuidados:** Respeitar robots.txt, termos de uso, rate limiting

3. **Bancos de Dados**
   - **Definição:** Sistemas organizados de armazenamento de dados
   - **Tipos:** Relacionais (SQL), NoSQL, Data Warehouses
   - **Quando usar:** Dados corporativos, transações, históricos
   - **Como usar:** Queries SQL, ORM, conectores específicos

4. **Arquivos**
   - **Definição:** Dados armazenados em formatos de arquivo
   - **Formatos comuns:** CSV, Excel, JSON, Parquet, HDF5
   - **Quando usar:** Dados estáticos, compartilhamento, backups
   - **Como usar:** Pandas, readers específicos por formato

#### Fase 3: Limpeza de Dados
**O que é:** Processo de identificar e corrigir problemas nos dados para garantir qualidade e confiabilidade.

**Por que é importante:**
- 80% do tempo de um projeto de dados é gasto em limpeza
- Dados ruins levam a insights incorretos
- "Garbage in, garbage out"

**Problemas comuns:**

1. **Valores Ausentes (Missing Values)**

   **Definição:** Dados faltantes em observações.

   **Tipos:**
   - **MCAR (Missing Completely At Random):** Ausência aleatória
   - **MAR (Missing At Random):** Ausência relacionada a outras variáveis
   - **MNAR (Missing Not At Random):** Ausência relacionada ao próprio valor

   **Como tratar:**
   - Remoção (quando poucos casos)
   - Imputação com média/mediana (dados numéricos)
   - Imputação com moda (dados categóricos)
   - Imputação avançada (KNN, regressão)
   - Criar flag de ausência

   **Quando usar cada método:**
   - **Remoção:** < 5% de dados ausentes, MCAR
   - **Média/Mediana:** Dados numéricos, distribuição simétrica
   - **Moda:** Dados categóricos
   - **Avançada:** Dados complexos, muitos ausentes

2. **Duplicatas**

   **Definição:** Registros repetidos no dataset.

   **Como identificar:**
   - Verificar todas as colunas
   - Verificar subset de colunas chave
   - Considerar tolerância em valores numéricos

   **Como tratar:**
   - Remover duplicatas exatas
   - Agregar duplicatas parciais
   - Investigar causa raiz

3. **Outliers**

   **Definição:** Valores significativamente diferentes do padrão dos dados.

   **Como identificar:**
   - Método IQR (Interquartile Range)
   - Z-score (> 3 ou < -3)
   - Visualização (boxplot, scatter)
   - Isolation Forest

   **Como tratar:**
   - Remover (se erro de medição)
   - Manter (se legítimo)
   - Transformar (winsorização, log transform)
   - Investigar separadamente

   **Quando remover:**
   - Erros de entrada de dados
   - Erros de medição
   - Valores impossíveis

   **Quando manter:**
   - Eventos raros mas legítimos
   - Interesse específico em extremos
   - Amostras pequenas

4. **Inconsistências**

   **Tipos:**
   - Formatação (datas, números)
   - Nomenclatura (maiúsculas/minúsculas)
   - Unidades de medida
   - Codificação de categorias

   **Como tratar:**
   - Padronização de formatos
   - Normalização de textos
   - Conversão de unidades
   - Mapeamento de categorias

#### Fase 4: Exploração de Dados (EDA)
**O que é:** Análise investigativa dos dados para descobrir padrões, anomalias e testar hipóteses.

**Objetivos:**
1. Entender a estrutura dos dados
2. Identificar relações entre variáveis
3. Detectar padrões e tendências
4. Formular hipóteses
5. Validar suposições

**Técnicas:**

1. **Estatísticas Descritivas**

   **Medidas de Tendência Central:**
   - **Média:** Soma dividida pelo número de observações
     - Quando usar: Distribuição simétrica, sem outliers extremos
     - Limitação: Sensível a outliers

   - **Mediana:** Valor central quando dados ordenados
     - Quando usar: Distribuição assimétrica, presença de outliers
     - Vantagem: Robusta a valores extremos

   - **Moda:** Valor mais frequente
     - Quando usar: Dados categóricos, distribuições multimodais
     - Aplicação: Identificar padrões de comportamento

   **Medidas de Dispersão:**
   - **Variância:** Média dos quadrados dos desvios
     - Interpretação: Quão espalhados estão os dados
     - Unidade: Quadrado da unidade original

   - **Desvio Padrão:** Raiz quadrada da variância
     - Vantagem: Mesma unidade dos dados
     - Interpretação: Distância média da média

   - **Amplitude:** Diferença entre máximo e mínimo
     - Limitação: Sensível a outliers
     - Uso: Visão rápida do range

   - **IQR (Interquartile Range):** Q3 - Q1
     - Vantagem: Robusto a outliers
     - Uso: Identificação de outliers

2. **Análise Univariada**

   **Definição:** Análise de uma variável por vez.

   **Para variáveis numéricas:**
   - Histogramas: Visualizar distribuição
   - Box plots: Identificar quartis e outliers
   - Density plots: Suavização da distribuição
   - Q-Q plots: Verificar normalidade

   **Para variáveis categóricas:**
   - Tabelas de frequência
   - Gráficos de barras
   - Gráficos de pizza (usar com moderação)

3. **Análise Bivariada**

   **Definição:** Análise da relação entre duas variáveis.

   **Numérica vs Numérica:**
   - Scatter plots: Visualizar relação
   - Correlação de Pearson: Relação linear
   - Correlação de Spearman: Relação monotônica

   **Categórica vs Numérica:**
   - Box plots por categoria
   - Violin plots
   - Estatísticas por grupo

   **Categórica vs Categórica:**
   - Tabelas de contingência
   - Heatmaps de frequência
   - Teste qui-quadrado

4. **Análise Multivariada**

   **Definição:** Análise de múltiplas variáveis simultaneamente.

   **Técnicas:**
   - Matriz de correlação
   - Pair plots
   - PCA (Principal Component Analysis)
   - Cluster analysis

#### Fase 5: Modelagem
**O que é:** Aplicação de algoritmos para aprender padrões dos dados e fazer predições.

**Tipos de problemas:**

1. **Supervisionado**
   - **Definição:** Aprendizado com dados rotulados
   - **Quando usar:** Temos exemplos de entrada e saída

   **Subtipos:**
   - **Classificação:** Predizer categoria
     - Binária: Sim/Não, Spam/Ham
     - Multiclasse: Tipo de produto, sentimento

   - **Regressão:** Predizer valor contínuo
     - Linear: Relação linear
     - Não-linear: Relações complexas

2. **Não Supervisionado**
   - **Definição:** Aprendizado sem rótulos
   - **Quando usar:** Descobrir estruturas ocultas

   **Subtipos:**
   - **Clustering:** Agrupar observações similares
   - **Redução de dimensionalidade:** Simplificar dados
   - **Detecção de anomalias:** Identificar padrões incomuns

3. **Semi-supervisionado**
   - **Definição:** Combinação de dados rotulados e não rotulados
   - **Quando usar:** Poucos dados rotulados disponíveis

#### Fase 6: Validação
**O que é:** Avaliação do desempenho e confiabilidade do modelo.

**Técnicas:**

1. **Holdout Method**
   - Dividir dados em treino e teste
   - Simples e rápido
   - Pode ser instável com amostras pequenas

2. **Cross-Validation**
   - K-Fold: Dividir em K partes
   - Mais robusto que holdout
   - Maior custo computacional

3. **Métricas de Avaliação**

   **Classificação:**
   - Acurácia, Precisão, Recall, F1-Score
   - Matriz de confusão
   - ROC-AUC

   **Regressão:**
   - MAE, MSE, RMSE
   - R², R² Ajustado
   - MAPE

---

## 2. Python para Ciência de Dados

### 2.1 Por que Python?

**Vantagens:**

1. **Sintaxe Clara e Intuitiva**
   - Código legível como pseudocódigo
   - Curva de aprendizado suave
   - Manutenção facilitada

2. **Ecossistema Rico**
   - Mais de 300.000 pacotes no PyPI
   - Bibliotecas especializadas para cada tarefa
   - Integração entre ferramentas

3. **Comunidade Ativa**
   - Grande base de usuários
   - Suporte em fóruns e comunidades
   - Documentação extensa
   - Tutoriais e cursos abundantes

4. **Versatilidade**
   - Prototipação rápida
   - Produção escalável
   - Integração com outras linguagens
   - Deploy em diversas plataformas

5. **Gratuito e Open Source**
   - Sem custos de licença
   - Código-fonte disponível
   - Modificável conforme necessidade

### 2.2 Estruturas de Dados Fundamentais

#### Listas

**Definição:** Coleção ordenada e mutável de elementos.

**Características:**
- Ordenada: Mantém ordem de inserção
- Mutável: Pode ser modificada após criação
- Heterogênea: Pode conter diferentes tipos
- Indexada: Acesso por posição (0-based)

**Quando usar:**
- Armazenar sequências de elementos
- Ordem importa
- Necessidade de modificação
- Elementos duplicados são permitidos

**Como usar:**
```python
# Criação
lista = [1, 2, 3, 4, 5]
lista_mista = [1, "texto", 3.14, True]

# Acesso
primeiro = lista[0]      # Primeiro elemento
ultimo = lista[-1]       # Último elemento
fatiamento = lista[1:4]  # Elementos de índice 1 a 3

# Modificação
lista.append(6)          # Adicionar ao final
lista.insert(0, 0)       # Inserir em posição
lista.remove(3)          # Remover elemento
lista.pop()              # Remover e retornar último

# Operações
tamanho = len(lista)     # Comprimento
existe = 3 in lista      # Verificar existência
lista.sort()             # Ordenar in-place
nova = sorted(lista)     # Retornar lista ordenada
```

**List Comprehension:**

**Definição:** Forma concisa de criar listas baseadas em iterações.

**Quando usar:**
- Transformar elementos de uma lista
- Filtrar elementos
- Criar listas de forma mais legível

**Sintaxe:**
```python
# Forma básica
[expressão for item in iterável]

# Com condição
[expressão for item in iterável if condição]

# Aninhada
[expressão for item1 in iterável1 for item2 in iterável2]
```

**Exemplos:**
```python
# Quadrados de 0 a 9
quadrados = [x**2 for x in range(10)]

# Números pares
pares = [x for x in range(20) if x % 2 == 0]

# Matriz
matriz = [[i*j for j in range(5)] for i in range(5)]

# Processar strings
nomes = ["alice", "bob", "charlie"]
maiusculas = [nome.upper() for nome in nomes]
```

#### Tuplas

**Definição:** Coleção ordenada e imutável de elementos.

**Características:**
- Ordenada: Mantém ordem
- Imutável: Não pode ser modificada
- Heterogênea: Diferentes tipos
- Hashable: Pode ser chave de dicionário

**Quando usar:**
- Dados que não devem mudar
- Retornar múltiplos valores de função
- Chaves de dicionário
- Melhor performance que listas (imutável)

**Como usar:**
```python
# Criação
tupla = (1, 2, 3)
coordenada = (10.5, 20.3)
single = (1,)  # Note a vírgula

# Unpacking
x, y = coordenada
a, b, c = (1, 2, 3)
primeiro, *resto = (1, 2, 3, 4, 5)

# Acesso
elemento = tupla[0]
fatia = tupla[1:3]

# Operações
tamanho = len(tupla)
concatenada = tupla + (4, 5)
repetida = tupla * 3
```

**Quando usar tupla vs lista:**
- **Tupla:** Dados imutáveis, coordenadas, configurações, chaves
- **Lista:** Dados mutáveis, coleções dinâmicas, necessidade de ordenação

#### Dicionários

**Definição:** Coleção de pares chave-valor, não ordenada (Python 3.7+ mantém ordem de inserção).

**Características:**
- Mutável: Pode ser modificado
- Chaves únicas: Não permite duplicatas
- Acesso rápido: O(1) em média
- Chaves hashable: Imutáveis (string, número, tupla)

**Quando usar:**
- Mapear relacionamentos chave-valor
- Lookup rápido
- Contagem de frequências
- Configurações e parâmetros
- Armazenar dados estruturados

**Como usar:**
```python
# Criação
pessoa = {
    'nome': 'Ana',
    'idade': 28,
    'cidade': 'São Paulo'
}

# Acesso
nome = pessoa['nome']           # Erro se não existir
idade = pessoa.get('idade')     # None se não existir
idade = pessoa.get('peso', 0)   # Valor padrão

# Modificação
pessoa['email'] = 'ana@email.com'  # Adicionar/modificar
del pessoa['cidade']                # Remover
removido = pessoa.pop('idade')      # Remover e retornar

# Operações
chaves = pessoa.keys()
valores = pessoa.values()
itens = pessoa.items()
existe = 'nome' in pessoa

# Iteração
for chave in pessoa:
    print(chave, pessoa[chave])

for chave, valor in pessoa.items():
    print(f"{chave}: {valor}")
```

**Dict Comprehension:**
```python
# Criar dicionário
quadrados = {x: x**2 for x in range(5)}

# Inverter dicionário
invertido = {v: k for k, v in original.items()}

# Filtrar
maiores = {k: v for k, v in dados.items() if v > 10}
```

#### Sets (Conjuntos)

**Definição:** Coleção não ordenada de elementos únicos.

**Características:**
- Não ordenado: Sem índice
- Elementos únicos: Remove duplicatas automaticamente
- Mutável: Pode adicionar/remover
- Elementos hashable: Imutáveis

**Quando usar:**
- Remover duplicatas
- Testes de pertinência rápidos
- Operações de conjunto (união, interseção)
- Quando ordem não importa

**Como usar:**
```python
# Criação
conjunto = {1, 2, 3, 4, 5}
vazio = set()  # {} cria dicionário vazio
de_lista = set([1, 2, 2, 3, 3, 3])  # {1, 2, 3}

# Operações de conjunto
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

uniao = a | b              # {1, 2, 3, 4, 5, 6}
intersecao = a & b         # {3, 4}
diferenca = a - b          # {1, 2}
diff_simetrica = a ^ b     # {1, 2, 5, 6}

# Modificação
conjunto.add(6)
conjunto.remove(3)         # Erro se não existir
conjunto.discard(3)        # Sem erro
conjunto.clear()

# Testes
existe = 3 in conjunto
subconjunto = a <= b
superconjunto = a >= b
```

### 2.3 Funções

**Definição:** Bloco de código reutilizável que realiza uma tarefa específica.

**Por que usar funções:**
1. **Reutilização:** Evitar repetição de código
2. **Modularização:** Dividir problemas complexos
3. **Manutenção:** Facilitar alterações
4. **Legibilidade:** Código mais claro
5. **Testabilidade:** Facilitar testes

**Estrutura básica:**
```python
def nome_da_funcao(parametros):
    """
    Docstring: Descreve o que a função faz
    """
    # Corpo da função
    return resultado
```

**Tipos de argumentos:**

1. **Posicionais:**
```python
def somar(a, b):
    return a + b

resultado = somar(5, 3)  # a=5, b=3
```

2. **Nomeados (Keyword):**
```python
resultado = somar(a=5, b=3)
resultado = somar(b=3, a=5)  # Ordem não importa
```

3. **Padrão:**
```python
def saudar(nome, saudacao="Olá"):
    return f"{saudacao}, {nome}!"

print(saudar("Ana"))              # Usa padrão
print(saudar("Ana", "Bom dia"))  # Sobrescreve
```

4. **Args variáveis:**
```python
def somar_todos(*numeros):
    return sum(numeros)

total = somar_todos(1, 2, 3, 4, 5)
```

5. **Kwargs variáveis:**
```python
def criar_perfil(**dados):
    for chave, valor in dados.items():
        print(f"{chave}: {valor}")

criar_perfil(nome="Ana", idade=28, cidade="SP")
```

**Funções Lambda:**

**Definição:** Funções anônimas de uma linha.

**Quando usar:**
- Funções simples e curtas
- Uso com map, filter, reduce
- Callbacks
- Quando não precisa de nome

**Sintaxe:**
```python
lambda argumentos: expressão
```

**Exemplos:**
```python
# Função simples
dobro = lambda x: x * 2
print(dobro(5))  # 10

# Múltiplos argumentos
soma = lambda a, b: a + b
print(soma(3, 4))  # 7

# Com map
numeros = [1, 2, 3, 4, 5]
dobrados = list(map(lambda x: x * 2, numeros))

# Com filter
pares = list(filter(lambda x: x % 2 == 0, numeros))

# Com sorted
pessoas = [('Ana', 25), ('Bruno', 30), ('Carlos', 20)]
ordenado = sorted(pessoas, key=lambda x: x[1])
```

**Quando NÃO usar lambda:**
- Lógica complexa
- Múltiplas linhas
- Necessidade de documentação
- Reutilização em vários lugares

### 2.4 Programação Funcional

**Map:**

**Definição:** Aplica uma função a cada elemento de um iterável.

**Quando usar:**
- Transformar todos os elementos
- Aplicar mesma operação em lista
- Alternativa a list comprehension

**Sintaxe:**
```python
map(funcao, iteravel)
```

**Exemplos:**
```python
# Elevar ao quadrado
numeros = [1, 2, 3, 4, 5]
quadrados = list(map(lambda x: x**2, numeros))

# Converter para maiúsculas
nomes = ["ana", "bruno", "carlos"]
maiusculas = list(map(str.upper, nomes))

# Múltiplos iteráveis
a = [1, 2, 3]
b = [10, 20, 30]
soma = list(map(lambda x, y: x + y, a, b))
```

**Filter:**

**Definição:** Filtra elementos baseado em condição.

**Quando usar:**
- Selecionar elementos que atendem critério
- Remover elementos indesejados
- Alternativa a list comprehension com if

**Sintaxe:**
```python
filter(funcao, iteravel)
```

**Exemplos:**
```python
# Números pares
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
pares = list(filter(lambda x: x % 2 == 0, numeros))

# Strings não vazias
palavras = ["", "python", "", "data", "science"]
nao_vazias = list(filter(None, palavras))

# Filtrar por condição complexa
pessoas = [
    {'nome': 'Ana', 'idade': 25},
    {'nome': 'Bruno', 'idade': 30},
    {'nome': 'Carlos', 'idade': 20}
]
maiores_25 = list(filter(lambda p: p['idade'] > 25, pessoas))
```

**Reduce:**

**Definição:** Aplica função de forma cumulativa aos elementos.

**Quando usar:**
- Agregar elementos em único valor
- Cálculos acumulativos
- Implementar operações complexas

**Sintaxe:**
```python
from functools import reduce
reduce(funcao, iteravel, inicial)
```

**Exemplos:**
```python
from functools import reduce

# Somar todos
numeros = [1, 2, 3, 4, 5]
soma = reduce(lambda x, y: x + y, numeros)  # 15

# Produto
produto = reduce(lambda x, y: x * y, numeros)  # 120

# Máximo
maximo = reduce(lambda x, y: x if x > y else y, numeros)

# Concatenar strings
palavras = ["Python", "é", "incrível"]
frase = reduce(lambda x, y: x + " " + y, palavras)
```

---

## 3. Bibliotecas Essenciais

### 3.1 NumPy - Computação Numérica

**Definição:** Biblioteca fundamental para computação científica em Python, fornecendo arrays multidimensionais eficientes e funções matemáticas.

**Por que NumPy é importante:**

1. **Performance**
   - Implementado em C
   - 10-100x mais rápido que listas Python
   - Operações vetorizadas

2. **Eficiência de memória**
   - Arrays são contíguos na memória
   - Menor overhead que listas
   - Tipos de dados específicos

3. **Funcionalidade**
   - Álgebra linear
   - Transformadas de Fourier
   - Números aleatórios
   - Operações estatísticas

**Quando usar NumPy:**
- Operações matemáticas em arrays
- Processamento de dados numéricos
- Base para outras bibliotecas (Pandas, Scikit-learn)
- Quando performance é crítica

**Arrays NumPy vs Listas Python:**

| Característica | NumPy Array | Lista Python |
|---|---|---|
| Velocidade | Muito rápido | Lento |
| Memória | Eficiente | Maior overhead |
| Tipo de dados | Homogêneo | Heterogêneo |
| Operações | Vetorizadas | Loop necessário |
| Dimensões | Multidimensional | 1D (nested para mais) |

**Conceitos fundamentais:**

#### ndarray (N-dimensional array)

**Definição:** Estrutura de dados central do NumPy, array multidimensional homogêneo.

**Atributos importantes:**
```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])

arr.shape      # (2, 3) - dimensões
arr.ndim       # 2 - número de dimensões
arr.size       # 6 - total de elementos
arr.dtype      # dtype('int64') - tipo de dados
arr.itemsize   # 8 - tamanho em bytes de cada elemento
```

**Criação de arrays:**

1. **A partir de listas:**
```python
# 1D
arr1d = np.array([1, 2, 3, 4, 5])

# 2D
arr2d = np.array([[1, 2, 3], [4, 5, 6]])

# 3D
arr3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
```

2. **Arrays especiais:**
```python
# Zeros
zeros = np.zeros((3, 4))           # Array 3x4 de zeros
zeros_like = np.zeros_like(arr)    # Mesmo shape que arr

# Uns
ones = np.ones((2, 3))             # Array 2x3 de uns
ones_like = np.ones_like(arr)

# Identidade
identidade = np.eye(4)             # Matriz identidade 4x4
diagonal = np.identity(3)          # Mesma coisa

# Vazio (não inicializado)
vazio = np.empty((2, 3))           # Valores aleatórios da memória

# Constante
constante = np.full((3, 3), 7)     # Array 3x3 preenchido com 7
```

3. **Sequências:**
```python
# Range
arange = np.arange(0, 10, 2)       # [0, 2, 4, 6, 8]
arange_float = np.arange(0, 1, 0.1)

# Espaçamento linear
linspace = np.linspace(0, 1, 5)    # 5 valores entre 0 e 1
# [0.  , 0.25, 0.5 , 0.75, 1.  ]

# Espaçamento logarítmico
logspace = np.logspace(0, 2, 5)    # 5 valores de 10^0 a 10^2
```

4. **Arrays aleatórios:**
```python
# Uniforme [0, 1)
uniform = np.random.rand(3, 4)

# Normal padrão
normal = np.random.randn(3, 4)

# Inteiros aleatórios
integers = np.random.randint(0, 10, size=(3, 4))

# Escolha aleatória
choice = np.random.choice([1, 2, 3, 4, 5], size=10)

# Seed para reproducibilidade
np.random.seed(42)
```

#### Operações Vetorizadas

**Definição:** Operações aplicadas elemento a elemento sem loops explícitos.

**Por que são importantes:**
- Muito mais rápidas que loops Python
- Código mais conciso e legível
- Aproveitam otimizações de baixo nível

**Operações básicas:**
```python
a = np.array([1, 2, 3, 4, 5])
b = np.array([10, 20, 30, 40, 50])

# Aritméticas
soma = a + b          # [11, 22, 33, 44, 55]
diferenca = a - b     # [-9, -18, -27, -36, -45]
produto = a * b       # [10, 40, 90, 160, 250]
divisao = b / a       # [10, 10, 10, 10, 10]
potencia = a ** 2     # [1, 4, 9, 16, 25]

# Com escalares
multiplicado = a * 2  # [2, 4, 6, 8, 10]
somado = a + 10       # [11, 12, 13, 14, 15]

# Comparações
maior = a > 3         # [False, False, False, True, True]
igual = a == 3        # [False, False, True, False, False]
```

**Broadcasting:**

**Definição:** Mecanismo que permite operações entre arrays de shapes diferentes.

**Regras:**
1. Se arrays têm diferentes números de dimensões, o de menor dimensão é preenchido com 1s à esquerda
2. Arrays são compatíveis em uma dimensão se forem iguais ou um deles for 1
3. Após broadcasting, cada array se comporta como se tivesse o shape máximo

**Exemplos:**
```python
# Escalar com array
a = np.array([1, 2, 3])
b = 2
resultado = a * b  # [2, 4, 6]

# 1D com 2D
a = np.array([1, 2, 3])        # shape (3,)
b = np.array([[1], [2], [3]])  # shape (3, 1)
resultado = a + b              # shape (3, 3)
# [[2, 3, 4],
#  [3, 4, 5],
#  [4, 5, 6]]

# Aplicação prática: normalização
dados = np.random.rand(100, 5)
media = dados.mean(axis=0)     # shape (5,)
std = dados.std(axis=0)        # shape (5,)
normalizados = (dados - media) / std  # Broadcasting
```

#### Indexação e Fatiamento

**1. Indexação Básica:**
```python
arr = np.array([10, 20, 30, 40, 50])

# Acessar elemento
primeiro = arr[0]      # 10
ultimo = arr[-1]       # 50

# 2D
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
elemento = arr2d[1, 2]  # 6 (linha 1, coluna 2)
linha = arr2d[1]        # [4, 5, 6]
coluna = arr2d[:, 1]    # [2, 5, 8]
```

**2. Slicing (Fatiamento):**
```python
arr = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

# [start:stop:step]
fatia = arr[2:7]       # [2, 3, 4, 5, 6]
cada_dois = arr[::2]   # [0, 2, 4, 6, 8]
reverso = arr[::-1]    # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

# 2D
arr2d = np.arange(12).reshape(3, 4)
sub = arr2d[0:2, 1:3]  # Linhas 0-1, Colunas 1-2
```

**3. Indexação Booleana:**

**Definição:** Usar array booleano para selecionar elementos.

**Quando usar:**
- Filtrar dados por condição
- Selecionar subset baseado em critérios
- Máscara condicional

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Criar máscara
mascara = arr > 5      # [False, False, False, False, False, True, ...]
maiores_5 = arr[mascara]  # [6, 7, 8, 9, 10]

# Direto
pares = arr[arr % 2 == 0]  # [2, 4, 6, 8, 10]

# Múltiplas condições
entre = arr[(arr > 3) & (arr < 8)]  # [4, 5, 6, 7]

# Modificar com máscara
arr[arr > 5] = 99  # Substitui valores > 5 por 99
```

**4. Fancy Indexing:**

**Definição:** Usar array de índices para selecionar elementos.

```python
arr = np.array([10, 20, 30, 40, 50])

# Array de índices
indices = [0, 2, 4]
selecionados = arr[indices]  # [10, 30, 50]

# 2D
arr2d = np.arange(12).reshape(3, 4)
linhas = [0, 2]
colunas = [1, 3]
elementos = arr2d[linhas, colunas]  # [arr2d[0,1], arr2d[2,3]]
```

#### Operações Estatísticas

**Funções básicas:**
```python
arr = np.random.randn(1000)

# Tendência central
media = np.mean(arr)
mediana = np.median(arr)

# Dispersão
variancia = np.var(arr)
desvio_padrao = np.std(arr)

# Extremos
minimo = np.min(arr)
maximo = np.max(arr)
amplitude = np.ptp(arr)  # Peak to peak

# Percentis
q25 = np.percentile(arr, 25)
q50 = np.percentile(arr, 50)
q75 = np.percentile(arr, 75)

# Agregação
soma = np.sum(arr)
produto = np.prod(arr)
```

**Operações por eixo:**

**Conceito de eixo (axis):**
- axis=0: Ao longo das linhas (colunas resultantes)
- axis=1: Ao longo das colunas (linhas resultantes)
- axis=None: Todo o array

```python
arr2d = np.array([[1, 2, 3], [4, 5, 6]])

# Soma
soma_total = np.sum(arr2d)          # 21
soma_colunas = np.sum(arr2d, axis=0)  # [5, 7, 9]
soma_linhas = np.sum(arr2d, axis=1)   # [6, 15]

# Média
media_colunas = np.mean(arr2d, axis=0)  # [2.5, 3.5, 4.5]
media_linhas = np.mean(arr2d, axis=1)   # [2, 5]

# Máximo e mínimo
max_colunas = np.max(arr2d, axis=0)  # [4, 5, 6]
min_linhas = np.min(arr2d, axis=1)   # [1, 4]

# Índices de máximo e mínimo
idx_max = np.argmax(arr2d)           # 5 (índice no array achatado)
idx_max_colunas = np.argmax(arr2d, axis=0)  # [1, 1, 1]
```

#### Álgebra Linear

**Multiplicação de vetores e matrizes:**
```python
# Produto escalar (dot product)
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
dot = np.dot(a, b)  # 1*4 + 2*5 + 3*6 = 32

# Produto de matrizes
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
produto = np.dot(A, B)  # ou A @ B (Python 3.5+)
# [[19, 22],
#  [43, 50]]

# Produto elemento a elemento (Hadamard)
hadamard = A * B
# [[5, 12],
#  [21, 32]]
```

**Operações matriciais:**
```python
A = np.array([[1, 2], [3, 4]])

# Transposta
A_T = A.T
# [[1, 3],
#  [2, 4]]

# Determinante
det = np.linalg.det(A)  # -2.0

# Inversa
inv = np.linalg.inv(A)
# [[-2. ,  1. ],
#  [ 1.5, -0.5]]

# Verificar: A @ inv deve ser identidade
identidade = A @ inv

# Traço (soma diagonal)
trace = np.trace(A)  # 5

# Posto (rank)
rank = np.linalg.matrix_rank(A)

# Autovalores e autovetores
autovalores, autovetores = np.linalg.eig(A)
```

**Resolver sistemas lineares:**

**Problema:** Ax = b

```python
# Sistema: 3x + y = 9
#         x + 2y = 8

A = np.array([[3, 1], [1, 2]])
b = np.array([9, 8])

# Solução
x = np.linalg.solve(A, b)  # [2, 3]

# Verificação
verificacao = A @ x  # Deve ser igual a b
```

### 3.2 Pandas - Manipulação de Dados

**Definição:** Biblioteca para manipulação e análise de dados estruturados, fornecendo estruturas DataFrame e Series.

**Por que Pandas é essencial:**

1. **Facilidade de uso**
   - API intuitiva
   - Integração com NumPy
   - Sintaxe expressiva

2. **Funcionalidade rica**
   - Leitura/escrita de múltiplos formatos
   - Limpeza e transformação
   - Agrupamento e agregação
   - Time series

3. **Performance**
   - Operações vetorizadas
   - Implementações otimizadas em Cython
   - Uso eficiente de memória

**Estruturas de dados principais:**

#### Series

**Definição:** Array unidimensional rotulado, similar a uma coluna de planilha.

**Características:**
- 1D labeled array
- Pode conter qualquer tipo de dado
- Tem índice (labels)
- Similar a dicionário

**Quando usar:**
- Representar uma única variável
- Operações em uma dimensão
- Time series simples

**Como usar:**
```python
import pandas as pd

# Criação
s = pd.Series([1, 2, 3, 4, 5])

# Com índice customizado
s = pd.Series([10, 20, 30], index=['a', 'b', 'c'])

# De dicionário
s = pd.Series({'a': 1, 'b': 2, 'c': 3})

# Acesso
print(s[0])      # Por posição
print(s['a'])    # Por label
print(s.iloc[0]) # Explicitamente por posição
print(s.loc['a']) # Explicitamente por label

# Atributos
print(s.index)   # Index(['a', 'b', 'c'])
print(s.values)  # array([1, 2, 3])
print(s.dtype)   # dtype('int64')

# Operações
print(s + 10)    # Adiciona 10 a todos
print(s * 2)     # Multiplica todos por 2
print(s[s > 1])  # Filtra valores > 1
```

#### DataFrame

**Definição:** Estrutura bidimensional rotulada com colunas potencialmente de diferentes tipos.

**Características:**
- Tabela 2D
- Colunas podem ter tipos diferentes
- Índice para linhas e colunas
- Similar a planilha ou tabela SQL

**Quando usar:**
- Dados tabulares
- Múltiplas variáveis
- Análise de dados estruturados

**Como criar:**
```python
# De dicionário
df = pd.DataFrame({
    'nome': ['Ana', 'Bruno', 'Carlos'],
    'idade': [25, 30, 35],
    'cidade': ['SP', 'RJ', 'BH']
})

# De listas
dados = [
    ['Ana', 25, 'SP'],
    ['Bruno', 30, 'RJ'],
    ['Carlos', 35, 'BH']
]
df = pd.DataFrame(dados, columns=['nome', 'idade', 'cidade'])

# De array NumPy
arr = np.random.rand(3, 4)
df = pd.DataFrame(arr, columns=['A', 'B', 'C', 'D'])

# Ler de arquivo
df = pd.read_csv('dados.csv')
df = pd.read_excel('dados.xlsx')
df = pd.read_json('dados.json')
```

**Inspeção de dados:**
```python
# Visualização
df.head()        # Primeiras 5 linhas
df.head(10)      # Primeiras 10 linhas
df.tail()        # Últimas 5 linhas
df.sample(5)     # 5 linhas aleatórias

# Informações
df.info()        # Resumo geral
df.describe()    # Estatísticas descritivas
df.shape         # (linhas, colunas)
df.columns       # Nomes das colunas
df.dtypes        # Tipos de dados
df.index         # Índice

# Valores
df.values        # Array NumPy dos valores
df.to_numpy()    # Mesmo que values
```

**Seleção de dados:**

**1. Seleção de colunas:**
```python
# Uma coluna (retorna Series)
idade = df['idade']
idade = df.idade  # Notação de atributo (evite se nome tem espaços)

# Múltiplas colunas (retorna DataFrame)
subset = df[['nome', 'idade']]

# Todas exceto algumas
sem_idade = df.drop('idade', axis=1)
sem_varias = df.drop(['idade', 'cidade'], axis=1)
```

**2. Seleção de linhas:**
```python
# Por índice numérico
primeiras = df.iloc[0:3]      # Linhas 0, 1, 2
linha = df.iloc[0]            # Primeira linha
ultimas = df.iloc[-3:]        # Últimas 3 linhas

# Por label
linha = df.loc[0]             # Linha com índice 0
intervalo = df.loc[0:2]       # Índices 0, 1, 2 (inclusivo)

# Por condição
maiores_30 = df[df['idade'] > 30]
sp = df[df['cidade'] == 'SP']

# Múltiplas condições
criterio = df[(df['idade'] > 25) & (df['cidade'] == 'SP')]
ou = df[(df['idade'] < 20) | (df['cidade'] == 'RJ')]
```

**3. Seleção combinada:**
```python
# loc[linhas, colunas]
valor = df.loc[0, 'nome']              # Valor específico
subset = df.loc[0:2, ['nome', 'idade']] # Subset

# iloc[linhas, colunas]
valor = df.iloc[0, 0]                  # Primeira linha, primeira coluna
subset = df.iloc[0:2, 0:2]             # Subset por posição

# Condicional + colunas
subset = df.loc[df['idade'] > 25, ['nome', 'cidade']]
```

**Manipulação de dados:**

**1. Adicionar colunas:**
```python
# Nova coluna constante
df['pais'] = 'Brasil'

# Calculada de outras colunas
df['idade_meses'] = df['idade'] * 12

# Condicional
df['faixa'] = df['idade'].apply(lambda x: 'Jovem' if x < 30 else 'Adulto')

# Múltiplas condições
def classificar(idade):
    if idade < 20:
        return 'Jovem'
    elif idade < 40:
        return 'Adulto'
    else:
        return 'Senior'

df['categoria'] = df['idade'].apply(classificar)
```

**2. Modificar colunas:**
```python
# Sobrescrever
df['idade'] = df['idade'] + 1

# Modificar com condição
df.loc[df['idade'] > 30, 'idade'] = 30

# Renomear
df = df.rename(columns={'idade': 'Idade', 'nome': 'Nome'})

# Mudar tipo
df['idade'] = df['idade'].astype(float)
df['nome'] = df['nome'].astype(str)
```

**3. Remover:**
```python
# Colunas
df = df.drop('idade', axis=1)
df = df.drop(['idade', 'cidade'], axis=1)

# Linhas
df = df.drop(0)                  # Por índice
df = df.drop([0, 1, 2])          # Múltiplas
df = df[df['idade'] > 25]        # Por condição
```

**Tratamento de valores ausentes:**

**Identificar:**
```python
# Verificar nulos
df.isnull()           # DataFrame booleano
df.isna()             # Alias de isnull
df.isnull().sum()     # Contar por coluna
df.isnull().sum().sum()  # Total de nulos

# Verificar não-nulos
df.notnull()
df.notna()

# Linhas com algum nulo
df[df.isnull().any(axis=1)]

# Linhas sem nulos
df[df.notnull().all(axis=1)]
```

**Remover:**
```python
# Remover linhas com qualquer nulo
df_sem_nulos = df.dropna()

# Remover linhas onde todas as colunas são nulas
df = df.dropna(how='all')

# Remover apenas se colunas específicas têm nulos
df = df.dropna(subset=['idade', 'nome'])

# Remover colunas com nulos
df = df.dropna(axis=1)

# Threshold: manter linhas com pelo menos N não-nulos
df = df.dropna(thresh=2)
```

**Preencher:**
```python
# Com valor constante
df['idade'] = df['idade'].fillna(0)
df = df.fillna(0)  # Todas as colunas

# Com estatística
df['idade'] = df['idade'].fillna(df['idade'].mean())
df['idade'] = df['idade'].fillna(df['idade'].median())
df['categoria'] = df['categoria'].fillna(df['categoria'].mode()[0])

# Forward fill (propagar último valor válido)
df = df.fillna(method='ffill')

# Backward fill (usar próximo valor válido)
df = df.fillna(method='bfill')

# Interpolação
df['valor'] = df['valor'].interpolate()
df['valor'] = df['valor'].interpolate(method='linear')
```

**Agrupamento e Agregação:**

**GroupBy:**

**Definição:** Dividir dados em grupos baseado em critério, aplicar função a cada grupo e combinar resultados.

**Processo (Split-Apply-Combine):**
1. **Split:** Dividir DataFrame em grupos
2. **Apply:** Aplicar função a cada grupo
3. **Combine:** Combinar resultados

**Quando usar:**
- Análises por categoria
- Estatísticas por grupo
- Agregações complexas
- Pivot tables

```python
# Agrupar por uma coluna
por_cidade = df.groupby('cidade')

# Ver grupos
print(por_cidade.groups)

# Estatística simples
media_idade = por_cidade['idade'].mean()
max_idade = por_cidade['idade'].max()
contagem = por_cidade.size()

# Múltiplas agregações
estatisticas = por_cidade['idade'].agg(['mean', 'min', 'max', 'std'])

# Diferentes agregações por coluna
resultado = por_cidade.agg({
    'idade': ['mean', 'min', 'max'],
    'salario': ['sum', 'mean']
})

# Múltiplas colunas de agrupamento
por_cidade_genero = df.groupby(['cidade', 'genero'])
media = por_cidade_genero['salario'].mean()

# Função customizada
def amplitude(x):
    return x.max() - x.min()

amplitudes = por_cidade['idade'].agg(amplitude)

# Transformação (mantém shape original)
normalized = por_cidade['idade'].transform(lambda x: (x - x.mean()) / x.std())
```

**Pivot Tables:**

**Definição:** Tabela de resumo que agrupa dados e aplica função de agregação.

**Quando usar:**
- Criar tabelas de resumo
- Análise multidimensional
- Relatórios executivos

```python
# Pivot table básica
pivot = pd.pivot_table(
    df,
    values='salario',      # Coluna a agregar
    index='cidade',         # Linhas
    columns='genero',       # Colunas
    aggfunc='mean'          # Função de agregação
)

# Múltiplas agregações
pivot = pd.pivot_table(
    df,
    values='salario',
    index='cidade',
    columns='genero',
    aggfunc=['mean', 'sum', 'count']
)

# Múltiplos índices e colunas
pivot = pd.pivot_table(
    df,
    values='salario',
    index=['cidade', 'departamento'],
    columns=['genero', 'faixa_etaria'],
    aggfunc='mean',
    fill_value=0,           # Preencher nulos
    margins=True            # Adicionar totais
)
```

**Merge e Join:**

**Definição:** Combinar DataFrames baseado em colunas ou índices comuns.

**Tipos de join:**
- **Inner:** Apenas matches (interseção)
- **Left:** Todos da esquerda + matches
- **Right:** Todos da direita + matches
- **Outer:** Todos de ambos (união)

**Quando usar:**
- Combinar dados de diferentes fontes
- Enriquecer dataset
- Relacionamentos tipo SQL

```python
df1 = pd.DataFrame({
    'id': [1, 2, 3],
    'nome': ['Ana', 'Bruno', 'Carlos']
})

df2 = pd.DataFrame({
    'id': [1, 2, 4],
    'salario': [3000, 4000, 5000]
})

# Inner join (padrão)
inner = pd.merge(df1, df2, on='id')
# Resultado: id 1 e 2 (interseção)

# Left join
left = pd.merge(df1, df2, on='id', how='left')
# Resultado: todos de df1, salario NaN para id 3

# Right join
right = pd.merge(df1, df2, on='id', how='right')
# Resultado: todos de df2, nome NaN para id 4

# Outer join
outer = pd.merge(df1, df2, on='id', how='outer')
# Resultado: todos os ids (1, 2, 3, 4)

# Diferentes nomes de coluna
df3 = pd.DataFrame({
    'pessoa_id': [1, 2, 4],
    'departamento': ['TI', 'RH', 'Vendas']
})

merged = pd.merge(df1, df3, left_on='id', right_on='pessoa_id')

# Múltiplas colunas
merged = pd.merge(df1, df2, on=['id', 'nome'])

# Sufixos para colunas duplicadas
merged = pd.merge(df1, df2, on='id', suffixes=('_esq', '_dir'))
```

**Concatenação:**

**Definição:** Empilhar DataFrames ao longo de um eixo.

**Quando usar:**
- Combinar datasets similares
- Adicionar mais observações
- Adicionar mais variáveis

```python
df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [5, 6], 'B': [7, 8]})

# Concatenar verticalmente (empilhar linhas)
vertical = pd.concat([df1, df2])
vertical = pd.concat([df1, df2], ignore_index=True)  # Resetar índice

# Concatenar horizontalmente (adicionar colunas)
horizontal = pd.concat([df1, df2], axis=1)

# Lidar com colunas diferentes
df3 = pd.DataFrame({'C': [9, 10], 'D': [11, 12]})
combined = pd.concat([df1, df3], axis=1)  # NaN nas não existentes
```

---

## 4. Manipulação de Dados

### 4.1 Leitura e Escrita de Arquivos

**CSV (Comma-Separated Values):**

**Definição:** Formato texto onde valores são separados por delimitador (geralmente vírgula).

**Quando usar:**
- Dados tabulares simples
- Compatibilidade universal
- Dados pequenos a médios (<100MB)
- Interoperabilidade entre sistemas

**Vantagens:**
- Legível por humanos
- Amplamente suportado
- Simples de editar

**Desvantagens:**
- Sem tipos de dados (tudo é texto)
- Pode ser grande
- Lento para grandes volumes

```python
# Ler CSV
df = pd.read_csv('dados.csv')

# Com opções
df = pd.read_csv(
    'dados.csv',
    sep=';',              # Delimitador diferente
    encoding='utf-8',     # Encoding
    thousands=',',        # Separador de milhares
    decimal='.',          # Separador decimal
    parse_dates=['data'], # Parsear como data
    index_col='id',       # Usar coluna como índice
    usecols=['A', 'B'],   # Ler apenas colunas específicas
    nrows=1000,           # Ler apenas N linhas
    skiprows=2,           # Pular primeiras N linhas
    na_values=['NA', '?'] # Valores a considerar como nulos
)

# Escrever CSV
df.to_csv('saida.csv', index=False)

# Com opções
df.to_csv(
    'saida.csv',
    index=False,
    sep=';',
    encoding='utf-8',
    columns=['A', 'B'],   # Apenas colunas específicas
    float_format='%.2f',  # Formato de floats
    na_rep='NULL'         # Representação de nulos
)
```

**Excel:**

**Quando usar:**
- Interoperar com usuários Excel
- Múltiplas planilhas
- Formatação importante

**Vantagens:**
- Amplamente usado em negócios
- Suporta múltiplas sheets
- Formatação rica

**Desvantagens:**
- Maior que CSV
- Mais lento
- Tamanho limitado

```python
# Ler Excel
df = pd.read_excel('dados.xlsx')

# Com opções
df = pd.read_excel(
    'dados.xlsx',
    sheet_name='Planilha1',  # ou 0 para primeira
    header=0,                 # Linha do cabeçalho
    usecols='A:C',            # Colunas a ler
    nrows=100
)

# Ler múltiplas planilhas
dfs = pd.read_excel('dados.xlsx', sheet_name=None)  # Dicionário
df1 = dfs['Planilha1']
df2 = dfs['Planilha2']

# Escrever Excel
df.to_excel('saida.xlsx', index=False)

# Múltiplas planilhas
with pd.ExcelWriter('saida.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Sheet1', index=False)
    df2.to_excel(writer, sheet_name='Sheet2', index=False)
```

**JSON:**

**Quando usar:**
- APIs web
- Dados hierárquicos/nested
- Dados semi-estruturados

**Vantagens:**
- Legível por humanos
- Estrutura flexível
- Padrão web

**Desvantagens:**
- Verboso
- Maior que formatos binários

```python
# Ler JSON
df = pd.read_json('dados.json')

# Com orientação específica
df = pd.read_json('dados.json', orient='records')
# orient: 'split', 'records', 'index', 'columns', 'values'

# Escrever JSON
df.to_json('saida.json', orient='records', indent=2)
```

**Parquet:**

**Definição:** Formato colunar binário eficiente.

**Quando usar:**
- Big data
- Analytics
- Armazenamento eficiente
- Performance crítica

**Vantagens:**
- Muito compacto
- Leitura rápida
- Preserva tipos
- Compressão eficiente

**Desvantagens:**
- Não legível por humanos
- Menos universal que CSV

```python
# Escrever Parquet
df.to_parquet('dados.parquet')

# Com compressão
df.to_parquet('dados.parquet', compression='gzip')
# Opções: 'snappy', 'gzip', 'brotli'

# Ler Parquet
df = pd.read_parquet('dados.parquet')

# Colunas específicas
df = pd.read_parquet('dados.parquet', columns=['A', 'B'])
```

**SQL:**

**Quando usar:**
- Dados em banco de dados
- Queries complexas
- Grandes volumes

```python
from sqlalchemy import create_engine

# Conectar
engine = create_engine('sqlite:///banco.db')

# Ler de query
df = pd.read_sql_query('SELECT * FROM tabela WHERE idade > 25', engine)

# Ler tabela inteira
df = pd.read_sql_table('tabela', engine)

# Escrever
df.to_sql('nova_tabela', engine, if_exists='replace', index=False)
# if_exists: 'fail', 'replace', 'append'
```

### 4.2 Transformações Avançadas

**Apply:**

**Definição:** Aplicar função ao longo de um eixo do DataFrame.

**Quando usar:**
- Transformações complexas
- Operações linha por linha
- Lógica customizada

**Como usar:**
```python
# Apply em Series
df['idade_dobro'] = df['idade'].apply(lambda x: x * 2)

# Função customizada
def classificar_idade(idade):
    if idade < 20:
        return 'Jovem'
    elif idade < 40:
        return 'Adulto'
    else:
        return 'Senior'

df['faixa'] = df['idade'].apply(classificar_idade)

# Apply em DataFrame (por linha)
def calcular_imc(row):
    return row['peso'] / (row['altura'] ** 2)

df['imc'] = df.apply(calcular_imc, axis=1)

# Retornar múltiplos valores
def stats(row):
    return pd.Series({
        'soma': row['A'] + row['B'],
        'produto': row['A'] * row['B']
    })

df[['soma', 'produto']] = df.apply(stats, axis=1)

# Apply por coluna
totais = df.apply(sum, axis=0)  # Soma de cada coluna
```

**Map:**

**Definição:** Mapear valores usando dicionário ou função (apenas Series).

**Quando usar:**
- Substituir valores
- Codificar categorias
- Transformações simples 1:1

```python
# Com dicionário
mapeamento = {'M': 'Masculino', 'F': 'Feminino'}
df['genero_completo'] = df['genero'].map(mapeamento)

# Com função
df['idade_string'] = df['idade'].map(str)

# Map com lambda
df['idade_cat'] = df['idade'].map(lambda x: 'Maior' if x >= 18 else 'Menor')
```

**Apply vs Map:**
- **Apply:** Mais versátil, DataFrame ou Series
- **Map:** Apenas Series, mais rápido para mapeamentos simples

**Pivot e Melt:**

**Pivot (Wide format):**

**Definição:** Transformar valores de uma coluna em novas colunas.

**Quando usar:**
- Dados em formato longo → largo
- Criar tabelas de resumo
- Facilitar visualização

```python
# Dados originais (long format)
vendas = pd.DataFrame({
    'data': ['2024-01-01', '2024-01-01', '2024-01-02', '2024-01-02'],
    'produto': ['A', 'B', 'A', 'B'],
    'vendas': [100, 150, 120, 180]
})

# Pivot para wide format
pivot = vendas.pivot(
    index='data',
    columns='produto',
    values='vendas'
)

# Resultado:
# produto       A    B
# data
# 2024-01-01  100  150
# 2024-01-02  120  180
```

**Melt (Long format):**

**Definição:** Transformar colunas em linhas.

**Quando usar:**
- Dados largos → longos
- Preparar para análise
- Formato tidy

```python
# Reverter pivot
melted = pivot.reset_index().melt(
    id_vars='data',
    var_name='produto',
    value_name='vendas'
)

# De volta ao formato original
```

**String Operations:**

**Definição:** Operações especializadas para colunas de texto.

**Quando usar:**
- Limpar dados textuais
- Extrair informações
- Padronizar formatos

```python
# Acessor .str
df['nome_upper'] = df['nome'].str.upper()
df['nome_lower'] = df['nome'].str.lower()
df['nome_title'] = df['nome'].str.title()

# Remover espaços
df['nome_limpo'] = df['nome'].str.strip()
df['sem_espacos'] = df['nome'].str.replace(' ', '')

# Buscar
df['tem_ana'] = df['nome'].str.contains('Ana')
df['comeca_a'] = df['nome'].str.startswith('A')
df['termina_o'] = df['nome'].str.endswith('o')

# Extrair
df['primeira_letra'] = df['nome'].str[0]
df['tres_primeiras'] = df['nome'].str[:3]

# Split
df[['nome', 'sobrenome']] = df['nome_completo'].str.split(' ', expand=True)

# Regex
df['email_valido'] = df['email'].str.match(r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$')

# Substituir
df['nome_corrigido'] = df['nome'].str.replace('João', 'João Pedro')

# Comprimento
df['tamanho_nome'] = df['nome'].str.len()
```

---

## 5. Visualização de Dados

### 5.1 Princípios de Visualização

**Por que visualizar:**
1. **Comunicação:** Transmitir informação complexa rapidamente
2. **Descoberta:** Identificar padrões não óbvios
3. **Análise:** Explorar relacionamentos
4. **Persuasão:** Apoiar argumentos com evidências visuais

**Princípios fundamentais:**

1. **Clareza**
   - Mensagem principal imediatamente aparente
   - Remover elementos desnecessários
   - Evitar chartjunk
   - Uma ideia por gráfico

2. **Precisão**
   - Representar dados fielmente
   - Não distorcer escalas
   - Começar eixo Y em zero (para barras)
   - Identificar outliers claramente

3. **Eficiência**
   - Escolher tipo certo de gráfico
   - Maximizar data-ink ratio
   - Usar cores com propósito
   - Ordenar categorias logicamente

4. **Estética**
   - Design agradável
   - Cores harmoniosas
   - Tipografia legível
   - Espaçamento adequado

**Data-Ink Ratio:**

**Definição:** Proporção de tinta dedicada a mostrar dados vs. decoração.

**Objetivo:** Maximizar informação, minimizar ruído.

**Como:**
- Remover gridlines desnecessárias
- Simplificar eixos
- Evitar 3D gratuito
- Focar no conteúdo, não na forma

### 5.2 Tipos de Gráficos

#### Comparação

**1. Gráfico de Barras**

**Definição:** Barras retangulares com comprimentos proporcionais aos valores.

**Quando usar:**
- Comparar categorias
- Mostrar ranking
- Valores discretos
- Poucas categorias (< 15)

**Quando NÃO usar:**
- Séries temporais (prefira linha)
- Muitas categorias (> 20)
- Valores contínuos

**Variações:**
- Vertical: Categorias no eixo X
- Horizontal: Melhor para nomes longos
- Agrupado: Comparar múltiplas séries
- Empilhado: Mostrar composição

**Boas práticas:**
- Sempre começar eixo Y em zero
- Ordenar barras logicamente (valor, alfabético)
- Usar cores consistentes
- Adicionar valores nas barras se útil

```python
import matplotlib.pyplot as plt

# Gráfico de barras vertical
categorias = ['A', 'B', 'C', 'D']
valores = [23, 45, 56, 78]

plt.figure(figsize=(10, 6))
plt.bar(categorias, valores, color='steelblue', edgecolor='black')
plt.xlabel('Categoria')
plt.ylabel('Valor')
plt.title('Comparação de Valores por Categoria')
plt.show()

# Gráfico de barras horizontal
plt.figure(figsize=(10, 6))
plt.barh(categorias, valores, color='coral')
plt.xlabel('Valor')
plt.ylabel('Categoria')
plt.title('Ranking de Categorias')
plt.show()

# Barras agrupadas
x = np.arange(len(categorias))
valores1 = [23, 45, 56, 78]
valores2 = [30, 40, 60, 70]
width = 0.35

plt.figure(figsize=(10, 6))
plt.bar(x - width/2, valores1, width, label='Série 1')
plt.bar(x + width/2, valores2, width, label='Série 2')
plt.xlabel('Categoria')
plt.ylabel('Valor')
plt.title('Comparação de Duas Séries')
plt.xticks(x, categorias)
plt.legend()
plt.show()
```

**2. Gráfico de Linha**

**Definição:** Pontos conectados por linhas mostrando tendências.

**Quando usar:**
- Séries temporais
- Mostrar tendências
- Mudanças contínuas
- Múltiplas séries relacionadas

**Quando NÃO usar:**
- Dados categóricos não ordenados
- Valores muito esparsos
- Quando precisão exata é crítica

**Boas práticas:**
- Tempo sempre no eixo X
- Máximo 5-7 linhas
- Cores distintas
- Legendas claras
- Marcar pontos importantes

```python
# Série temporal simples
datas = pd.date_range('2024-01-01', periods=100)
valores = np.cumsum(np.random.randn(100)) + 100

plt.figure(figsize=(12, 6))
plt.plot(datas, valores, linewidth=2, color='darkblue')
plt.xlabel('Data')
plt.ylabel('Valor')
plt.title('Evolução Temporal')
plt.grid(True, alpha=0.3)
plt.show()

# Múltiplas séries
plt.figure(figsize=(12, 6))
plt.plot(datas, valores, label='Série 1', linewidth=2)
plt.plot(datas, valores * 1.2, label='Série 2', linewidth=2)
plt.plot(datas, valores * 0.8, label='Série 3', linewidth=2)
plt.xlabel('Data')
plt.ylabel('Valor')
plt.title('Comparação de Séries Temporais')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

#### Distribuição

**1. Histograma**

**Definição:** Gráfico que mostra frequência de valores em intervalos (bins).

**Quando usar:**
- Entender distribuição de variável contínua
- Identificar forma da distribuição
- Detectar outliers
- Comparar com distribuições teóricas

**Conceitos:**
- **Bins:** Intervalos que agrupam valores
- **Frequência:** Contagem em cada bin
- **Densidade:** Frequência normalizada

**Como escolher número de bins:**
- Regra de Sturges: k = 1 + log₂(n)
- Regra de Rice: k = 2n^(1/3)
- Teste visual: 10-30 bins geralmente funciona
- Muito poucos: perde detalhe
- Muito muitos: muito ruído

```python
# Histograma básico
dados = np.random.normal(100, 15, 1000)

plt.figure(figsize=(10, 6))
plt.hist(dados, bins=30, alpha=0.7, color='skyblue', edgecolor='black')
plt.axvline(np.mean(dados), color='red', linestyle='--',
            linewidth=2, label=f'Média: {np.mean(dados):.2f}')
plt.axvline(np.median(dados), color='green', linestyle='--',
            linewidth=2, label=f'Mediana: {np.median(dados):.2f}')
plt.xlabel('Valor')
plt.ylabel('Frequência')
plt.title('Distribuição de Valores')
plt.legend()
plt.show()

# Densidade
plt.figure(figsize=(10, 6))
plt.hist(dados, bins=30, density=True, alpha=0.7, color='lightgreen')
plt.xlabel('Valor')
plt.ylabel('Densidade')
plt.title('Distribuição (Densidade)')
plt.show()
```

**2. Box Plot**

**Definição:** Visualização que mostra quartis, mediana e outliers.

**Componentes:**
- **Caixa:** Q1 a Q3 (IQR)
- **Linha central:** Mediana
- **Whiskers:** 1.5 * IQR
- **Pontos:** Outliers

**Quando usar:**
- Comparar distribuições
- Identificar outliers
- Ver assimetria
- Resumo compacto de distribuição

**Interpretação:**
- Caixa grande: Alta dispersão
- Mediana não centralizada: Assimétrica
- Whiskers longos: Cauda longa
- Muitos pontos: Muitos outliers

```python
# Box plot único
plt.figure(figsize=(10, 6))
plt.boxplot(dados, vert=True)
plt.ylabel('Valor')
plt.title('Box Plot da Distribuição')
plt.show()

# Box plots comparativos
dados_grupos = [
    np.random.normal(100, 10, 100),
    np.random.normal(110, 15, 100),
    np.random.normal(90, 12, 100)
]

plt.figure(figsize=(10, 6))
plt.boxplot(dados_grupos, labels=['Grupo A', 'Grupo B', 'Grupo C'])
plt.ylabel('Valor')
plt.title('Comparação de Distribuições entre Grupos')
plt.show()
```

**3. Violin Plot**

**Definição:** Combina box plot com kernel density estimation.

**Quando usar:**
- Mostrar distribuição completa
- Identificar multimodalidade
- Comparar grupos
- Quando box plot perde informação

**Vantagens sobre box plot:**
- Mostra forma completa da distribuição
- Revela múltiplos picos
- Mais informação visual

**Desvantagens:**
- Mais complexo de interpretar
- Requer mais dados
- Pode confundir audiência não técnica

```python
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.violinplot(data=[dados_grupos[0], dados_grupos[1], dados_grupos[2]])
plt.xlabel('Grupo')
plt.ylabel('Valor')
plt.title('Violin Plot - Comparação de Distribuições')
plt.show()
```

#### Relação

**1. Scatter Plot**

**Definição:** Pontos representando pares de valores de duas variáveis.

**Quando usar:**
- Explorar relação entre variáveis
- Identificar correlação
- Detectar clusters
- Identificar outliers bivariados

**Interpretação:**
- **Positiva:** Pontos sobem da esquerda para direita
- **Negativa:** Pontos descem da esquerda para direita
- **Sem relação:** Pontos espalhados aleatoriamente
- **Não-linear:** Padrão curvo

**Elementos adicionais:**
- **Tamanho:** Terceira variável
- **Cor:** Quarta variável (categórica)
- **Linha de tendência:** Mostrar relação
- **Transparência:** Lidar com sobreposição

```python
# Scatter básico
x = np.random.randn(100)
y = 2*x + np.random.randn(100)*0.5

plt.figure(figsize=(10, 6))
plt.scatter(x, y, alpha=0.6)
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot - Relação entre X e Y')
plt.grid(True, alpha=0.3)
plt.show()

# Com cor e tamanho
tamanhos = np.random.randint(20, 200, 100)
cores = np.random.randn(100)

plt.figure(figsize=(10, 6))
scatter = plt.scatter(x, y, s=tamanhos, c=cores, cmap='viridis', alpha=0.6)
plt.colorbar(scatter, label='Terceira variável')
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot com 4 Variáveis')
plt.show()

# Com linha de regressão
from scipy import stats
slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)

plt.figure(figsize=(10, 6))
plt.scatter(x, y, alpha=0.6, label='Dados')
plt.plot(x, slope*x + intercept, 'r', linewidth=2,
         label=f'Regressão (R²={r_value**2:.3f})')
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot com Linha de Regressão')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

**2. Heatmap**

**Definição:** Matriz de valores representados por cores.

**Quando usar:**
- Visualizar matriz de correlação
- Mostrar padrões em tabela
- Comparar múltiplas dimensões
- Identificar clusters

**Escolha de cores:**
- **Sequencial:** Uma cor, dados ordenados
- **Divergente:** Duas cores, ponto central importante
- **Qualitativa:** Categorias

**Boas práticas:**
- Incluir valores nas células se legíveis
- Escala de cores apropriada
- Ordenar linhas/colunas logicamente

```python
# Heatmap de correlação
df = pd.DataFrame(np.random.randn(100, 5), columns=list('ABCDE'))
correlacao = df.corr()

plt.figure(figsize=(10, 8))
sns.heatmap(correlacao, annot=True, cmap='coolwarm', center=0,
            square=True, linewidths=1, cbar_kws={"shrink": 0.8})
plt.title('Matriz de Correlação')
plt.show()

# Heatmap de dados
dados_matriz = np.random.rand(10, 12)

plt.figure(figsize=(12, 8))
sns.heatmap(dados_matriz, annot=True, fmt='.2f', cmap='YlOrRd')
plt.title('Heatmap de Valores')
plt.show()
```

#### Composição

**1. Gráfico de Pizza**

**Definição:** Círculo dividido em fatias proporcionais.

**Quando usar (com MUITO cuidado):**
- Mostrar partes de um todo
- Poucas categorias (2-5)
- Uma categoria claramente dominante
- Audiência geral

**Quando NÃO usar:**
- Mais de 5 categorias
- Valores similares
- Comparações precisas necessárias
- Múltiplas séries

**Alternativas melhores:**
- Gráfico de barras
- Treemap
- Waffle chart

**Se usar pizza:**
- Ordenar fatias (maior para menor)
- Começar às 12h
- Limitar a 5 fatias
- Considerar donut chart

```python
# Pizza básica (use com moderação!)
categorias = ['A', 'B', 'C', 'D']
valores = [35, 25, 20, 20]

plt.figure(figsize=(8, 8))
plt.pie(valores, labels=categorias, autopct='%1.1f%%', startangle=90)
plt.title('Distribuição por Categoria')
plt.axis('equal')
plt.show()

# Melhor alternativa: barras horizontais
plt.figure(figsize=(10, 6))
plt.barh(categorias, valores)
plt.xlabel('Valor')
plt.ylabel('Categoria')
plt.title('Distribuição por Categoria (Alternativa Melhor)')
plt.show()
```

### 5.3 Cores em Visualizações

**Teoria das cores:**

**Tipos de escalas:**

1. **Sequencial**
   - **Quando:** Dados ordenados, mesma variável
   - **Exemplos:** Temperatura, idade, renda
   - **Paletas:** Blues, Greens, Reds

2. **Divergente**
   - **Quando:** Ponto central importante, desvios
   - **Exemplos:** Correlação, diferença, mudança
   - **Paletas:** RdBu, RdYlGn, PiYG

3. **Qualitativa**
   - **Quando:** Categorias distintas
   - **Exemplos:** Tipos, grupos, regiões
   - **Paletas:** Set1, Set2, Paired

**Acessibilidade:**
- Evitar apenas vermelho-verde (daltonismo)
- Testar em escala de cinza
- Usar padrões além de cores
- Incluir legendas claras

```python
# Sequencial
plt.figure(figsize=(15, 4))
for i, cmap in enumerate(['Blues', 'Greens', 'Oranges'], 1):
    plt.subplot(1, 3, i)
    data = np.random.rand(10, 10)
    plt.imshow(data, cmap=cmap)
    plt.colorbar()
    plt.title(f'Sequencial: {cmap}')
plt.tight_layout()
plt.show()

# Divergente
plt.figure(figsize=(15, 4))
for i, cmap in enumerate(['RdBu', 'RdYlGn', 'PiYG'], 1):
    plt.subplot(1, 3, i)
    data = np.random.randn(10, 10)
    plt.imshow(data, cmap=cmap, vmin=-3, vmax=3)
    plt.colorbar()
    plt.title(f'Divergente: {cmap}')
plt.tight_layout()
plt.show()
```

---
