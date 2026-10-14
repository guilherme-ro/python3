# Cheatsheet Completo: Python 3 & Manipulação de Strings

Este documento reúne uma visão geral da sintaxe fundamental de Python 3, acompanhado de um guia aprofundado dedicado exclusivamente à manipulação de strings.

---

# Parte 1: Visão Geral de Python 3

## 1. Tipos de Dados e Variáveis

```python
# Tipos Básicos
inteiro = 42
flutuante = 3.14
texto = "Olá, Mundo!"
booleano = True  # ou False
nulo = None

# Conversão de Tipos (Casting)
x = int("10")       # 10
y = float(5)        # 5.0
z = str(100)        # "100"

# Formatação de Strings (f-strings)
nome = "Ana"
idade = 25
print(f"Nome: {nome}, Idade: {idade}")
```

---

## 2. Operadores

| Categoria | Operadores | Exemplo / Descrição |
| :--- | :--- | :--- |
| **Aritméticos** | `+`, `-`, `*`, `/` | Adição, Subtração, Multiplicação, Divisão (`7 / 2 = 3.5`) |
| | `//`, `%`, `**` | Divisão Inteira (`7 // 2 = 3`), Módulo/Resto (`7 % 2 = 1`), Potência (`2 ** 3 = 8`) |
| **Comparação** | `==`, `!=`, `>`, `<`, `>=`, `<=` | Igual, Diferente, Maior, Menor, Maior/Igual, Menor/Igual |
| **Lógicos** | `and`, `or`, `not` | E (ambos True), OU (pelo menos um True), NÃO (inverte o valor) |
| **Identidade / Pertencimento** | `is`, `is not`, `in`, `not in` | Mesma referência em memória (`is`), Presente em coleção (`in`) |

---

## 3. Estruturas de Controle

### Condicionais (`if`, `elif`, `else`)

```python
nota = 85

if nota >= 90:
    print("Excelente")
elif nota >= 70:
    print("Aprovado")
else:
    print("Reprovado")

# Operador Ternário (if inline)
status = "Aprovado" if nota >= 70 else "Reprovado"
```

### Laços de Repetição (`for`, `while`)

```python
# For em intervalo (0 a 4)
for i in range(5):
    print(i)

# While
contador = 0
while contador < 3:
    print(contador)
    contador += 1
```

---

## 4. Coleções de Dados

```python
# Listas (Mutáveis, ordenadas)
frutas = ["maçã", "banana", "laranja"]
frutas.append("uva")       # Adiciona ao final
frutas.insert(1, "kiwi")   # Insere na posição especificada
frutas.remove("banana")    # Remove pelo valor
primeira = frutas[0]       # Acesso por índice

# Tuplas (Imutáveis, ordenadas)
ponto = (10, 20)
x, y = ponto               # Desempacotamento

# Dicionários (Chave-Valor)
aluno = {"nome": "Carlos", "idade": 22}
print(aluno["nome"])          # Acesso direto
aluno["curso"] = "TI"         # Adiciona ou atualiza chave
idade = aluno.get("idade", 0) # Acesso seguro com valor padrão de fallback

# Conjuntos / Sets (Valores únicos, não ordenados)
numeros = {1, 2, 2, 3}     # Resulta em {1, 2, 3}
numeros.add(4)
```

### Slicing em Coleções

```python
# Sintaxe: colecao[início:fim:passo]
nums = [0, 1, 2, 3, 4, 5]
sub = nums[1:4]      # [1, 2, 3]
inverso = nums[::-1] # [5, 4, 3, 2, 1, 0]
```

---

## 5. List Comprehension

```python
# Criar lista de quadrados para números pares de 0 a 9
pares_quadrados = [x**2 for x in range(10) if x % 2 == 0]
# Resultado: [0, 4, 16, 36, 64]
```

---

## 6. Funções e Tratamento de Exceções

```python
# Declaração com valor default
def saudar(nome, msg="Olá"):
    return f"{msg}, {nome}!"

# Argumentos Arbitrários (*args e **kwargs)
def somar_tudo(*args, **kwargs):
    # args: tupla de argumentos posicionais
    # kwargs: dicionário de argumentos nomeados
    return sum(args)

# Tratamento de Exceções
try:
    resultado = 10 / 0
except ZeroDivisionError as e:
    print(f"Erro: {e}")
finally:
    print("Executado sempre.")
```

---

## 7. Arquivos e Módulos

```python
# Leitura e escrita segura usando Context Manager (with)
with open("arquivo.txt", "w", encoding="utf-8") as f:
    f.write("Escrevendo linha...\n")

with open("arquivo.txt", "r", encoding="utf-8") as f:
    conteudo = f.read()

# Módulos Úteis da Biblioteca Padrão
import os, sys, math, json
from datetime import datetime

hoje = datetime.now()
dados_json = json.dumps({"status": 200})
raiz = math.sqrt(16)
```

---
---

# Parte 2: Guia Detalhado de Strings em Python 3

## 1. Criação, Escape e F-Strings Básicas

