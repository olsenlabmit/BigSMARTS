# BigSMARTS: A Topologically Aware Query Language and Substructure Search Algorithm for Polymer Chemical Structures

# Journal Article
https://pubs.acs.org/doi/10.1021/acs.jcim.3c00978

# Description
Molecular search is important in chemistry, biology, and informatics for identifying molecular structures within large data sets, improving knowledge discovery and innovation, and making chemical data FAIR (findable, accessible, interoperable, reusable). Search algorithms for polymers are significantly less developed than those for small molecules because polymer search relies on searching by polymer name, which can be challenging because polymer naming is overly broad (i.e., polyethylene), complicated for complex chemical structures, and often does not correspond to official IUPAC conventions. Chemical structure search in polymers is limited to substructures, such as monomers, without awareness of connectivity or topology. This work introduces a novel query language and graph traversal search algorithm for polymers that provides the first search method able to fully capture all of the chemical structures present in polymers. The BigSMARTS query language, an extension of the small-molecule SMARTS language, allows users to write queries that localize monomer and functional group searches to different parts of the polymer, like the middle block of a triblock, the side chain of a graft, and the backbone of a repeat unit. The substructure search algorithm is based on the traversal of graph representations of the generating functions for the stochastic graphs of polymers. Operationally, the algorithm first identifies cycles representing the monomers and then the end groups and finally performs a depth-first search to match entire subgraphs. To validate the algorithm, hundreds of queries were searched against hundreds of target chemistries and topologies from the literature, with approximately 440,000 query–target pairs. This tool provides a detailed algorithm that can be implemented in search engines to provide search results with full matching of the monomer connectivity and polymer topology.

# Organization
- The validation spreadsheet contains a matrix of query and target polymer searches that validate the substructure search algorithm, not yet released.
- The tabs are classified by query topology, including single stochastic object (homopolymer, random copolymer, AA-BB copolymer), block, graft, star, and polymer network. 
- The queries in row 1 are written in BigSMARTS line notation, and the targets in column A are written in BigSMILES line notation. Every BigSMARTS is searched in all BigSMILES.
- A 0 or a 1 is handwritten depending on whether a substructure match is expected between the query and target. 
- The queries become more restricted moving from left to right. 
	- CCO is a SMARTS that searches an entire BigSMILES
	- {[]CCO[]} localizes hits to the repeat units
	- {[][<]CCO[>][]} localizes hits to the target repeat unit backbones
	- {[][<]COC[>][]} is a frameshifted polymer that would match the same cases as the above query
	- {[][<][CH2][CH2]O[>][]} prevents matches to pendant groups not specified in the query
	- {[][<][CH2][CH2]O[>],!*[]} prevents matches to extra repeat units not specified in the query
	- {[][<][CH2][CH2]O[>],!*;!*[]} prevents matches to extra repeat units and end groups not specified in the query

# Data Collection Methodology
Every BigSMILES target is a real polymer from peer-reviewed scientific literature, with the source written.

# Repository Location
http://doi.org/10.5281/zenodo.4780309

# Creators
- Nathan J. Rebello (https://orcid.org/0000-0002-0178-7701)
- Tzyy-Shyang Lin (https://orcid.org/0000-0002-8265-6702)
- Heeba Nazeer (hn1@wellesley.edu)
- Bradley D. Olsen (https://orcid.org/0000-0002-7272-7140)

# Rights
The dataset is released under CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/) in Zenodo (http://doi.org/10.5281/zenodo.4780309).
