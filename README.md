# Example workflow


## Load ontology
Via GitHub link or local directory

```python
import ontopics as ot
ontology = ot.load_onthology("https://github.com/OpenCS-ontology/OpenCS")
# or 
ontology = ot.load_onthology("onthologies/OpenCS", objects = "", descriptions = "")

data = ot.prepare_topics(ontology, topics: str = "skos:Concept", labels: str = "skos:prefLabel")
```

## Prepare topics for classification

```python
from ontopic.models import TopicEmbedder

model = TopicEmbedder()
# embedding topics from ontology
topics_embedded = model.embed(data)
ot.save_topics(topics_embedded, "onthologies/OpenCS")
```

## Classify text to ontologies

```python
import ontopics as ot
from ontopic.models import TopicalClassifier

topics = ot.load_topics("onthologies/OpenCS")
text = "In this paper we introduce novel NLP NER machine learning model"
model = TopicalClassifier()

# to get top 10 topics, 5 is by default
predictions = model.predict(text, topics, top=10)

# to get topics which are above given threshold of 'probability'
predictions = model.predict(text, topics, threshold=0.2)

# to get topics and also distance
predictions, distance = model.predict(text, topics, distance=True)
```
