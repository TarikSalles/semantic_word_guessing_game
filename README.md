# Jogo de Adivinhação Semântica com Word Embeddings

Este projeto apresenta uma exploração prática das propriedades geométricas de **Word Embeddings** por meio de um jogo interativo baseado em similaridade vetorial.

Utilizando o modelo pré-treinado **GloVe (glove-wiki-gigaword-100)** da biblioteca `gensim`, palavras são representadas como vetores em um espaço de 100 dimensões (embeddings). O objetivo do jogo é que o usuário a encontre uma palavra semanticamente próxima da soma vetorial de duas palavras fornecidas (os embeddings de palavras provam seguirem lógicas e associações humanas em diversos casos).

---

## Instalação

Clone o repositório:

```bash
git clone https://github.com/TarikSalles/semantic-word-guessing-game
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

---

## Fundamento Matemático

Cada palavra é representada como um vetor:

w ∈ ℝ¹⁰⁰

A similaridade entre palavras é calculada utilizando **similaridade de cosseno**:

cos(u, v) = (u · v) / (||u|| ||v||)

No jogo, duas palavras w₁ e w₂ são combinadas:

v = w₁ + w₂

O jogador deve encontrar uma palavra w₃ tal que:

cos(w₃, v) ≥ 0.60

Ou seja, a palavra escolhida deve estar suficientemente próxima da soma vetorial das duas palavras iniciais.

---

## Estrutura do Jogo

O jogo funciona da seguinte forma:

1. Uma categoria é escolhida aleatoriamente entre:
   - Objetos
   - Comidas
   - Profissões

2. Duas palavras da mesma categoria são selecionadas.

3. O sistema verifica se existe uma terceira palavra cuja similaridade de cosseno com a soma vetorial seja ≥ 0.60 (todas as palavras do dicionário inglês são percorridas).

4. O jogador deve tentar adivinhar essa palavra ou uma palavra que possua pelo menos uma similaridade de 60% com essa soma vetorial.

5. Caso acerte, recebe pontuação proporcional à similaridade:

   Pontos = similaridade × 1000

6. O jogador possui 3 vidas.

7. É possível chamar os jurados uma única vez por jogo:
   - 50% de chance de receber uma dica útil (palavra entre as top similares)
   - 50% de chance de receber uma palavra aleatória

---

## Observações Importantes

Durante os testes foi observado que:

- Nem sempre a soma vetorial gera uma palavra composta literal.
- O modelo aprende padrões estatísticos de coocorrência e às vezes palavras semelhantes não fazem sentido direto.
- Relações lineares funcionam melhor quando há forte estrutura semântica.

Exemplo observado:

man + sales ≈ salesman (mais de 40% de semelhança)

computer + scientist ≈ programmer (mais de 60% de semelhança)

Mas nem sempre a composição morfológica é capturada perfeitamente.

---

## Tecnologias Utilizadas

- Python
- NumPy
- Gensim
- Jupyter Notebook
