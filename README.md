# DWC-OWL-RDF

An effort to use terms from [an ontology that is based on Darwin Core terms](https://github.com/aminem0/dwc-owl) in order to semantically describe biodiversity datasets.

Given that this project is developped in conjunction with the ontology, any modifications to the ontology will be reflected in these examples.

## Test datasets

- **Broke-West fish campaign**: the Darwin Core DataPackage was downloaded [from the test IPT](https://dwcdp-ipt.gbif-test.org/resource?r=broke-west-fish).
- **Crop flower visit**: A dataset of visits of insects to flowering plants in a Japanese orchard. The dataset, as a sampling event Darwin Core Archive was downloaded [from the GBIF website](https://www.gbif.org/dataset/bbaca86c-f703-41fc-800a-fa301c0661fd).
- **Insektmobilen**: The files were obtained from the Darwin Core DataPackage examples [GitHub repository](https://github.com/gbif/dwc-dp-examples/tree/master/survey/insektmobilen/output_data). The data were arranged so as to be csv files with utf-8 encoding as if they were in a DataPackage file. Also, some additional classes were considered, such as dwc:Agent and dwc:UsagePolicy.
- **NMNH paleobiology specimen**: the Darwin Core DataPackage was downloaded [from the test IPT](https://dwcdp-ipt.gbif-test.org/resource?r=paleo-test-a).
- **Turtle movement dataset**: A dataset of geographically tracked sea turtles. The dataset was downloaded in pieces (one .csv file per individual) from the Movebank [through the Tracking Data Map](https://www.movebank.org/cms/webapp/map).
- **Viridian forest survey**: The dataset consists of a forest survey for bug and flying Pokémon done by Ash Ketchum in Viridian forest. The Darwin Core DataPackage was obtained [from the test IPT](https://dwcdp-ipt.gbif-test.org/resource?r=viridian-forest-survey).

## Importance of the ontology

The Viridian forest survey is exceptionally good, because it is small enough to let us view the labelled edges.

![Labeled graph of the Viridian forest survey](images/viridian-labeled-graph.png)

As can be seen, the graph reads like a book, and tells exactly the story researchers want it to say. This is crucial, as if biodiversity data is to be shared and reused among fellow researchers, first and foremost it needs to be fully understood. The set of terms in Darwin Core and the recently proposed Darwin Core DataPackage allow for the articulation of how the data are meant to be understood. To that end, the ontology in DWC-OWL allows for complex linking and eventually querying of these entities, maximizing reuse potential.

## Real-world datasets

Whereas the Viridian forest survey dataset contained `251` triples, the Broke-West fish dataset contains `173 062` triples and considers more classes. Despite this, the same underlying logic can be applied to obtain a directional graph as well, which faithfully describes the dataset.

![Directed graph of the Broke-West fish dataset](images/broke-directed-graph.png)

The Insektmobilen dataset produced an extremely high number of triples, due to its identification related to barcoding. Indeed, graphical representation of a subset produced `266 130` triples.

![Directed graph of the Insektmobilen dataset](images/insektmobilen-directed-graph.png)

The NMNH paleobiology dataset, when expressed as a (somewhat) direct RDF translation of the relational tables in the DataPackage, produced a disconnected graph. The main graph is evident, with around it several subgraphs or even single nodes. Note that this is not an issue for RDF, as these resources are still queriable. Nonetheless, some additional relating of data, such as relating dwc:Identification to the dwc:MaterialEntity on which they are based would connect the isolated subgraphs to the main graph.

![Directed graph of the NMNH paleobiology dataset](images/nmnh-directed-graph.png)

The crop-flower-visit dataset, when expressed as a direct translation of the star-schema based Darwin Core Archive, produced isolated small islands of entities. In each case, there was a central dwc:Event, from which several dwc:MaterialEntities were collected and dwc:Identifications were done on these preserved individuals. Accordingly, these dwc:Identifications form the basis of evidence for the dwc:Occurrence of the taxa at said site. This is what gives rise to the flower-like pattern seen in the graph. To connect these islands of entities, and to do so in a meaningful manner, a dwc:Protocol instance was created and pointed to the original paper of the study.

![Directed graph of the crop-flower-visit dataset](images/crop-directed-graph.png)

In the case of the turtle-remote-sensing dataset, every dwc:Event is a signal from the radio transmitter. Each of these represent a geolocalized occurrence of a particular individual dwc:Organism, whose path can be followed across space and time. This type of data will become particularly important, especially when considering networks that accumulate, study and share this data, such as [Move BON](https://geobon.org/move-bon/).

![Directed graph of the turtle-remote-sensing dataset](images/turtle-directed-graph.png)

## Value of revisiting datasets

The crop-flower-visit dataset was originally published as an sampling event dataset on GBIF, and was registered on September 1st 2023. As it is, the dataset has information not only on insect visitors, but also on several other entities, such as the plants they visited, dwc:Assertions about these plants (the sex of the plant), and the nature of the relationship itself, which is a type of dwc:OrganismInteraction. However, the entirety of this information is provided as free-form text in the data property such as dwc:OccurrenceRemarks.

![Directed graph of the reworked crop-flower-visit dataset](images/cropv2-directed-graph.png)

Extraction of this information and updating of the dataset using DwCDP terms and the DWC-OWL ontology leads to a richer and more expressive dataset. It also leads itself more readily to analyses and querying. For example, a SPARQL query can now target occurrences of insects but only on male Japanese persimmon trees (*Diospyros kaki*). Before, this would have required laborious regexing of the text. Consequently, the use of DwCDP terms and the DWC-OWL ontology should not be seen only as something that should be used from now on, but also as something that researchers can use to make previously published datasets more expressive.