# Coletânea de Cheat Sheets e Automação em Python

Este documento reúne resumos práticos das principais bibliotecas de Data Science e manipulação do sistema operacional em Python, além de exercícios resolvidos com a biblioteca `os`.

---

## 1. NumPy Cheat Sheet

Biblioteca fundamental para computação científica e manipulação de arrays multidimensionais eficientes.

### 1.1 Criando Arrays

```python
import numpy as np

# A partir de listas
a = np.array([1, 2, 3])  # 1D array
b = np.array([[1, 2], [3, 4]])  # 2D array (matriz)

# Preenchimento automático
zeros = np.zeros((3, 3))  # Matriz 3x3 de 0s
ones = np.ones((2, 4))  # Matriz 2x4 de 1s
full = np.full((2, 2), 7)  # Matriz 2x2 com o valor 7
eye = np.eye(3)  # Matriz identidade 3x3

# Sequências numéricas
seq = np.arange(0, 10, 2)  # [0, 2, 4, 6, 8] (início, fim exclusivo, passo)
lin = np.linspace(0, 1, 5)  # 5 valores igualmente espaçados de 0 a 1

# Números aleatórios
rand = np.random.rand(2, 3)  # Float aleatório entre 0 e 1 (2x3)
randint = np.random.randint(0, 10, size=(2, 2))  # Inteiros de 0 a 9
```

### 1.2 Inspeção e Propriedades

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

arr.shape  # (2, 3) -> Linhas, Colunas
arr.ndim  # 2 -> Número de dimensões
arr.size  # 6 -> Total de elementos
arr.dtype  # int64 -> Tipo de dado dos elementos
```

### 1.3 Indexação e Fatiamento (Slicing)

```python
# Array 1D
a = np.array([10, 20, 30, 40])
a[1]  # 20
a[1:3]  # [20, 30]

# Array 2D: arr[linha, coluna]
m = np.array([[1, 2, 3], [4, 5, 6]])
m[0, 1]  # 2 (Linha 0, Coluna 1)
m[:, 1]  # [2, 5] (Todas as linhas, apenas Coluna 1)
m[0, :]  # [1, 2, 3] (Apenas Linha 0, todas as colunas)

# Filtro Booleano (Máscaras)
m[m > 3]  # [4, 5, 6] (Retorna elementos que satisfazem a condição)
```

### 1.4 Manipulação de Forma (Reshaping)

```python
a = np.array([1, 2, 3, 4, 5, 6])

# Reorganizar elementos
b = a.reshape(2, 3)  # Transforma em matriz 2x3

# Achatar para 1D
c = b.flatten()  # Retorna cópia 1D

# Transposição
m = np.array([[1, 2], [3, 4]])
m.T  # Troca linhas por colunas

# Junção (Concatenar)
a1 = np.array([1, 2])
a2 = np.array([3, 4])
np.hstack((a1, a2))  # Empilha na horizontal: [1, 2, 3, 4]
np.vstack((a1, a2))  # Empilha na vertical: [[1, 2], [3, 4]]
```

### 1.5 Operações Matemáticas (Vetorizadas)

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Operações elemento por elemento
a + b  # [5, 7, 9]
a * b  # [4, 10, 18]
a**2  # [1, 4, 9]

# Álgebra Linear
np.dot(a, b)  # Produto escalar (32)
m1 @ m2  # Multiplicação de matrizes

# Funções Matemáticas
np.sin(a)
np.exp(a)
np.sqrt(a)
```

### 1.6 Estatística e Agregações

```python
m = np.array([[1, 2], [3, 4]])

m.sum()  # Soma total
m.mean()  # Média
m.std()  # Desvio padrão
m.min()  # Menor valor
m.max()  # Maior valor

# Por eixo (axis)
m.sum(axis=0)  # Soma ao longo das COLUNAS
m.sum(axis=1)  # Soma ao longo das LINHAS

# Índices de extremos
m.argmin()  # Índice do menor elemento
m.argmax()  # Índice do maior elemento
```

---

## 2. Pandas Cheat Sheet

Estruturas de dados de alto desempenho para análise, manipulação e limpeza tabular.

### 2.1 Estruturas Básicas e Criação

```python
import pandas as pd

# Series e DataFrame
s = pd.Series([10, 20, 30], index=["a", "b", "c"])

dados = {
    "Nome": ["Ana", "Bruno", "Carla", "Diego"],
    "Idade": [25, 30, 22, 35],
    "Cidade": ["SP", "RJ", "SP", "BH"],
    "Salario": [4000, 5500, 3200, 7000],
}
df = pd.DataFrame(dados)

# Leitura e Escrita
df = pd.read_csv("dados.csv")
df = pd.read_excel("dados.xlsx")
df.to_csv("resultado.csv", index=False)
```

### 2.2 Inspeção Inicial

