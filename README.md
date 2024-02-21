# BigSMARTS: A Topologically Aware Query Language and Substructure Search Algorithm for Polymer Chemical Structures

# Journal Article
https://pubs.acs.org/doi/10.1021/acs.jcim.3c00978

# Description
Molecular search is important in chemistry, biology, and informatics for identifying molecular structures within large data sets, improving knowledge discovery and innovation, and making chemical data FAIR (findable, accessible, interoperable, reusable). Search algorithms for polymers are significantly less developed than those for small molecules because polymer search relies on searching by polymer name, which can be challenging because polymer naming is overly broad (i.e., polyethylene), complicated for complex chemical structures, and often does not correspond to official IUPAC conventions. Chemical structure search in polymers is limited to substructures, such as monomers, without awareness of connectivity or topology. This work introduces a novel query language and graph traversal search algorithm for polymers that provides the first search method able to fully capture all of the chemical structures present in polymers. The BigSMARTS query language, an extension of the small-molecule SMARTS language, allows users to write queries that localize monomer and functional group searches to different parts of the polymer, like the middle block of a triblock, the side chain of a graft, and the backbone of a repeat unit. The substructure search algorithm is based on the traversal of graph representations of the generating functions for the stochastic graphs of polymers. Operationally, the algorithm first identifies cycles representing the monomers and then the end groups and finally performs a depth-first search to match entire subgraphs. To validate the algorithm, hundreds of queries were searched against hundreds of target chemistries and topologies from the literature, with approximately 440,000 query–target pairs. This tool provides a detailed algorithm that can be implemented in search engines to provide search results with full matching of the monomer connectivity and polymer topology.

# Data Collection and Organization
- The validation spreadsheet contains a matrix of query and target polymer searches that validate the substructure search algorithm, not yet released.
- The tabs are classified by query topology, including single stochastic object (homopolymer, random copolymer, AA-BB copolymer), block, graft, star, and polymer network. 
- The queries in row 1 are written in BigSMARTS line notation, and the targets in column A are written in BigSMILES line notation. Every BigSMARTS is searched in all BigSMILES.
- Every BigSMARTS query tests a rule; for example, cyclic permutations, monomer splits, inversions, and frame shifts should not affect the number of matches.
- Every BigSMILES target is a real polymer from peer-reviewed scientific literature, with the source written.
- A 0 or a 1 is handwritten depending on whether a substructure match is expected between the query and target. The substructure search algorithm validates this.

# Test Cases

BigSMARTS queries can be written with increasing restriction on the target ensemble depending on the grammatical elements used.

| BigSMARTS | Meaning| # BigSMILES Hits |
| :---- | :---: | :---: |
| CCO | SMARTS that searches an entire BigSMILES | 207 |
| {[]CCO[]} | localizes hits to the repeat units | 198 |
| {[][<]CCO[>][]} | localizes hits to the target repeat unit backbones | 68 |
| {[][<][CH2][CH2]O[>][]} | prevents matches to pendant groups not specified in the query | 57 |
| {[][<][CH2][CH2]O[>],!\*[]} | prevents matches to extra repeat units not specified in the query | 45 |
| {[][<][CH2][CH2]O[>],!\*\;!\*[]} | prevents matches to extra repeat units and end groups not specified in the query | 1 |

Different string representations of the same molecular ensemble will not affect the number of matches.

| BigSMARTS | Change | # BigSMILES Hits |
| :---- | :---: | :---:
| {[][<]CCO[>][]} | PEG backbone search | 68 |
| {[][>]CCO[<][]} | change in bonding descriptors | 68 |
| {[][<]COC[>][]} | frame shift | 68 |
| {[][<]OCC[>][]} | inversion | 68 |
| {[][<]C[<2],[>2]CO[>][]} | split | 68 |
| {[][<]CCO[>],[<]CCO[>][]} | duplication | 68 |

These are simple cases, but there is no restriction on the number of repeat units and end groups in the query and target, greatly increasing the complexity of search. The algorithm handles all of these cases.

# Repository Location
http://doi.org/10.5281/zenodo.4780309

# Creators
- Nathan J. Rebello (https://orcid.org/0000-0002-0178-7701)
- Tzyy-Shyang Lin (https://orcid.org/0000-0002-8265-6702)
- Heeba Nazeer (hn1@wellesley.edu)
- Bradley D. Olsen (https://orcid.org/0000-0002-7272-7140)

# Rights
The dataset is released under CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/) in Zenodo (http://doi.org/10.5281/zenodo.4780309).
