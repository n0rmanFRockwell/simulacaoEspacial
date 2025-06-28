# 🚀 Exploração Espacial - Simulação em Java

## 🌌 Componentes da Simulação

### 🌿 Recursos

Cada recurso possui **valor** e **peso**, ambos imutáveis após a criação.

| Recurso   | Valor | Peso |
|-----------|-------|------|
| Água      | 180   | 10   |
| Oxigênio  | 300   | 2    |
| Silício   | 60    | 16   |
| Ouro      | 120   | 25   |
| Ferro     | 30    | 32   |

### 🪐 Planetas

Um planeta contém:

- Uma **posição** (int)
- Uma lista de **recursos**

É possível obter:

- **Valor total**: soma do valor de todos os recursos
- **Valor por peso**: soma das divisões individuais de valor/peso

> Exemplo: Água (180/10), Oxigênio (300/2), Ouro (120/25) → Valor total = 600, Valor por peso ≈ 18 + 150 + 4 = 172

### 🚀 Nave

A nave possui:

- Quantidade inicial de **combustível**
- Uma **posição** atual (inicialmente 0)
- Um custo de **3L de combustível por posição percorrida**

#### Funcionalidades:

- `getQuantidadeDeCombustivel()`: retorna o combustível restante
- `explorar(...)`: recebe um planeta ou lista de planetas e retorna recursos coletados, considerando o combustível disponível

#### Regras de movimentação:

- A nave tenta visitar os planetas seguindo uma determinada **prioridade** (posição, valor total ou valor por peso)
- Se o combustível for insuficiente, a nave vai até onde puder
- Após a missão, tenta retornar à base (posição 0)

---

## 🧪 Testes Obrigatórios

Para garantir o funcionamento correto da simulação, os seguintes testes estão presentes:

- `deveFicarADerivaQuandoFaltarCombustivelParaIrAteUmPlaneta`
- `deveTerValorTotalZeradoQuandoNaoExistirNenhumRecurso`
- `deveTerValorTotalQuandoExistirRecursosNoPlaneta`
- `deveTerValorPorPesoZeradoQuandoNaoExistirNenhumRecurso`
- `deveTerValorPorPesoQuandoExistirRecursosNoPlaneta`

### 🧾 Exemplo de Teste

```java
@Test
public void deveFicarADerivaQuandoFaltarCombustivelParaIrAteUmPlaneta() {
    int posicaoEsperada = 3;
    int combustivelEsperado = 1;
    Nave milleniumFalcon = new Nave(10);
    Planeta tatooine = new Planeta(4, new ArrayList<>());

    List<Recurso> recursos = milleniumFalcon.explorar(tatooine);

    Assert.assertTrue(recursos.isEmpty());
    Assert.assertEquals(combustivelEsperado, milleniumFalcon.getQuantidadeDeCombustivel());
    Assert.assertEquals(posicaoEsperada, milleniumFalcon.getPosicao());
}
```

## 🎯 Bônus: Estratégias de Exploração

Ao passar uma lista de planetas para `explorar`, é possível priorizá-los de acordo com:

- **Posição**
- **Valor total**
- **Valor por peso**

Diferentes estratégias afetam a quantidade final de combustível. Testes devem comprovar essa variação.