```python
df.head(5)  # Primeiras 5 linhas
df.tail(3)  # Últimas 3 linhas
df.info()  # Tipos de dados, memória e valores não nulos
df.describe()  # Estatísticas descritivas
df.shape  # (linhas, colunas)
df.columns  # Lista de colunas
df.dtypes  # Tipos de cada coluna
```

### 2.3 Seleção e Fatiamento

```python
# Colunas
df["Nome"]  # Retorna Series
df[["Nome", "Salario"]]  # Retorna DataFrame

# Posição (iloc)
df.iloc[0]  # Linha 0
df.iloc[0:3, 0:2]  # Linhas 0-2, Colunas 0-1

# Rótulo e Condições (loc)
df.loc[0, "Nome"]
df.loc[df["Idade"] > 25]
df.loc[(df["Cidade"] == "SP") & (df["Salario"] > 3500)]
```

### 2.4 Limpeza e Tratamento

```python
# Valores Nulos
df.isnull().sum()
df_limpo = df.dropna()
df["Idade"] = df["Idade"].fillna(df["Idade"].mean())

# Remoção e Renomeação
df = df.drop(columns=["Cidade"])
df = df.rename(columns={"Salario": "Renda"})
df.drop_duplicates(inplace=True)

# Tipagem
df["Idade"] = df["Idade"].astype(int)
df["Data"] = pd.to_datetime(df["Data"])
```

### 2.5 Agrupamento e Ordenação

```python
df.sort_values(by="Salario", ascending=False)
df.groupby("Cidade")["Salario"].mean()
df.groupby("Cidade").agg({"Salario": "mean", "Idade": "max"})
df["Cidade"].value_counts()
```

### 2.6 Junção e Combinação

```python
# Concatenação
pd.concat([df1, df2], axis=0)

# Merge (JOIN relacional)
df_merged = pd.merge(df1, df2, on="ID_Cliente", how="inner")
```

---

## 3. Matplotlib Cheat Sheet

Criação e personalização de gráficos usando a interface orientada a objetos (`plt.subplots`).

### 3.1 Estrutura Básica

```python
import matplotlib.pyplot as plt
import numpy as np

fig, ax = plt.subplots(figsize=(8, 4))

x = np.linspace(0, 10, 100)
y = np.sin(x)

ax.plot(x, y, label="Seno", color="blue", linestyle="--", linewidth=2)
plt.show()
fig.savefig("grafico.png", dpi=300, bbox_inches="tight")
```

### 3.2 Tipos Comuns de Gráficos

```python
fig, ax = plt.subplots()

# Linha
ax.plot(x, y, color="tab:blue", marker="o", markersize=4)

# Dispersão (Scatter)
ax.scatter(x, y, c="red", alpha=0.5, s=20)

# Barras
categorias = ["A", "B", "C"]
valores = [10, 24, 15]
ax.bar(categorias, valores, color="skyblue")  # ax.barh() para horizontal

# Histograma
dados = np.random.randn(1000)
ax.hist(dados, bins=30, color="green", edgecolor="black")

# Boxplot
ax.boxplot(dados, vert=True)
```

### 3.3 Customização e Anotações

```python
fig, ax = plt.subplots()
ax.plot(x, y, label="Dados")

ax.set_title("Título do Gráfico", fontsize=14, fontweight="bold")
ax.set_xlabel("Eixo X", fontsize=10)
ax.set_ylabel("Eixo Y", fontsize=10)

ax.set_xlim(0, 10)
ax.set_ylim(-1.5, 1.5)
ax.grid(True, linestyle=":", alpha=0.6)
ax.legend(loc="upper right")

ax.annotate(
    "Pico",
    xy=(np.pi / 2, 1),
    xytext=(np.pi / 2 + 1, 1.2),
    arrowprops=dict(facecolor="black", shrink=0.05),
)
```

### 3.4 Subplots e Estilos

```python
# Múltiplos painéis
fig, axes = plt.subplots(2, 2, figsize=(10, 8))
axes[0, 0].plot(x, y, color="red")
axes[0, 1].scatter(x, y, color="blue")
axes[1, 0].bar(["A", "B"], [5, 10])
axes[1, 1].hist(np.random.randn(100))
plt.tight_layout()

# Estilos visuais prontos
plt.style.use("seaborn-v0_8-darkgrid")
```

---

## 4. Biblioteca `os` Cheat Sheet

Módulo padrão do Python 3 para interação direta com o sistema operacional e sistema de arquivos.

### 4.1 Informações do Sistema

```python
import os

os.name  # 'posix' ou 'nt'
os.getcwd()  # Diretório atual
os.getlogin()  # Usuário logado
os.environ.get("HOME")  # Variável de ambiente
```

### 4.2 Navegação e Exploração

```python
os.chdir("/caminho/do/diretorio")  # Muda de diretório
os.listdir(".")  # Lista conteúdos

# Varredura recursiva da árvore de pastas
for root, dirs, files in os.walk("."):
    print(f"Diretório: {root} | Subpastas: {dirs} | Arquivos: {files}")
```

### 4.3 Arquivos e Diretórios

