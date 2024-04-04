# lkycic-ors-project

To start with, I tried several models available on huggingface for sentiment analysis and decided on the 'adam-chell/tweet-sentiment-analyzer' which seemed to be the most robust and reliable when dealing with all tweets. I also noticed that since this model has already been finetuned specifically for tweets and the sort of language that is used there- there isn't quite a need for us to train any model being used for sentiment analysis using our own data.

For topic classification however, have a look at the following:

In the file ```topiccfnb.ipynb``` there's an implementation of the 'MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7' classification model that takes in a list of topics and then based on the weights from the pre-trained model churns out relative probabilitu that each tweet is related to that topic.

After that, since for our usecase ultimately we don't want to just classify tweets in one topic but instead have a holistic outlook of the tweet to see if it could be related to outdoor recreation spaces, I create a list of weights for each topic's importance. This for now, is just a random list of weights but upon combining it with some of the topic classificationr results we have got from textblob we could refine these.

Using these weights we can generate one single weight for each tweet to see if it's related to ORS or not. Once this is done, we generate two sets of data one for training and one for testing.

We then go over to the ```finetuningbert.ipynb``` where we train using the two generated training and testing datasets where we basically treat them as a source of truth and hope for a good model. In either case, the model that's finetuned on our own dataset should still be better at our classification related to identifying tweets related to ORS.

### Things to Note

Please note that in the current implementation, we are only using 6 tweets at a time since the computation requirement for running it on the whole dataset is quite large. I have been having quite some issues with my own personal system where it just crashes or hangs and hence have not been able to produce comprehensive results and not at all run the finetuningbert file. I hope you can try this yoruselves using the same files on better systems and gather some results!