# DWC-OWL-RDF

An effort to use terms from [an ontology that is based on Darwin Core terms](https://github.com/aminem0/dwc-owl) in order to semantically describe biodiversity datasets.

Given that this project is developped in conjunction with the ontology, any modifications to the ontology will be reflected in these examples.

## Test datasets

- **Broke-West fish campaign**: the Darwin Core DataPackage was downloaded [from the test IPT](https://dwcdp-ipt.gbif-test.org/resource?r=broke-west-fish).
- **Insektmobilen**: The files were obtained from the Darwin Core DataPackage examples [GitHub repository](https://github.com/gbif/dwc-dp-examples/tree/master/survey/insektmobilen/output_data). The data were arranged so as to be csv files with utf-8 encoding as if they were in a DataPackage file. Also, some additional classes were considered, such as dwc:Agent and dwc:UsagePolicy.
- **Orford raccoon captures**: The dataset is a two-year mark–recapture monitoring of raccoons (*Procyon lotor*) in Orford, Québec, including morphometric data measurements taken on each individual. An Excel spreadsheet was provided by Pr. Fanie Pelletier of Université de Sherbrooke. The data were standardized and mapped to DwCDP terms and then to the DWC-OWL ontology.
- **Viridian forest survey**: The dataset consists of a forest survey for bug and flying Pokémon done by Ash Ketchum in Viridian forest. The Darwin Core DataPackage was obtained [from the test IPT](https://dwcdp-ipt.gbif-test.org/resource?r=viridian-forest-survey).

## Importance of the ontology

The Viridian forest survey is exceptionally good, because it is small enough to let us view the labelled edges.

![Labeled graph of the Viridian forest survey](images/viridian-labeled-graph.png)

As can be seen, the graph reads like a book, and tells exactly the story researchers want it to say. This is crucial, as if biodiversity data is to be shared and reused among fellow researchers, first and foremost it needs to be fully understood. The set of terms in Darwin Core and the recently proposed Darwin Core DataPackage allow for the articulation of how the data are meant to be understood. To that end, the ontology in DWC-OWL allows for complex linking and possibly querying of these entities, maximizing reuse potential.

## Real-world datasets

Whereas the Viridian forest survey dataset contained `251` triples, the Broke-West fish dataset contains `173 062` triples and considers more classes. Despite this, the same underlying logic can be applied to obtain a directional graph as well, which faithfully describes the dataset.

![Directed graph of the Broke-West fish dataset](images/broke-directed-graph.png)

The Insektmobilen dataset produced an extremely high number of triples, due to its identification related to barcoding. Indeed, graphical representation of a subset produced `266 130` triples.

![Directed graph of the Insektmobilen dataset](images/insektmobilen-directed-graph.png)

The raccon dataset showed several dwc:OrganismAssertions linked to individual dwc:Organisms. It represents a particularly useful method to represent repeated measures on the same individuals.

![Directed graph of the raccoon dataset](images/raccoon-directed-graph.png)
