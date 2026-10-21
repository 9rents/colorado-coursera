# Probabilistic Models and RNNs: Module Notes

Summary of the module: probability basics, language models, autoregressive image models, recurrent neural networks and sequence-to-sequence models.

## 1. Probability basics

- **Bound vs unbound variables.** A variable in a probability expression is either fixed to a specific value (bound) or left "free" (unbound), in which case the expression describes a distribution over its possible outcomes.
- **Conditional probability `P(A | B)`**: the vertical bar means the probability of A is computed given the values of the variables to the right of the bar.
- **Joint probability `P(A, B)`**: the probability that the events happen together. Its denominator is the global total (all the data); the denominator of a conditional probability is a local aggregate (only the cases where the condition holds). That is why conditional probabilities are easier to estimate: they rely on local counts, not global ones.
- **Chain rule**:

```
P(x1, x2, ..., xn) = P(x1) · P(x2 | x1) · P(x3 | x1, x2) · ... · P(xn | x1..xn-1)
```

  - does not require the events to be independent;
  - is applied recursively, breaking a complex model into simple conditional pieces;
  - in a probability tree each step along a path is a conditional probability, and the product along the path gives the joint probability.
- **Probability trees** show visually how probabilities branch depending on the conditions.

## 2. Language models

- A language model estimates how likely a sentence is, using probabilities.
- The joint probability in a language model is the probability of a sequence of words occurring together.
- By the chain rule it factorizes into a product of conditional probabilities "next word given the previous words".

## 3. Autoregressive image models

- Generate an image sequentially, one pixel (or stroke) at a time, predicting each from those already generated.
- Joint probability of the image = product of the conditional probabilities of all pixels in generation order.
- Estimating the joint distribution directly is hard: the number of possible images is astronomically large. The chain rule solves this.
- Significance: they model an image as a sequence and capture complex dependencies between pixels.

## 4. Recurrent neural networks (RNN)

- The **hidden state** carries information about past steps and is updated incrementally with each new input. Feedback connections feed information back into the network.
- **RNN vs MLP**: an MLP's output depends only on the current input; an RNN's output can depend on all previous inputs.
- **RNN vs batch processing**: a batch processes many independent instances at once and keeps no state between them (stateless). RNNs are chosen when temporal dependencies matter.
- **One-to-many**: a single input produces a sequence of outputs.
- **Long-range dependencies**: information passes through many transformations, so the influence of early inputs fades. The main cause is the **vanishing gradient**.
- **Deep RNNs**: extra hidden layers capture more complex patterns and hierarchical representations.

## 5. Autoregressive RNNs

- Each output is fed back as the input of the next step ("shifted output").
- They rely on temporal dependencies between sequence elements and use hidden states.
- The main challenge is long-range dependencies.
- In language: they predict the next word from the previous ones and can generate coherent, context-appropriate sentences.

## 6. Seq2seq and encoder-decoder

- **Sequence-to-sequence**: transforming a sequence in one domain into a sequence in another (e.g. translation).
- The **encoder-decoder** design handles sequences of variable length.
