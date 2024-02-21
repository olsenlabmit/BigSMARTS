# BigSMARTS: A Topologically Aware Query Language and Substructure Search Algorithm for Polymer Chemical Structures

# Article
https://pubs.acs.org/doi/10.1021/acs.jcim.3c00978

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
