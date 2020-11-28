# Investigação Operacional

## **Modelo de Programação Linear**

- Variáveis de decisão (sempre quantitativas)
    - $x_{1}, x_{2}, x_{3} ...$
- Função objetivo
- Restrições

### **Exemplo:**

- Variáveis de decisão
    - $x_{1}$ → número de unidades de área a plantar de arroz
    - $x_{2}$ → número de unidades de área a plantar de milho
- Função objetivo
    - maximizar o lucro (UM aka unidades monetárias) a obter das plantações
    - $Max Z = 5x_{1} + 2x_{2}$
- Restrições
    - $x_{1} + 2x_{2} \leqslant 9$ (mão-obra)
    - $x_{1} \leqslant 3$ (unidades de área)
    - $x_{2} \leqslant 4$ (unidades de área)
    - $x_{1} \geqslant 0, x_{1} \geqslant 0$ (não negatividade)

Estes modelos podem ser escritos usando dois tipos de notação: cartesiana ou matricial.

### **Notação cartesiana:**

$Max Z = 5x_{1} + 2x_{2}$

Sujeito a:
- $x_{1} + 2x_{2} \leqslant 9$
- $x_{1} \leqslant 3$ 
- $x_{2} \leqslant 4$
- $x_{1} \geqslant 0, x_{1} \geqslant 0$

### **Notação matricial:**

$x =\begin{bmatrix}
x_{1}\\
x_{2}\\
\end{bmatrix}$
$C =\begin{bmatrix}
5\\
2\\
\end{bmatrix}$
$Z = x * C^{T} = \begin{bmatrix}
x_{1}\\
x_{2}\\
\end{bmatrix} 
\begin{bmatrix}
5 & 2\\
\end{bmatrix}$

$0 =\begin{bmatrix}
0\\
0\\
\end{bmatrix}$

$A =\begin{bmatrix}
1 & 2\\
1 & 0\\
0 & 1\\
\end{bmatrix}$
$b =\begin{bmatrix}
9\\
3\\
4\\
\end{bmatrix}$

---

## **Método Gráfico**

Este método serve para resolver funções do tipo $Max Z$ e do tipo $Min Z$ graficamente.

1. Tornar as equações em inequações e desenhar um gráfico com as retas respetivas
    - Para obter pontos para facilitar o desenho é ir igualando as variáveis $x_{1}$ e $x_{2}$ individualmente para obter pontos que se situem nos eixos principais (geralmente sao $x$ e $y$, mas neste caso serão $x_{1}$ e $x_{2}$)
2. Detetar qual o semiplano representado por cada inequação e qual é a região admissível
    - Para facilitar a perceção disto é só igualar $x_{1}$ e $x_{2}$ a 0 para perceber se a origem do referencial (ou seja, o ponto (0, 0)) faz parte do semiplano
3. Traçar uma reta auxiliar para um valor de $Z$ à escolha
    - A recomendação é que este valor de Z seja um mmc dos coeficientes das variáveis
4. Traçar uma reta auxiliar para $Z = 0$
    - Fazemos isto para conseguir perceber em que sentido é que o $Z$ aumenta ou diminui
5. Com o auxílio duma régua ou algo que possa fazer de régua, seguir paralelamente às retas auxiliares no sentido relevante para o problema até atingir o último PEA (ponto extremo admissível)

As coordenadas do PEA escolhido no final dos passos em cima serão os valores que temos que dar às variáveis $x_{1}$ e $x_{2}$ para obter o valor ótimo de $Z$.

Em caso de ambiguidade em algum dos valores, usa-se o valor que temos a certeza e substituimos nas equações das retas que se cruzam para obter o outro.

---

## **Método Simplex**

Apenas funciona para funções do tipo $Max Z$.

Como o método simples apenas funciona com equações, transformamos as inequações em equações usando slacks, artificiais e/ou surplus.

| Condição | Regra |
| --- | --- |
| $\leqslant$ | + slacks |
| $=$ | + artificial |
| $\geqslant$ | - surplus <br> + artificial |

### **Exemplo:**

$Max Z = 5x_{1} + 2x_{2}$

Sujeito a:
- $x_{1} + 2x_{2} \leqslant 9$
- $x_{1} \leqslant 3$ 
- $x_{2} \leqslant 4$
- $x_{1} \geqslant 0, x_{1} \geqslant 0$

Adicionando slacks:

