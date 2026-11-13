A Large Language Model (LLM) is a sophisticated mathematical algorithm that predicts what word comes next for any piece of text. An LLM assigns a probability to an array of words and picks the next one based on which one is most likely to be correct in context.

Take the sentence:

> Paris is a city in _____

The LLM could then assign the following probabilities:

```
- France: 17%
- the: 10%
- northern: 3%
- Texas: 1%
```

Evidently, the LLM isn't born knowing these probabilities, or anything in general. To the LLM, Paris having a connection to France comes from countless hours of training. LLMs are fed information and data from all kinds of sources: books, websites, articles, magazines, etc.

The amount of training data and therefore the number of parameters available to a given LLM is precisely what makes the difference between something like Claude Sonnet 5.5 or Claude Fable 5.1.

LLMs can have **billions** of parameters available. Evidently, these parameters are not setup by hand, instead, LLMs are trained by receiving an excerpt from one of the aforementioned sources with the last word of the excerpt removed. For example:

> "It was the best of times it was the ..."

The training algorithm knows that the next word is "**worst**", the LLM is then tuned to assign the highest probability to that exact word.
	Interestingly, this is exactly why LLMs can be biased towards beliefs and practices of certain cultures, religions, politics, and much more. For example, roughly 30% of the world's population is Christian, making it the world's largest religion. Assuming that most religious text is also Christian by association, it's no wonder that models like GPT assume God to be Jesus [https://www.ncronline.org/news/ai-has-bias-toward-catholicism-researchers-say].

To avoid biases, parameters can be tweaked so that the LLM is either more or less likely to pick a word as the next candidate.

The text based training phase is typically called "Pretraining". However, an AI assistant that can take action based on given input requires a bit more training than just text-prediction. This is when "Reinforcement Learning with Human Feedback" comes into the picture, known as [[RLHF]].

Before 2017, most LLMs would process text one word at a time. A team of researches at Google then introduced a new model, known as the [[Transformer]] model. Transformers don't read text from start to finish, instead they soak it all in at once in parallel.
	A transformer will associate each word with a long list of numerical values.

