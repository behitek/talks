# NLP Fundamentals Speaker Transcript

Date: 2026-03-31

## Purpose

This file is a practical speaking script for the seminar. It is written so the presenter can follow it directly during the talk without needing to improvise too much.

The whole talk follows one story:

`Why does the word "bank" seem simple to us, but difficult for a model once meaning depends on context?`

Use this sentence several times during the talk:

`The model does not start with meaning. It starts with representation.`

## How To Use This Script

- You do not need to memorize everything
- Read the `Main script` lines as your default speech
- Use the `Short backup` lines if you want a simpler sentence
- If you forget something, jump to the next section and continue

## 1. Opening

### Slide 1: Opening puzzle

Main script:

Let me start with one question. Why does the word "bank" seem simple to us, but difficult for a model? For us, this word feels easy because we use context naturally. But a model does not begin with that same human intuition. This is the main question for the whole seminar.

Short backup:

Our main question is why the word "bank" becomes difficult for a model.

### Slide 2: Pause and think

Main script:

Please do not answer this question yet. Just keep it in your mind. I want the answer to become clearer step by step. At the end of the talk, we will return to this same question and answer it with a better framework.

Short backup:

Please keep this puzzle in mind. We will answer it at the end.

### Slide 3: Why this matters

Main script:

This is not only an academic question. This matters in search, retrieval, classification, and many practical systems. Real text is full of ambiguity. The same word can mean different things in different situations. As highlighted in the core premise on screen, the challenge is often not only language itself. The challenge is how language is represented inside the model.

Short backup:

This matters because many practical systems depend on how text is represented.

### Slide 4: Session map

Main script:

The talk has four parts. First, the opening puzzle. Second, the concept block, where we build the mental model. Third, a guided interactive demo, where we test the ideas. And finally, the closing, where we return to the original puzzle. Inside the concept block, we will move through three stages: how text becomes numbers, how meaning becomes geometry, and why context changes the answer.

Short backup:

We will go from text to numbers, then vectors, then context, and then back to the original puzzle.

### Slide 5: Title lockup

Main script:

Before we go deeper, here is the session in one sentence. Today I want to build a practical mental model for how text becomes pieces, vectors, and context. If we keep that sentence in mind, the later examples will feel like parts of one story rather than isolated NLP terms.

Short backup:

Today is about a practical mental model for text, vectors, and context.

Transition:

Now let us start with the most basic question. How can a machine use text at all?

## 2. Concept Block

### 2.1 How Text Becomes Numbers

### Slide 6: Text versus machine view

Main script:

Humans read text as meaning. We see words, phrases, intent, and context very quickly. A model does not start that way. A model needs some numeric form that it can process. So before we talk about meaning, we first need to talk about representation. This is a very important idea for the whole seminar. The model does not start with meaning. It starts with representation.

Short backup:

Humans start with meaning. Models start with representation.

### Slide 7: Conversion pipeline

Main script:

The basic flow is simple. First, text is split into pieces. Then those pieces are mapped into numbers. Then those numbers can be compared, transformed, or used by downstream tasks. So when we ask why two strings look different to a model, we are really asking where in this pipeline that difference appears.

Short backup:

The flow is text, then pieces, then numbers, then comparison.

### Slide 8: Progression of methods

Main script:

As we move through Bag of Words, TF-IDF, word2vec, and contextual embeddings, I want to keep one question in mind. What problem does each new method solve that the previous one could not solve well? This question is useful because it makes the methods feel like a progression, not just a list of NLP terms.

Short backup:

For each method, ask: what new problem does it solve?

### Slide 9: Bag of Words intuition

Main script:

Bag of Words is one of the simplest ways to represent text. The idea is very direct. We represent a document by counting which words appear and how often they appear. This already gives us something machine-friendly. It turns text into a structured numeric form. So as a first step, it is useful.

Short backup:

Bag of Words means representing text using word counts.

### Slide 10: Bag of Words example visual

Main script:

Look at the table. We have three short phrases — "river bank", "bank loan", "loan account". Our vocabulary has eight words: bank, river, loan, account, water, money, flood, credit. Now look at how many cells are zero. Each phrase only touches two of those eight columns. The dimmed zeros are not empty — they are real data points. The model sees them as meaningful absence. In a real corpus of millions of words and thousands of documents, almost every single cell would be zero. That is what sparse means. And there is something else to notice here. Doc A and Doc B both have "bank" — so their count patterns look similar. But one is about a river and one is about finance. Bag of Words cannot see that difference. We will come back to that.

Short backup:

Most cells are zero — that is sparsity. And two very different documents can look similar just because they share one word.

### Slide 11: Bag of Words limitations

Main script:

