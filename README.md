# BDB_Anticancer
Specialized database for anticancer proteins in humans, bovines and C. elegans.
Anticancer.tsv corresponds to the whole anticancer database build from UniProt Database, using the filter: "ANTICANCER" OR "ANTI-CANCER" OR "ANTI CANCER" NOT (organism_id:10090) NOT (organism_id:10116). 
Anticancer.fasta corresponds to peptides less or equal to fifty aminoacids.
If you want to convert from tsv to json, you can use the next command in Python: 
>>> import pandas as pd
>>> proteins= pd.read_csv('Anticancer.tsv', sep='\t')
>>> sequences= proteins.to_json(orient="records")
>>> with open("Anticancer_2.json","w") as output: 
...     output.write(sequences)
later yo can use mongo to search specific information in this database:
mongoimport --db Anticancer --collection proteins --type json --file Anticancer_2.json --jsonArray
db.proteins.find({"Organism": 'Homo sapiens (Human)'})
db.proteins.find({"Reviewed": 'reviewed'})
db.proteins.find({"EC number": {$ne:null}})