```python
# Declaração
s1 = 'Aspas simples'
s2 = "Aspas duplas"
s3 = """Texto multilinha
com aspas triplas"""

# Caracteres de Escape
escapado = "Linha 1\nLinha 2\t(tabulação) e aspas: \"exemplo\""

# Raw Strings (ignora sequências de escape, útil para regex e caminhos)
caminho = r"C:\novos_arquivos\testes"

# Interpolação via F-Strings
nome = "Ana"
idade = 28
preco = 49.9

print(f"Usuária: {nome}, Idade: {idade}")
print(f"Preço formatado: R$ {preco:.2f}")       # R$ 49.90 (2 casas decimais)
print(f"Expressão: {nome.upper()}")            # Suporta métodos e expressões Python
```

---

## 2. Indexação, Slicing e Imutabilidade

> **Regra fundamental:** Strings em Python são **imutáveis**. Qualquer operação que transforme um texto retorna um novo objeto em memória.

```python
# Tabela de Índices:
#   Texto:   P   y   t   h   o   n
# Positivo:  0   1   2   3   4   5
# Negativo: -6  -5  -4  -3  -2  -1

texto = "Python"

# Acesso direto
primeira = texto[0]   # 'P'
ultima = texto[-1]    # 'n'

# Sintaxe do Slicing: string[início:fim:passo] (o índice 'fim' é exclusivo)
sub1 = texto[0:4]     # 'Pyth'
sub2 = texto[2:]      # 'thon' (do índice 2 até o fim)
sub3 = texto[:3]      # 'Pyt'  (do início até o índice 2)
passo = texto[::2]    # 'Pto'  (de 2 em 2 caracteres)
inverso = texto[::-1] # 'nohtyP' (inverte a string completa)
```

---

## 3. Modificação, Limpeza e Caixa

| Método | Descrição | Exemplo $\rightarrow$ Retorno |
| :--- | :--- | :--- |
| `.upper()` | Caixa alta | `"python".upper()` $\rightarrow$ `'PYTHON'` |
| `.lower()` | Caixa baixa | `"PYTHON".lower()` $\rightarrow$ `'python'` |
| `.capitalize()` | Primeira letra maiúscula | `"olá mundo".capitalize()` $\rightarrow$ `'Olá mundo'` |
| `.title()` | Cada palavra em maiúscula | `"olá mundo".title()` $\rightarrow$ `'Olá Mundo'` |
| `.strip()` | Remove espaços das extremidades | `"  oi  ".strip()` $\rightarrow$ `'oi'` |
| `.lstrip()` / `.rstrip()` | Remove espaços à esquerda / direita | `"  oi  ".lstrip()` $\rightarrow$ `'oi  '` |
| `.replace(old, new)` | Substitui substrings | `"banana".replace("a", "o")` $\rightarrow$ `'bonono'` |

---

## 4. Divisão, Junção e Alinhamento

```python
# .split(separador): divide uma string e gera uma lista
csv = "maçã,banana,laranja"
frutas = csv.split(",")        # ['maçã', 'banana', 'laranja']

texto_livre = "Python é incrível"
palavras = texto_livre.split() # Sem argumentos, divide por espaços em branco

# .join(iterável): une itens de uma lista com o delimitador
lista = ["2026", "10", "13"]
data = "-".join(lista)         # "2026-10-13"

# Preenchimento e Alinhamento
codigo = "42"
print(codigo.zfill(5))         # "00042" (completa com zeros à esquerda)
print("Oi".center(10, "-"))    # "----Oi----"
print("Oi".ljust(10, "."))     # "Oi........"
```

---

## 5. Verificação, Busca e Testes de Conteúdo

```python
frase = "Aprender Python é fácil"

# Operador 'in' (Case-sensitive)
existe = "Python" in frase     # True

# Busca e Contagem
posicao = frase.find("Python") # 9 (retorna -1 se não encontrar)
total = frase.count("a")       # 2 (conta ocorrências)

# Testes de Início / Fim
print(frase.startswith("Aprender")) # True
print(frase.endswith("fácil"))      # True

# Validação de Caracteres
print("12345".isdigit())       # True (apenas dígitos)
print("abcDE".isalpha())       # True (apenas letras)
print("abc12".isalnum())       # True (apenas letras e números)
print("   ".isspace())         # True (apenas caracteres em branco)
print("hello".islower())       # True (apenas letras minúsculas)
```

---

## 6. Recursos Avançados de F-Strings

```python
import datetime

# 1. Debugging rápido com '=' (imprime a expressão e o valor resultante)
x = 10
y = 25
print(f"{x=}, {y=}, {x+y=}")   # "x=10, y=25, x+y=35"

# 2. Alinhamento e Preenchimento inline
print(f"{'Centro':^20}")       # "       Centro       "
print(f"{'Esquerda':<15}")     # "Esquerda       "
print(f"{'Direita':>15}")      # "        Direita"

# 3. Formatação Numérica e Porcentagem
valor = 1234567.891
porcentagem = 0.756

print(f"{valor:,.2f}")         # "1,234,567.89"
print(f"{porcentagem:.1%}")    # "75.6%"

# 4. Formatação de Datas
hoje = datetime.datetime.now()
print(f"Data: {hoje:%d/%m/%Y às %H:%M}") # "Data: 13/10/2026 às 22:18"
```