But Bag of Words has clear limits. It does not naturally capture word order. It does not understand that two different words can have related meaning. And it does not handle context well. As highlighted on the right side of the slide, this is the tradeoff of sparse limits: we gain a machine-friendly numeric snapshot, but completely drop human intent. To the model, these are just isolated buckets with no mechanism to connect related meanings. This is the first place where we feel the gap between surface form and deeper representation.

Short backup:

Bag of Words captures appearance, but drops human intent. To the model, they are just isolated buckets.

### Slide 12: TF-IDF intuition

Main script:

TF-IDF improves the weighting. It says that not all words should contribute equally. Very common words usually carry less information, while rarer and more topic-specific words may carry more signal. If my query is about river bank erosion, then words like `river` and `erosion` should carry more of the score than a generic word like `the`. So TF-IDF does not change the basic count-based representation, but it makes the weighting much more useful.

Short backup:

TF-IDF says some words should matter more than others.

### Slide 13: TF-IDF contrast example

Main script:

This is an important improvement, because many common words appear everywhere and do not tell us much. If the query is `river bank erosion`, TF-IDF should rank a river document above a loan document, even though both contain the word `bank`. That is better ranking. But even after this improvement, we still have a sparse, surface-based view. The model still does not naturally know that `doctor` and `physician` are related, and it still does not truly separate the two meanings of `bank`.

Short backup:

TF-IDF improves ranking, but it still does not create semantic closeness.

### Slide 14: Sparse methods hit a ceiling

Main script:

This is where sparse methods start to hit a ceiling. They can separate texts, but they do not naturally place similar meanings near each other. That is the key limitation. We need a representation where related usage can become geometric closeness. That is what leads us to embeddings.

Short backup:

Sparse methods help, but they do not naturally create semantic neighborhoods.

Transition:

Sparse methods give us a useful structure, but they are not enough. Next we talk about representations.

### 2.2 Geometry of Meaning

### Slide 15: word2vec intuition

Main script:

word2vec changes the story in an important way. Instead of representing words mainly as sparse count positions, it learns dense vectors. The intuition is that words appearing in similar contexts tend to get similar vectors. This is a big shift. Meaning starts to become geometry.

Short backup:

word2vec learns vectors, and similar usage can lead to similar vectors.

### Slide 16: How word2vec learns

Main script:

Now the obvious question is: how does word2vec actually learn those vectors? The answer is through a prediction task. There are two common approaches. The first is CBOW, or Continuous Bag of Words. You give the model several context words around a gap, and it tries to predict the missing center word. The second is Skip-gram. You give the model a center word, and it tries to predict which words tend to appear around it. In both cases, the model has to adjust its internal representation of each word every time it gets a prediction right or wrong. After millions of these adjustments, words that appear in similar situations end up with similar vectors.

Short backup:

word2vec trains by predicting context. The vectors are a side effect of learning to predict.

Transition:

So now we understand where the vectors come from. Next, let us look at what they represent.

### Slide 17: Meaning becomes geometry

Main script:

Now we are no longer thinking only in terms of counts. We are thinking in terms of positions in a space. If two words are used in similar ways, they may end up closer together. If two words behave very differently, they may end up farther apart. So now meaning is represented as geometry, at least in a useful approximate sense.

Short backup:

In embeddings, related usage often becomes closeness in vector space.

### Slide 18: Cluster visual

Main script:

A cluster picture is useful here. We can imagine related words appearing near each other in a space. This does not mean the model has human understanding. But it does mean the model has learned useful statistical structure. That structure is often enough to support search, retrieval, or similarity tasks.

Short backup:

Clusters show that related terms can become neighbors in embedding space.

### Slide 19: Near-versus-far example

Main script:

Before introducing any formula, I want to make the comparison problem concrete. `car` and `automobile` should feel very near. `doctor` and `physician` should also feel near. `bank` and `money` may feel somewhat close because they often appear in finance contexts. `bank` and `river` are more interesting because the relationship depends on which sense we mean. So once we accept the idea of near and far, the next question becomes very natural: how exactly do we measure that closeness?

Short backup:

Once we see near and far in the space, we need a way to measure closeness.

### Slide 20: Cosine similarity

Main script:

Once we have vectors, we need a way to compare them. One common method is cosine similarity. The idea is simple. Instead of focusing mainly on raw size, we ask whether two vectors point in a similar direction. As the visual illustrates, a smaller angle between the vectors means a higher cosine similarity. If they do point in a similar direction, the cosine similarity is high. If they do not, it is lower.

Short backup:

Cosine similarity asks how similar the vector directions are—a smaller angle means a higher cosine.

### Slide 21: What cosine similarity measures

Main script:

This is a useful comparison, but we should be precise about what it means. High cosine similarity suggests that two vectors are related in the learned representation. It does not automatically mean deep understanding. It means the model has learned a useful statistical closeness.

Short backup:

High cosine similarity means useful closeness, not human-like understanding.

### Slide 22: Analogy and caveat

Main script:

The classic example is king minus man plus woman is close to queen, as illustrated by the vector relationships shown here. This example is memorable because it shows that vector spaces can capture interesting patterns. But we should be careful. The model is learning statistical structure from data. It is not proving that it understands concepts the way a human does. So this example is useful, but it should not be overinterpreted.

Short backup:

The analogy example is useful, but it reflects learned structure, not real understanding. The visual shows how these vectors relate.

### Slide 23: Geometry takeaway

Main script:

So the main lesson in this section is that embeddings let us represent related usage as geometric closeness. This is much more expressive than simple counts. But it still has an important limit. A single word can have more than one meaning, and a single fixed vector may not be enough.

Short backup:

Embeddings are more powerful than counts, but one fixed vector can still be too simple.

Transition:

That brings us to the next problem. What happens when the same word means different things?

### 2.3 Static vs Contextual Embeddings

### Slide 24: Static embedding limitation

Main script:

In static embeddings, one word usually gets one vector. This is already much better than simple sparse counts. But it also means the representation is fixed. The model cannot fully adapt the meaning of that word based on the surrounding words.

Short backup:

Static embeddings are useful, but one word still gets one fixed representation.

### Slide 25: One word, one vector problem

Main script:

This is where the limitation becomes clear. Human language is full of ambiguity. The same surface form can have different meanings in different situations. The word `bank` might need one set of signals for river, water, and shore, and a different set of signals for loan, account, and money. But if the model always uses one fixed vector, then those two patterns get compressed into one compromise representation.

Short backup:

One fixed vector compresses different meanings together.

### Slide 26: Contextual embeddings idea

Main script:

Contextual embeddings change this idea. The representation of a word is allowed to depend on the words around it. If the surrounding words are things like `river` and `erosion`, the representation of `bank` should lean in one direction. If the surrounding words are `account` and `loan`, it should lean in another. So now we no longer say one word always has one meaning representation. Instead, we say the representation is influenced by context.

Short backup:

In contextual embeddings, surrounding words help define the representation.

### Slide 27: The bank contrast

Main script:

This is why the word "bank" is such a useful example. In the sentence "He sat by the river bank," the meaning is about a place near water. In the sentence "She opened a bank account," the meaning is about a financial institution. The word is the same on the surface, but the intended meaning is different. A better representation should reflect that difference.

Short backup:

Same word surface, different context, different meaning.

### Slide 28: BERT introduction

Main script:

So the idea is that surrounding words should influence the representation. That model is BERT — Bidirectional Encoder Representations from Transformers. I am not going to explain the architecture today. What matters for this session is the intuition. word2vec gives "bank" one fixed vector — the same one every time. BERT reads the whole sentence and produces a different vector for "bank" depending on what surrounds it. In "river bank", the representation leans toward geography. In "bank account", it leans toward finance. The word on the surface is identical. The representation is not. That is the key shift.

Short backup:

BERT produces different vectors for the same word depending on the surrounding sentence. word2vec cannot do this.

Transition:

Now, what about the pieces themselves?

### Slide 29: How BERT learns — Masked LM

Main script:

But how does BERT actually learn to do this? BERT is trained using a technique called Masked Language Modeling, or MLM. The idea is simple. Take a sentence, hide one of the words by replacing it with a special MASK token, and ask the model to predict what the hidden word was. For example, in the sentence "He sat by the [MASK] bank", the correct answer is "river". For BERT to predict that correctly, it needs to read the whole surrounding sentence and understand that this is a geographical context, not a financial one. By doing this across billions of sentences, BERT gets very good at encoding context into its representations.

Short backup:

BERT is trained to predict hidden words. To do that it must read the full sentence. That is how contextual representations emerge.

### Slide 30: BPE tokenization

Main script:

Modern models didn't just change the numbers — they also changed the pieces. Bag of Words and TF-IDF treated each whole word as a single unit. Modern models use subword tokenization instead. There are two common strategies. The first is BPE, or Byte Pair Encoding, used by models like GPT-2. It learns to merge the most frequent pairs of characters or subwords until it reaches a target vocabulary size. The second is WordPiece, used by BERT. It works similarly but marks continuation subwords with a double hash prefix, like hash hash ing. That prefix makes it explicit which pieces belong together as part of one word. For example, the word banking might split into bank and hash hash ing. The hash hash tells you that the second piece is a suffix, not a standalone token. In BPE, the pieces just sit next to each other with no such marker. Before any meaning is calculated, the model already starts with these internal units.

Short backup:

Both BPE and WordPiece split rare words into subword pieces. WordPiece uses the ## prefix to mark continuation pieces. That is the actual starting point before meaning begins.

