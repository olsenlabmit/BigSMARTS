# BigSMARTS: A Topologically Aware Query Language and Substructure Search Algorithm for Polymer Chemical Structures

# Journal Article
https://pubs.acs.org/doi/10.1021/acs.jcim.3c00978

# Description
Molecular search is important in chemistry, biology, and informatics for identifying molecular structures within large data sets, improving knowledge discovery and innovation, and making chemical data FAIR (findable, accessible, interoperable, reusable). Search algorithms for polymers are significantly less developed than those for small molecules because polymer search relies on searching by polymer name, which can be challenging because polymer naming is overly broad (i.e., polyethylene), complicated for complex chemical structures, and often does not correspond to official IUPAC conventions. Chemical structure search in polymers is limited to substructures, such as monomers, without awareness of connectivity or topology. This work introduces a novel query language and graph traversal search algorithm for polymers that provides the first search method able to fully capture all of the chemical structures present in polymers. The BigSMARTS query language, an extension of the small-molecule SMARTS language, allows users to write queries that localize monomer and functional group searches to different parts of the polymer, like the middle block of a triblock, the side chain of a graft, and the backbone of a repeat unit. The substructure search algorithm is based on the traversal of graph representations of the generating functions for the stochastic graphs of polymers. Operationally, the algorithm first identifies cycles representing the monomers and then the end groups and finally performs a depth-first search to match entire subgraphs. To validate the algorithm, hundreds of queries were searched against hundreds of target chemistries and topologies from the literature, with approximately 440,000 query–target pairs. This tool provides a detailed algorithm that can be implemented in search engines to provide search results with full matching of the monomer connectivity and polymer topology.

# Data Collection and Organization
- The query-target-dataset.xlsx spreadsheet contains a matrix of query and target polymer searches that validate the substructure search algorithm, not yet released.
- The tabs are classified by query topology, including single stochastic object (homopolymer, random copolymer, AA-BB copolymer), block, graft, star, and polymer network. 
- The queries in row 1 are written in BigSMARTS line notation, and the targets in column A are written in BigSMILES line notation. Every BigSMARTS is searched in all BigSMILES.
- Every BigSMARTS query tests a rule; for example, cyclic permutations, monomer splits, inversions, and frame shifts should not affect the number of matches.
- Every BigSMILES target is a real polymer from peer-reviewed scientific literature, with the source written.
- A 0 or a 1 is handwritten depending on whether a substructure match is expected between the query and target. The substructure search algorithm validates this.

# Test Cases

**Table 1.** Queries with increasing restriction on the target ensemble matched.

| BigSMARTS | Meaning| # BigSMILES Hits |
| :---- | :---: | :---: |
| CCO | ethanol SMARTS that searches an entire BigSMILES | 207 |
| {[]CCO[]} | ethanol SMARTS that localizes hits to the repeat units | 198 |
| {[][<]CCO[>][]} | PEG query with wildcard end groups that localizes hits to the repeat unit backbones | 68 |
| {[][<][CH2][CH2]O[>][]} | prevents matches to pendant groups not specified in the query | 57 |
| {[][<][CH2][CH2]O[>],!\*[]} | prevents matches to extra repeat units not specified in the query | 45 |
| {[][<][CH2][CH2]O[>],!\*\;!\*[]} | prevents matches to extra repeat units and end groups not specified in the query | 1 |

**Table 2.** Repeat unit mutations that do not affect the targets matched.

| BigSMARTS | Change | # BigSMILES Hits |
| :---- | :---: | :---:
| {[][<]CCO[>][]} | PEG backbone search | 68 |
| {[][>]CCO[<][]} | change in bonding descriptors | 68 |
| {[][<]COC[>][]} | frame shift | 68 |
| {[][<]OCC[>][]} | inversion | 68 |
| {[][<]C[<2],[>2]CO[>][]} | split | 68 |
| {[][<]CCO[>],[<]CCO[>][]} | duplication | 68 |

**Table 3.** Block copolymer query-target pairings.