- $x_{1} + 2x_{2} + x_{3} = 9$
- $x_{1} + x_{4} = 3$ 
- $x_{2} + x_{5} = 4$
- $x_{j} \geqslant 0, j = 1, ..., 5$

$
\begin{matrix}
\begin{array}{c|ccccc|c}
     & 5 & 2 & 0 & 0 & 0 & \\
     & x_1 & x_2 & x_3 & x_4 & x_5 & b \\ \hline
    x_3 \ 0 & 1 & 0 & 1 & 0 & 0 & 3 \\
    x_4 \ 0 & 0 & 1 & 0 & 1 & 0 & 4  \\
    x_5 \ 0 & 1 & 2 & 0 & 0 & 1 & 9 \\ \hline
    z_j-c_j & -5 & -2 & 0 & 0 & 0 & 0 \\
\end{array}
\end{matrix}
$

SBA: $x=(0, 0, 3, 4, 9)$

Enquanto existirem valores negativos na linha $z_{j}-c_{j}$, é possivel melhorar o valor de $Z$.

Selecionando a coluna $x_{1}$ e a linha $x_{3}$ como pivot.

- Coluna pivot: coluna da variável que vai entrar na base
- Linha pivot: linha da variável que vai sair da base

$
\begin{matrix}
\begin{array}{c|ccccc|c}
     & 5 & 2 & 0 & 0 & 0 & \\
     & x_1 & x_2 & x_3 & x_4 & x_5 & b \\ \hline
    x_1 \ 5 & 1 & 0 & 1 & 0 & 0 & 3 \\
    x_4 \ 0 & 0 & 1 & 0 & 1 & 0 & 4  \\
    x_5 \ 0 & 0 & 2 & -1 & 0 & 1 & 6 \\ \hline
    z_j-c_j & 0 & -2 & 5 & 0 & 0 & 15 \\
\end{array}
\end{matrix}
\begin{array}{ll}
    \\ 
    (1)' = (1) \\
    (2)' = (2) \\
    (3)' = (3) - (1)' 
\end{array}
$

SBA: $x=(3, 0, 0, 4, 6)$

O objetivo com as operações de linhas é fazer com que o número pivot seja 1 e os restantes 0.

O objetivo com o método simplex é ir resolvendo quadros até não existirem valores negativos na linha $z_{j} - c_{j}$ e, quando isto se verificar diz-se que se atingiu o quadro ótimo e o valor de $Z$ obtido será o valor ótimo (ou seja, máximo).

---

## **Método Simplex e Variáveis Artificiais**

Com a introdução de variáveis artificiais (como às vezes é obrigatório) torna-se impossível usar o método simplex sem fazer alguns ajustes na maneira como usamos o método. Para solucionar este problema temos o método do **Grande M** e o método das **2 fases**.

Não esquecer que um problema só esta resolvido se as variáveis artificiais tiverem valor 0.

### **Método do Grande M:**

Neste método damos uso a uma número imaginário chamado de M. Este é uma constande positiva de valor muito elevado.

Para usar este método, ao adicionarmos as variáveis necessárias ao problema para usar o método simplex, metemos as variáveis artificais na função objetivo com -M. Depois é só aplicar o método simplex usando a nova função objetivo.

### **Método das 2 fases:**

Neste método separamos o uso do método simplex em duas fases (como indica o nome).

Primeira fase:

1. Criar uma nova função objetivo composta pelas variáveis artificiais acompanhadas pelo coeficiente -1
2. Usar o método simplex até se obter um quadro ótimo (neste quadro as variáveis artificiais devem ter valor 0)

Segunda fase:

1. Pegar no quadro obtido na primeira fase e remover as colunas das variáveis artificiais
2. Usar a função objetivo original e obter um quadro ótimo

De um modo geral o método da 2 fases é considerado mais fácil e mais intuitivo.

---

## **Casos Particulares do Método Simplex**

- Empate na escolha do valor mais negativo na linha $z_{j} - c_{j}$
    - Qualquer um pode ser selecionado
- Existe $z_{j} - c_{j}$ negativos, mas apenas elementos não positivos na coluna pivot
    - Este problema de otimização tem solução não limitada
- Variável artificial aparece na solução ótima (tem valor diferente de 0)
    - Este problema de otimização não tem solução
- Empate nos quocientes, ou seja, nas escolha da variável que vai sair da base
    - Qualquer uma pode sair, mas conduz a uma solução degenerada