### Slide 31: Static versus contextual summary

Main script:

So the contrast is clear. The shared image on this slide makes the difference visible with one word: `apple`. In the static view, there is one reusable point, so company and fruit meaning are forced into the same representation. In the contextual view, those meanings can separate because the surrounding words help decide which sense we mean. That is the same reason later examples like `dog bites man` and `man bites dog` no longer collapse into the same bag. Contextual embeddings let the sentence shape the representation, which is why they are better at ambiguity, word order, nuance, and polysemy.

Short backup:

One image, two stories: fixed word vector on the left, sentence-shaped meaning on the right.

### Slide 32: Why context matters in practice

Main script:

This matters in many practical tasks. It matters in matching names and abbreviations. It matters in search. It matters in retrieval and classification. In real systems, surface form alone is often not enough. The surrounding context changes what the text should mean for the model.

Short backup:

Context matters because real systems depend on meaning in use, not only surface form.

### Slide 33: Puzzle checkpoint

Main script:

Now we can connect this back to the original puzzle. Humans can handle the word "bank" very easily because we use context without thinking. But a model only sees what the representation allows it to see. A fixed embedding may compress multiple meanings into one vector. A contextual model can separate those meanings more effectively. That is why representation and context matter so much.

Short backup:

The puzzle depends on tokenization, representation, similarity, and context.

Transition:

Next, let us test these ideas in a small interactive demo.

## 3. Guided Interactive Demo

### Slide 34: Demo roadmap

Main script:

The purpose of the demo is not to add new theory. The purpose is to make the earlier ideas concrete. We will use a small interactive website with three main views. First, tokenization. Second, similarity. Third, context. If time allows, we can also look at a simple embedding map.

Short backup:

The demo is here to test the ideas from the concept section.

## Demo-specific transcript

Use the companion browser-first demo transcript immediately after slide 34.

## Live Demo Run Script

Use this immediately after slide 34.

Primary presenter surface:

- browser guided demo route `?demo=1`

Backup / deep-dive surface:

- `nlp_live_demo.ipynb`

Use the notebook only when you need arbitrary audience inputs, Colab, or a deeper off-script comparison.

High-level live flow:

1. tokenization
2. similarity / nearest neighbors
3. context comparison for `bank`
4. optional embedding map

Suggested live framing while the demo is on screen:

- Tokenization: Compare examples like "bank", "river bank", and "bank account" so the audience can see that different strings can already become different token pieces before meaning shows up.
- Similarity: Use word-level pairs such as "car" and "automobile", "doctor" and "physician", "bank" and "money", or "bank" and "river", and ask for a guess before revealing the cosine score.
- Context: Compare "He sat by the river bank" with "She opened a bank account" to show that the same surface word can take on different internal representations when the surrounding words change.
- Optional map: If you show a UMAP-style view, frame it as intuition only, not the full original geometry.

Transition back to closing:

Now that we have seen tokenization, similarity, and context in one guided flow, we can return to the original puzzle. The question is no longer just whether the model is right or wrong. The better question is what the representation makes easy, and what it makes hard.

## 4. Closing

### Slide 35: Return to the opening puzzle

Main script:

Now let us return to the first question. Why does the word "bank" become difficult for a model once meaning depends on context? At this point, the answer should feel less mysterious. We now have a framework for it.

Short backup:

Now we can answer the original puzzle with a better framework.

### Slide 36: Answer framework

Main script:

First, tokenization. The input does not reach the model in the same form that we read it, so `bank`, `river bank`, and `bank account` do not all begin from exactly the same internal units. Second, representation. In older static methods, one word may get one fixed vector or one sparse pattern. Third, similarity. That representation can be close to some meanings and far from others, so `bank` may look closer to finance words than to river words depending on the representation. Fourth, context. In contextual models, the surrounding words help shape how the model interprets `bank` in each sentence. So the issue is not that the model is simply wrong. The issue is that representation choices make some distinctions easy and other distinctions hard.

Short backup:

The answer is tokenization, representation, similarity, and context.

### Slide 37: Reflection and Q&A

Main script:

So the final message is this. Modern NLP is not magic. It is representation, geometry, and context at scale. If we understand that, we can reason more clearly about what these systems do well, where they fail, and why. I want to close with one reflection question: what assumption about language models changed for you today?

Short backup:

Modern NLP is representation, geometry, and context at scale.

## Very Short Backup Script

Use this only if you want a much simpler script:

1. Today I want to answer one question: why does the word "bank" become difficult for a model?
2. A model does not start with meaning. It starts with representation.
3. First, text becomes numbers.
4. Then meaning becomes geometry in vector space.
5. Then we see that one word can have different meanings, so context matters.
6. The demo shows tokenization, similarity, and context in action.
7. The final answer is tokenization, representation, similarity, and context.
