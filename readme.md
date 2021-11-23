```python

ner = SimpleNERTagger()

# this usually comes from mycroft.conf and is set by transformers service
ner.config = { "units": True, # enable quantulum3 predefined parser
               "rules": {  # user defined rules <- main use case
                   "en": {
                       "name": ["my name is {person}",
                                "my friends call me {person}"]
                   },
                   "pt": {
                       "name": ["o meu nome é {person}",
                                "os meus amigos chamam-me {person}"]
                   }
               }}


for utt in [
    "The LHC smashes proton beams at 12.8–13.0 TeV",
    "my name is Casimiro"]:
    _, context = ner.transform([utt])
    print(context)

    # {'entities': {'Energy:Electronvolt': [{'entity': 'Energy:Electronvolt',
    #                                        'source_text': 'The LHC smashes proton '
    #                                                       'beams at 12.8–13.0 TeV',
    #                                        'span': (32, 45),
    #                                        'value': '12.8–13.0 TeV'}]}}
    # {'entities': {'person': [{'entity': 'person',
    #                           'source_text': 'my name is Casimiro',
    #                           'span': (11, 19),
    #                           'value': 'Casimiro'}]}}
```

A very useful tagger is dbpedia spotlight, however it can be a little spammy

```python

ner = SimpleNERTagger()

# this usually comes from mycroft.conf and is set by transformers service
ner.config = {"spotlight": True}

for utt in ["Isaac Newton discovered gravity, that is the reason humans don't float"]:
    _, context = ner.transform([utt])
    print(context)

    # {'entities': {'DBpedia:Agent': [{'entity': 'DBpedia:Agent',
    #                                  'source_text': 'Isaac Newton discovered '
    #                                                 'gravity, that is the reason '
    #                                                 "humans don't float",
    #                                  'span': (0, 12),
    #                                  'value': 'Isaac Newton'}],
    #               'DBpedia:Person': [{'entity': 'DBpedia:Person',
    #                                   'source_text': 'Isaac Newton discovered '
    #                                                  'gravity, that is the reason '
    #                                                  "humans don't float",
    #                                   'span': (0, 12),
    #                                   'value': 'Isaac Newton'}],
    #               'DBpedia:Scientist': [{'entity': 'DBpedia:Scientist',
    #                                      'source_text': 'Isaac Newton discovered '
    #                                                     'gravity, that is the '
    #                                                     "reason humans don't float",
    #                                      'span': (0, 12),
    #                                      'value': 'Isaac Newton'}],
    #               'DUL:Agent': [{'entity': 'DUL:Agent',
    #                              'source_text': 'Isaac Newton discovered gravity, '
    #                                             "that is the reason humans don't "
    #                                             'float',
    #                              'span': (0, 12),
    #                              'value': 'Isaac Newton'}],
    #               'DUL:NaturalPerson': [{'entity': 'DUL:NaturalPerson',
    #                                      'source_text': 'Isaac Newton discovered '
    #                                                     'gravity, that is the '
    #                                                     "reason humans don't float",
    #                                      'span': (0, 12),
    #                                      'value': 'Isaac Newton'}],
    #               'Http://xmlns.com/foaf/0.1/Person': [{'entity': 'Http://xmlns.com/foaf/0.1/Person',
    #                                                     'source_text': 'Isaac '
    #                                                                    'Newton '
    #                                                                    'discovered '
    #                                                                    'gravity, '
    #                                                                    'that is '
    #                                                                    'the reason '
    #                                                                    'humans '
    #                                                                    "don't "
    #                                                                    'float',
    #                                                     'span': (0, 12),
    #                                                     'value': 'Isaac Newton'}],
    #               'Schema:Person': [{'entity': 'Schema:Person',
    #                                  'source_text': 'Isaac Newton discovered '
    #                                                 'gravity, that is the reason '
    #                                                 "humans don't float",
    #                                  'span': (0, 12),
    #                                  'value': 'Isaac Newton'}],
    #               'Wikidata:Q215627': [{'entity': 'Wikidata:Q215627',
    #                                     'source_text': 'Isaac Newton discovered '
    #                                                    'gravity, that is the '
    #                                                    "reason humans don't float",
    #                                     'span': (0, 12),
    #                                     'value': 'Isaac Newton'}],
    #               'Wikidata:Q24229398': [{'entity': 'Wikidata:Q24229398',
    #                                       'source_text': 'Isaac Newton discovered '
    #                                                      'gravity, that is the '
    #                                                      "reason humans don't "
    #                                                      'float',
    #                                       'span': (0, 12),
    #                                       'value': 'Isaac Newton'}],
    #               'Wikidata:Q5': [{'entity': 'Wikidata:Q5',
    #                                'source_text': 'Isaac Newton discovered '
    #                                               'gravity, that is the reason '
    #                                               "humans don't float",
    #                                'span': (0, 12),
    #                                'value': 'Isaac Newton'}],
    #               'Wikidata:Q901': [{'entity': 'Wikidata:Q901',
    #                                  'source_text': 'Isaac Newton discovered '
    #                                                 'gravity, that is the reason '
    #                                                 "humans don't float",
    #                                  'span': (0, 12),
    #                                  'value': 'Isaac Newton'}]}}

```