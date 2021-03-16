# Introdução à Inteligência Artificial

## **Métodos de Pesquisa**

**Pesquisa não Informada:**
- Profundidade
- Largura
- Uniforme

**Pesquisa Informada:**
- Sôfrega: h
- A* = f = g + h

Deve-se definir uma heuristica que seja admissível, ou seja, menor ou igual ao custo real.
Quanto melhor o h, melhor o desempenho do algoritmo.

```plantuml
@startuml
skinparam shadowing false
skinparam backgroundColor #282a36
skinparam DefaultFontColor #f8f8f2

skinparam defaultFontName sans-serif
skinparam classFontSize 14

skinparam usecase {
    BackgroundColor #282a36
    BorderColor #f8f8f2
    ArrowColor #f8f8f2
}

together {
    (A)
    (B)
    (G)
}

(A) as A
(B) as B
(C) as C
(G) as G
(H) as H

A -- B: 1
A -- C: 3

B -- C: 1
B -- G: 9

C -- G: 5
C -- H: 2

H -- G: 1
@enduml
```
O objetivo é encontrar o caminho de A para G.

---

### **Método de Profundidade:**

```plantuml
@startuml
skinparam shadowing false
skinparam backgroundColor #282a36
skinparam DefaultFontColor #f8f8f2

skinparam defaultFontName sans-serif
skinparam classFontSize 14

skinparam usecase {
    BackgroundColor #282a36
    BorderColor #f8f8f2
    ArrowColor #f8f8f2
}

(A) as A
(B) as B
(C) as C1
(C) as C2
(G) as G1
(G) as G2
(H) as H
A -- B
A -- C1

B -- C2
B -- G1

C2 -- G2
C2 -- H
@enduml
```

Para este método o custo não conta. Aqui expandimos sempre o ramo mais à esquerda e apenas este.

---

### **Método de Largura:**

```plantuml
@startuml
skinparam shadowing false
skinparam backgroundColor #282a36
skinparam DefaultFontColor #f8f8f2

skinparam defaultFontName sans-serif
skinparam classFontSize 14

skinparam usecase {
    BackgroundColor #282a36
    BorderColor #f8f8f2
    ArrowColor #f8f8f2
}

skinparam note {
    BackgroundColor #282a36
    BorderColor #f8f8f2
}

(A) as A
(B) as B
(C) as C1
(C) as C2
(G) as G1
(G) as G2
(G) as G3
(H) as H1
(H) as H2
A -- B
A -- C1

B -- C2
B -- G1

C1 -- G2
C1 -- H1

C2 -- G3
C2 -- H2

note bottom of (G1)
  Chegada
end note
@enduml
```

Para este método o custo não conta. Aqui abrimos sempre todos os ramos possíveis, da esquerda para a direita, ate atingirmos o ojetivo.

---

### **Método da Sôfrega:**

Seja h(A) = 5, h(B) = 4, h(C) = 1, h(H) = 1, h(G) = 0.

```plantuml
@startuml
skinparam shadowing false
skinparam backgroundColor #282a36
skinparam DefaultFontColor #f8f8f2

skinparam defaultFontName sans-serif
skinparam classFontSize 14

skinparam usecase {
    BackgroundColor #282a36
    BorderColor #f8f8f2
    ArrowColor #f8f8f2
}

skinparam note {
    BackgroundColor #282a36
    BorderColor #f8f8f2
}

(A) as A
(B [4]) as B1
(B [4]) as B2
(C [1]) as C
(G [0]) as G
(H [1]) as H

A -- B1
A -- C

C -- B2
C -- G
C -- H
note bottom of (G)
  Chegada
end note
@enduml
```

Para este método o custo esperado (sôfrega) é tido em conta. Aqui expande-se o ramo que parece mais perto do objetivo.

---

### **Método do Custo Uniforme:**

```plantuml
@startuml
skinparam shadowing false
skinparam backgroundColor #282a36
skinparam DefaultFontColor #f8f8f2

skinparam defaultFontName sans-serif
skinparam classFontSize 14

skinparam usecase {
    BackgroundColor #282a36
    BorderColor #f8f8f2
    ArrowColor #f8f8f2
}

skinparam note {
    BackgroundColor #282a36
    BorderColor #f8f8f2
}

(A) as A
(B [1]) as B1
(B [4]) as B2
(C [3]) as C1
(C [2]) as C2
(G [10]) as G1
(G [7]) as G2
(G [5]) as G3
(G [8]) as G4
(G [6]) as G5
(H [4]) as H1
(H [5]) as H2

A -- B1
A -- C1

B1 -- C2
B1 -- G1

C1 -- B2
C1 -- G4
C1 -- H2

C2 -- G2
C2 -- H1

H2 -- G5

H1 -- G3

note bottom of (G5)
  Chegada
end note
@enduml
```

Para este método o custo real (uniforme) é tido em conta. Aqui expandem-se todos os ramos e escolhe-se a situação onde custa menos chega ao objetivo.

**[Página Inicial](../../../index.md) | [Página Anterior](./Main.md)**