- Valor de $z_{j} - c_{j}$ nulo sendo $x_{j}$ uma variável não básica
    - Este problema tem mais do que uma solução ótima

---

## **Solução para variáveis com restrição diferente de $\geqslant$ para aplicação do Método Simplex**

Por vezes é necessário moldar o modelo PL de modo a ter as variáveis todas com restrições do tipo $\geqslant 0$. 

Para fazer isto, dum modo geral, transforma-se a variável em 2 variáveis: uma que representa a parte positiva e outra que representa a parte negativa (ambas com valor superior ou igual a 0).

### **Exemplo:** 

$x_1 \ livre \rightarrow x_1 = x_1^+ - x_1^-, x_1^+ \geqslant 0, x_1^- \geqslant 0$

Após isto é só substituir no problema $x_1$ por $x_1^+ - x_1^-$.

---

## **Variável Folga (definição genérica)**

- slack (folga negativa)
    - representa o défice do lado esquerdo em relação ao lado direito
- surplus (folga positiva)
    - representa o excesso do lado esquerdo em relação ao lado direito

---

## **Dualidade**

A cada modelo PL corresponde um outro chamado dual, formado pelos mesmos coeficientes mas organizado de maneira diferente.

Na relação com o problema dual, o problema inicial chama-se de problema primal.

Na solução ótima, o $Z$ do dual e o $Z$ do primal são iguais.

**Relações Primal-Dual**

| Max FO | | | Min FO |
| --- | --- | --- | --- |
| Restrições <br> <br> <br> | $\geqslant$ <br> $\leqslant$ <br> $=$ | $\leqslant 0$ <br> $\geqslant 0$ <br> $livre$ | Variáveis <br> <br> <br> |
| Variáveis <br> <br> <br> | $\geqslant 0$ <br> $\leqslant 0$ <br> $livre$ | $\geqslant$ <br> $\leqslant$ <br> $=$ | Restrições <br> <br> <br> |

| Variável Primal | Variável Dual Associada |
| --- | --- |
| Básica (valor = 0) | Não Básica (valor = 0) |
| Não Básica (valor = 0) | Básica (valor = 0) |

### **Exemplo:**

**PRIMAL**

$MaxZ = 5x_1 + 3x_2$

s.a.
- $x_1 + 2x_2 \leqslant 5 \leftarrow u_1$
- $-x_1 + x_2 \leqslant 3 \leftarrow u_2$
- $3x_1 + x_2 \leqslant 6 \leftarrow u_3$
- $x_1 \geqslant 0, x_2 \geqslant 0$

**DUAL**

$MinZd = 5u_1 + 3u_2 + 6u_3$

s.a.
- $u_1 - u_2 + 3u_3 \geqslant 5$
- $2u_1 + u_2 + u_3 \geqslant 3$
- $u_1 \geqslant 0, u_2 \geqslant 0, u_3 \geqslant 0$

### **Como tirar a solução ótima dum quadro ótimo dual:**

$
\begin{matrix}
\begin{array}{c|ccc:cccc|c}
     & -3 & -4 & -9 & 0 & -M & 0 & -M & \\
     & u_1 & u_2 & u_3 & u_4 & u_5 & u_6 & u_7 & b \\ \hline
    u_1 \ -3 & 1 & -\frac{1}{2} & 0 & -1 & 1 & \frac{1}{2} & -\frac{1}{2} & 4 \\
    u_3 \ -9 & 0 & \frac{1}{2} & 1 & 0 & 0 & -\frac{1}{2} & \frac{1}{2} & 1 \\ \hline
    z_j-c_j & 0 & 1 & 0 & 3 & M - 3 & 3 & M - 3 & 21 \\
     & \uparrow & \uparrow & \uparrow & \uparrow & & \uparrow & & \uparrow \\
     & x_3 & x_4 & x_5 & x_1 & & x_2 & & Zd \\
\end{array}
\end{matrix}
$

A divisão feita no quadro Simplex separa as variáveis originais para a esquerda e as folgas mais as artificiais para a direita. 

Começamos da linha que separa para a direita, saltando as artificiais, depois começamos da direita para a esquerda na parte esquerda da tabela, obtendo assim os valores equivalentes às variáveis originais e, deste modo, obtendo a solução básica admíssivel a partir do dual.

**[Página Inicial](../../../index.md) | [Página Anterior](./Main.md)**