| BigSMARTS | Change | # BigSMILES Hits |
| :---- | :---: | :---:
| {[][>]CC(c1ccccc1)[<][>]}?*{[>][<]CC(C(=O)O)[>][]} | polystyrene-*b*-polyacrylate block substructure with wildcard linker | 11 |
| {[][$]CC(c1ccccc1)[$][$]}{[$][$]CC(C(=O)O)[$][]} | no wildcard linker | 7 |
| {[][$]CC(C(=O)O)[$][$]}{[$][$]CC(c1ccccc1)[$][]} | flip the blocks | 7 |
| {[][<]CC(c1ccccc1)[>][<]}{[>][<]CC(C(=O)O)[>][]} | head-to-tail repeat units only | 7 |
| {[][<]CC(c1ccccc1)[>],[<]CC(c1ccccc1)[>2],[<2]CC(C(=O)O)[>2][]} | a single stochastic object, but still encodes a diblock! | 7 |
| {[][<]CC(c1ccccc1)[>];[<]CC(c1ccccc1){[>][<]CC(C(=O)O)[>][]}[]} | implicit/explicit end group representation| 7 |

**Table 4.** Polymer network query-target pairings.

| BigSMARTS | Change | # BigSMILES Hits |
| :---- | :---: | :---:
| {[][<]CCCCC(C)(C)C(=O)O{[>][<]CCO[>][<]}C(=O)C(C)(C)CCCC[<],[>]n1cc([<2])nn1,[>2]COCC(COC[>2])(COC[>2])C[]} | A2 + B3 polymer network | 2 |
| {[][<]CCCCC(C)(C)C(=O)O{[>][<]CCOCCO[>][<]}C(=O)C(C)(C)CCCC[<],[>]n1cc([<2])nn1,[>2]COCC(COC[>2])(COC[>2])C[]} | duplicated nested repeat unit | 2 |
| {[][<]CCCCC(C)(C)C(=O)O{[>][<]C[<3],[>3]CO[>][<]}C(=O)C(C)(C)CCCC[<],[>]n1cc([<2])nn1,[>2]COCC(COC[>2])(COC[>2])C[]} | nested repeat unit split | 2 |
| {[][>]CCCCC(C)(C)C(=O)O{[>][<]CCO[>][<]}C(=O)C(C)(C)CCCC[>],[<]n1cc([<5])nn1,[>5]COCC(COC[>5])(COC[>5])C[]} | change in bonding descriptors | 2 |

**Table 5.** Topological graph queries.

| BigSMARTS | Meaning | # BigSMILES Hits |
| :---- | :---: | :---:
| {[][]} | wildcard stochastic object, matches to all polymers | 489 |
| {[][]}!{[][]} | only one stochastic object, does not match to diblocks, triblocks, or stars | 382 |
| {[][]}?*{[][]} | diblock substructure, can match to triblocks and tetrablocks | 107 |
| {[][]}?*{[][]}!{[][]} | diblock substructure with no other blocks | 78 |
| {[][]}?\*{[][]}?\*{[][]} | triblock substructure, can match to tetrablocks and hexablocks | 15 |
| {[][]}?\*{[][]}?\*{[][]}!{[][]} | triblock substructure with no other blocks | 2 |
| {[][<]?\*{[>][<]?\*[>][<]}?\*[>][]} | segmented topology (nested object along the backbone) | 10 |
| {[][<]?\*(?\*{[>][<]?\*[>][]})?\*[>][]} | graft topology (nested object on the sidechain) | 11 |
| {[][]}?\*(?\*{[][]})?\*{[][]} | 3-arm star polymer substructure | 21 |

**Table 6.** Functonal groups along the backbone queries.

| BigSMARTS | Chemistry Class | # BigSMILES Hits |
| :---- | :---: | :---:
| {[][<]C(=O)O?*[>][]} | polyester | 75 |
| {[][<]OC(=O)O?*[>][]} | polycarbonate | 29 |
| {[][<]NC(=O)O?*[>][]} | polyurethane | 1 |
| {[][<]C=C?*[>][]} | polydiene | 31 |
| {[][<]NC(=O)N?*[>][]} | polyurea | 6 |

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
