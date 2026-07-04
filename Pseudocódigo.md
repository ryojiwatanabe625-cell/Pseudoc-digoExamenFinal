# Pseudocódigo — Explotar Globos (Burst Balloons)
## Curso: Análisis de Algoritmos y Estrategias de Programación
## Grupo 08

## Algoritmo 1: Fuerza Bruta Recursiva — O(n!)

```
ALGORITMO FuerzaBrutaRecursiva(globos):

  globos <- [1] + globos + [1]

  FUNCION Resolver(arr):
    SI longitud(arr) == 2 ENTONCES
      RETORNAR 0
    FIN SI

    mejor <- 0

    PARA i DESDE 1 HASTA longitud(arr) - 2 HACER
      puntos <- arr[i-1] * arr[i] * arr[i+1]
      nuevoArreglo <- arr SIN el elemento en la posicion i
      candidato <- puntos + Resolver(nuevoArreglo)

      SI candidato > mejor ENTONCES
        mejor <- candidato
      FIN SI
    FIN PARA

    RETORNAR mejor
  FIN FUNCION

  RETORNAR Resolver(globos)

FIN ALGORITMO
```

**Complejidad temporal:** O(n!)  
**Complejidad espacial:** O(n)  

---

## Algoritmo 2: Programación Dinámica sobre Intervalos — O(n³)

```
ALGORITMO ProgramacionDinamica(globos):

  globos <- [1] + globos + [1]
  n <- longitud(globos)
  dp <- matriz de n x n inicializada en 0

  PARA longitud DESDE 2 HASTA n - 1 HACER
    PARA i DESDE 0 HASTA n - longitud - 1 HACER
      j <- i + longitud

      PARA k DESDE i + 1 HASTA j - 1 HACER
        monedas <- globos[i] * globos[k] * globos[j] + dp[i][k] + dp[k][j]

        SI monedas > dp[i][j] ENTONCES
          dp[i][j] <- monedas
        FIN SI
      FIN PARA

    FIN PARA
  FIN PARA

  RETORNAR dp[0][n-1]

FIN ALGORITMO
```

**Complejidad temporal:** O(n³)  
**Complejidad espacial:** O(n²)  

---

## Comparación de complejidades

| Algoritmo             | Tiempo | Espacio | n=8 (ms) | n=300 (ms) |
|-----------------------|--------|---------|----------|------------|
| Fuerza Bruta          | O(n!)  | O(n)    | ~48.8    | inviable   |
| Programación Dinámica | O(n³)  | O(n²)   | ~0.03    | ~478       |