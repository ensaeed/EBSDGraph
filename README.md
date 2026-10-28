BSDGraph Crystallographically constrained graph reduction of electron backscatter diffraction (EBSD) data

EBSDGraph is a Python research workflow for constructing spatial graphs from indexed EBSD measurements and reducing them under crystallographic constraints. It includes quantitative evaluation of orientation reconstruction fidelity and selected structural properties.
EBSDGraph does not replace conventional EBSD analysis or grain reconstruction, and no downstream graph neural network model is evaluated in this study.

Features
- Import EBSD measurements from Channel Text Files (.ctf).
- Construct undirected four-neighbour graphs from valid indexed measurements.
- Preserve crystallographic and available measurement-quality attributes.
- Reduce graphs within 5 × 5 and 10 × 10 spatial blocks, enforcing phase purity, spatial connectivity and a maximum pairwise symmetry-aware misorientation of 15°.
- Represent reduced components using observed orientation medoids, not arithmetic Euler-angle averages.
- Validate orientation reconstruction error and, where evaluated, graph connectivity and high-angle boundary retention.
Public datasets
Original data: Davis, Hönnige and Martina (2022), Zenodo record 5822710.
Label	Original file
Dataset A	Figure_10_EBSD.ctf
Dataset B	Figure_6b_EBSD.ctf


Both files originate from the same research collection on Ti-6Al-4V. Download them from Zenodo; this repository does not redistribute the original files.
Running the notebook
1. Clone or download this repository.
2. Download both .ctf files from the Zenodo record.
3. Open the uploaded EBSDGraph .ipynb notebook in Google Colab or a compatible Jupyter environment.
4. Install the packages required by the notebook. Known dependencies include Python, NumPy, pandas and orix; the complete package list and tested versions still need to be verified from the notebook.
5. Change input/output paths to your own files. Replace any private Google Drive paths before running.
6. Run the notebook's preprocessing, graph construction, reduction and validation stages in their intended order.
Large EBSD datasets may require significant memory and execution time. A clean-environment rerun has not yet been confirmed, so this repository should not yet be described as independently reproducible.
Method summary
1. Retain valid indexed measurements and their spatial coordinates.
2. Build an undirected graph using four-neighbour spatial adjacency.
3. Partition measurements into spatially bounded, phase-pure, connected components subject to the 15° maximum pairwise symmetry-aware misorientation constraint.
4. Choose observed medoid orientations for reduced nodes.
5. Contract the graph while retaining adjacency between different reduced components.
6. Evaluate crystallographic reconstruction and selected structural preservation metrics.
The study includes two-stage and greedy reduction procedures. For Dataset B, the 10 × 10 greedy configuration received the reported independent crystallographic validation; the controlled two-stage 10 × 10 comparison was not independently validated to the same extent.
Reported validation results
These are manuscript results, not a claim that a fresh checkout of the repository has been rerun.
Configuration	Original indexed nodes	Reduced nodes	Node reduction	Mean orientation error
Dataset A, 5 × 5, two-stage	1,503,311	115,006	92.35%	1.0903°
Dataset A, 10 × 10, two-stage	1,503,311	43,184	97.13%	1.2593°
Dataset B, 5 × 5, two-stage	2,480,095	178,389	92.81%	0.7399°
Dataset B, 10 × 10, greedy	2,480,095	78,510	96.83%	1.0844°


For Dataset A, the original graph contained 2,479,075 undirected edges and 4,081 connected components. The 10 × 10 reduced graph contained 68,695 edges and retained 4,081 connected components. All 37,870 original high-angle boundary adjacencies remained structurally represented between distinct reduced nodes, while medoid-based high-angle boundary sensitivity exceeded 98.9% at both reduction scales. Structural retention does not mean exact preservation of boundary geometry or all misorientation values.
Limitations
- Both evaluated 2D datasets originate from one research collection.
- Omitting non-indexed measurements can affect graph connectivity.
- Graph reduction loses some local detail, quantified in part by reconstruction errors.
- Runtime, memory and data-access improvements over conventional EBSD arrays have not been demonstrated.
- Three-dimensional scalability and downstream machine-learning performance remain untested.
Citation
If using the source EBSD data, cite:

Davis, A. E., Hönnige, J. R., & Martina, F. (2022). Dataset for “Quantification of strain fields and grain refinement in Ti-6Al-4V inter-pass rolled wire-arc AM by EBSD misorientation analysis”. Zenodo. https://doi.org/10.5281/zenodo.5822710

