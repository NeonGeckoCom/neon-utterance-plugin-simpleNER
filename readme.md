```python

ner = SimpleNERTagger()
for utt in [
    "The LHC smashes proton beams at 12.8–13.0 TeV",
    "The first man to walk on the moon was Neil Armstrong",
    "Isaac Newton discovered gravity, that is the reason humans don't float"
]:
    print(ner.transform([utt]))
```