```python
os.mkdir("pasta")  # Cria uma pasta
os.makedirs("pasta/subpasta/final")  # Cria estrutura aninhada
os.rename("antigo.txt", "novo.txt")  # Renomeia ou move
os.remove("arquivo.txt")  # Remove arquivo
os.rmdir("pasta_vazia")  # Remove pasta (apenas se vazia)
os.removedirs("pasta/subpasta")  # Remove pastas aninhadas vazias
```

### 4.4 `os.path`

```python
caminho = os.path.join("pasta", "subpasta", "arquivo.txt")

os.path.basename(caminho)  # 'arquivo.txt'
os.path.dirname(caminho)  # 'pasta/subpasta'
os.path.split(caminho)  # ('pasta/subpasta', 'arquivo.txt')
os.path.splitext(caminho)  # ('pasta/subpasta/arquivo', '.txt')

os.path.exists(caminho)  # True se existir
os.path.isfile(caminho)  # True se for arquivo
os.path.isdir(caminho)  # True se for pasta
os.path.getsize("arquivo.txt")  # Tamanho em bytes
```

### 4.5 Processos e Comandos

```python
os.system("echo Hello World")  # Executa comando de terminal
os.getpid()  # ID do processo atual
os.getppid()  # ID do processo pai
```

---

## 5. Exercícios de Automação com a Biblioteca `os`

### Exercícios Propostos

1. **Organizador de Downloads por Extensão**: Varrer uma pasta e mover arquivos para subpastas conforme sua extensão (`.pdf` -> `PDF/`, `.jpg` -> `JPG/`).
2. **Calculadora de Tamanho de Diretório**: Função `tamanho_total_pasta(caminho)` que soma o tamanho de todos os arquivos de um diretório e subdiretórios em MB.
3. **Busca de Arquivos de Log Recentes**: Encontrar arquivos `.log` recursivamente cujo nome contenha a palavra `"ERROR"`.
4. **Limpeza de Pastas Vazias**: Identificar e remover diretórios vazios em uma árvore de pastas.
5. **Gerador de Estrutura de Projeto**: Criar um script que monte a estrutura de pastas inicial de um projeto (`src/css`, `src/js`, `docs`, `tests`).

---

### Gabarito dos Exercícios

#### Gabarito 1: Organizador de Arquivos por Extensão
```python
import os


def organizar_pasta(diretorio):
    if not os.path.exists(diretorio):
        print("Diretório não encontrado.")
        return

    for item in os.listdir(diretorio):
        caminho_item = os.path.join(diretorio, item)

        if os.path.isfile(caminho_item):
            _, extensao = os.path.splitext(item)

            if extensao:
                extensao_limpa = extensao[1:].upper()
                pasta_destino = os.path.join(diretorio, extensao_limpa)

                if not os.path.exists(pasta_destino):
                    os.mkdir(pasta_destino)

                novo_caminho = os.path.join(pasta_destino, item)
                os.rename(caminho_item, novo_caminho)
```

#### Gabarito 2: Calculadora de Tamanho em MB
```python
import os


def tamanho_total_pasta(caminho):
    tamanho_bytes = 0

    for raiz, _, arquivos in os.walk(caminho):
        for arquivo in arquivos:
            caminho_completo = os.path.join(raiz, arquivo)
            if os.path.exists(caminho_completo):
                tamanho_bytes += os.path.getsize(caminho_completo)

    tamanho_mb = tamanho_bytes / (1024 * 1024)
    return round(tamanho_mb, 2)
```

#### Gabarito 3: Busca de Logs com "ERROR"
```python
import os


def buscar_logs_erro(diretorio_raiz):
    print("Arquivos de LOG com erro encontrados:")

    for raiz, _, arquivos in os.walk(diretorio_raiz):
        for arquivo in arquivos:
            nome, ext = os.path.splitext(arquivo)

            if ext.lower() == ".log" and "ERROR" in nome.upper():
                caminho_completo = os.path.join(raiz, arquivo)
                print(f"- {caminho_completo}")
```

#### Gabarito 4: Remoção de Pastas Vazias
```python
import os


def limpar_pastas_vazias(diretorio_raiz):
    # topdown=False garante varredura do nível mais profundo para o topo
    for raiz, pastas, arquivos in os.walk(diretorio_raiz, topdown=False):
        try:
            if not os.listdir(raiz):
                os.rmdir(raiz)
                print(f"Pasta removida: {raiz}")
        except PermissionError:
            pass
```

#### Gabarito 5: Criação de Estrutura de Projeto
```python
import os


def criar_estrutura_projeto(nome_projeto):
    subpastas = [
        os.path.join(nome_projeto, "src", "css"),
        os.path.join(nome_projeto, "src", "js"),
        os.path.join(nome_projeto, "docs"),
        os.path.join(nome_projeto, "tests"),
    ]

    for pasta in subpastas:
        os.makedirs(pasta, exist_ok=True)

    print(f"Estrutura do projeto '{nome_projeto}' criada com sucesso!")
```