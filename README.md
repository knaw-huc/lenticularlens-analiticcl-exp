# Lenticular Lens - Analiticcl integration experiments

**onderzoeksvraag**: kan de performance van lenticular lens verbeterd worden door gebruik te maken van analiticcl?

**hypothese**: lenticular lens doet momenteel via postgresql een $n \cdot m$ lookup om data1 ($n$) aan data2 ($m$) te koppelen, waarbij elk paar middels levenshtein vergeleken wordt. analiticcl kan in theorie deze vergelijking sneller doen door in eerste instantie gebruik te maken van anagram hashing, waarna maar een kleinere collectie overblijft om daadwerkelijk levenshtein-damarau (en andere metrieken) op te bereken.

**deelvragen**:
    - is de huidige performance van ll überhaupt een probleem?
    - zit de bottleneck qua performance ook echt hier? (dit zou gemeten moeten worden)
    
**baseline experiment**:

* onafhankelijk benchmark experiment aan beide kanten (ll+postgresql vs analiccl)
    *  op dezelfde datasets. welke? eén van de twee kan het beste autoritieve lijst (lexicon) zijn van redelijke omvang. een plaatsnamen gazetteer bv?
    *  op dezelfde machine (ook de postgres!)
    *  in zo vergelijkbaar mogelijke configuraties  (max levenshtein distance etc).
    *  **hypothese:** analiticcl is sneller dan ll+postgresql
    
**integratie experiment**

* analiticcl aanroepen vanuit ll
    * dit betekent dat *alle* te matchen data vanuit postgres aan analiticcl gevoerd moet worden (tenzij het vanuit een derde bron in beide geladen kan worden). dit geeft een overhead waarbij ik me zorgen maak of deze mogelijke performancewinst niet teniet doet.
