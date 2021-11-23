# Portuguese Neural Machine Translation: Translator Qualitative Analysis

1. [Introduction](#introduction)
    1. [Disclaimer](#disclaimer)
1. [Error descriptions](#error-descriptions)
1. [Translation examples and qualitative evaluation](#qualitative-evaluation)

<a id="introduction"></a>
## Introduction

This repository contains further details about the qualitative analysis performed for the paper "Tackling neural machine translation in low-resource settings: Portuguese case study". It contains a description of the errors identified and one sentence per complexity level.

<a id="disclaimer"></a>
### Disclaimer

The goal of this documentation is to just hold a brief summary of the sentences that the translator has classified with respect to complexity and errors, and the reason behind the classification. Only a sentence per complexity level is available here (4 sentences). If the reader is looking for more examples, please check [this spreadsheet](https://docs.google.com/spreadsheets/d/1LOYKcWYwHbLAuI8vAg0Fp0MDz-TtXzutwlmptLyd3_Q/edit#gid=1133528615).

<a id="error-descriptions"></a>
## Error descriptions

The table below contains a detailed description of the error types created.

| Error type        | Description |
| ----------------- | ----------- |
| Similar word choice | A similar, related word was used in a context where it makes sense, but is different from the reference, or the order of words are switched. **Renamed to REFERENCE MATCHING error in dissertation when compared to the paper.**  |
| Omission            | Happens when the model simply ignores part of the source sentence, and it simply doesn’t appear in the model guess. |
| Out of context      | The model uses a word that doesn’t fit in the surrounding context, and the translation loses cohesion. This error also contemplates inexistent words created by BPE. |
| Verb tense      | When conjugating a verb, the model misses to capture the right tense and changes it on its guess, generating an innaccurate translation. |
| Sentence choice      | The model translates a sequence that is way different from the expected translation. This usually happens when several word choice errors are committed and to preserve cohesion between words, the final sentence result significantly lose its meaning when compared to the source sentence. **Renamed to MEANING DEVIATION error in dissertation when compared to the paper.** |
| Insertion      | This category indicates that the algorithm has inserted words that are unnecessary given the context. |
| Repetition      | Happens when the likelihood estimate of the next translation becomes biased, inducing the model to keep translating the same set of words more than once. |

<a id="qualitative-evaluation"></a>
## Translation examples and qualitative evaluation

In order to perform the qualitative analysis, random samples were extracted from TED, analysed by a human translator and stratified according to [CEFR scale](https://www.coe.int/en/web/common-european-framework-reference-languages/level-descriptions). As TED Talks is a dataset that contains **orally spoken** sentences, it is **rare to find very complex english sentences**, so the study was initially limited to sentences belonging to the levels A1, A2, B1 and B2. One C1 example is present in this material just for the reader to understand the criteria used.

For illustration purposes, one example from each sentence complexity was taken from the dataset and classified with respect to complexity and error class. It is curious to observe that sometimes even the reference has errors, which can be considerd a flaw in the way we evaluate model performance. The explanations for both and the respective category chosen for the sentence are displayed in the following table:

| Original sentence        | Reference                 | Model guess                  | Model Type           | Complexity and reason | English error classification                                                                 |
|----|-----|-----|-----|-----|-----|
| Você não muda nunca, né? | You never change, do you? | You don't change it, do you? | Transformer with BPE | A1 - Simple present   | 1) Insertion error: "it" was added. 2) Similar word choice (reference matching): Never/Don't are close in meaning |
| Tente perguntar coisas assim: "Como é que foi aquilo" ? | try asking them things like, "what was that like?" | try to ask things like this: "how is it that?" | Transformer with BPE | A2 - ING used as infinitive and intermediate level question in Simple Past  | 1) Verb Tense Error: model changes ING infinitive (try asking) for TO infinitive (try to ask). Omission Error: model omitted "them". 2) Insertion Error: the model inserted "this". 3) Sentence Choice (meaning deviation) Error: "what was that like?" was changed to  "how is it that?" |
| E vocês sabem, uma epifania é normalmente algo que encontramos que tínhamos deixado cair em algum lugar. | And you know, an epiphany is usually something you find that you dropped someplace | And you know, an epiphany is normally something that we've found that we'd left somewhere. | Transformer 66% of TED | B1 - Simple present and simple past, with uncommon vocabulary | 1) Similar word choice (reference matching): usually/normally. 2) Sentence choice (meaning deviation) and Verb tense: The meaning and tense were changed, "you find that you dropped someplace" was replaced for "we've found that we'd left somewhere" |
| Ele tinha acabado de ouvir a primeira e a quarta sinfonia de Beethoven, e veio até o backstage se apresentar. | He had just heard a performance of Beethoven's first and fourth symphonies, and came backstage and introduced himself. | He'd just heard the first one and the fourth symphony of Beethoven, and came to the \<unk> to introduce him. | Transformer 33% of TED | B2 - Past perfect and past simple, with uncommon vocabulary | 1) Omission Error: The model omitted "a performance of" that appears in the original sentence. 2) Unk error. 3) Insertion error: first one. |
| Eu estava lendo esta lista em voz alta para um amigo e minha primeira reação foi rir, era tão ridícula. Mas eu tinha acabado de ler desfigurado, e minha voz falhou e eu tive que parar e me recompor do choque emocional e do impacto que o assalto dessas palavras desencadeou. | I was reading this list out loud to a friend and at first was laughing, it was so ludicrous, but I'd just gotten past "mangled," and my voice broke, and I had to stop and collect myself from the emotional shock and impact that the assault from these words unleashed. | I was reading this list in high voice to a friend and my first reaction was to laugh, it was so ridiculous, but I just had to read \<unk>, and my voice failed and I had to stop and prevent myself from the emotional shock and impact that their words took off. It took off. It was so ridiculous. | Transformer 66% of TED | C1 - Complex structure in Simple Past and Past Perfect, mixed with expressions and uncommon words | 1) Word Choice Error: the model changes "out loud" for "in high voice"/"ludicrous", "ridiculous"/collect" for "prevent". 2) Sentence Choice (meaning deviation) Error: the model changed "and at first was laughing" for "and my first reaction was to laugh", "but i'd just gotten past mangled" for "but i just had to read \<unk>", "and my voice broke" for "and my voice failed", "the emotional shock and impact that the assault from these words unleashed" for "the emotional shock and impact that their words took off". 3) Insertion Error: the model inserted "it took off" and "it was so ridiculous" at the end. 4) Repetition error: took off |
