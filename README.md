# 2024-Antibodies-and-AI

## Team Roster: AI/ML
|Role|Contributor|Affiliation|
|----------|----------|----------|
|Team Lead|Todd Smith|Digital World Biology, LLC|
|Developer|Timothy Brugarolas|Pasadena City College|
|Developer, Co-Writer|Wengang Zhang|National Cancer Institute|
|Developer|Vee Xu|Gladstone Institutes|

<br>

## Team Roster: Immune Profiling & Gene Expression
|Role|Contributor|Affiliation|
|----------|----------|----------|
|Team Lead|Eric Olson|Chinook Therapeutics|
|Developer, Writer|Benjamin Bekey|Pasadena City College|
|Developer, Co-Writer|Samhita Gopalan|University of Washington|
|Developer|Jack Lin|Unaffiliated|

<br>

## Motivation and Background
In our immune system, antibodies play an important role in identifying and neutralizing foreign invaders such as pollen, viruses, and bacteria. These Y-shaped proteins are produced by B-cells, also known as immunoglobins (Igs). The tips of the Y-shaped structure form the "variable region" or complementarity-determining regions (CDRs), which is highly specific to a particular antigen (the foreign substance). The rest of the structure, known as the "constant region," determines the antibody's class (IgG, IgA, IgM, etc.). The variable regions (CDRs) of an antibody have unique sequences and structures that bind to specific epitopes (the part of an antigen recognized by the immune system). This binding is highly specific, akin to a lock and key mechanism. Once an antibody binds to an antigen, it can neutralize the threat directly (e.g., by blocking a virus from entering cells) or mark it for destruction by other immune cells. Beyond their role in the immune system, antibodies are widely used in research, diagnostics, and therapy. Monoclonal antibodies, for instance, are engineered to target specific proteins in diseases like cancer or autoimmune disorders. 

However, developing antibodies that can effectively target new or evolving pathogens is a complex and time-consuming process. Traditionally, developing effective antibodies is a labor-intensive process and often need to screen thousands of potential antibodies to find ones that effectively bind to and neutralize a target pathogen. By leveraging AI and Machine Learning, we aim to accelerate the discovery and optimization of antibodies. 

The goal of this year's hackathon was to build off past hackathons and refine past code, give example analysis, annotate reference notebooks, and start on developing glossaries / tutorials for undergraduate research use. A second subteam focused on immunoprofiling and gene expression characterization to test potential data science applications for identifying effective T-cell clones for targeted biomarkers. Both teams used Jupyter Notebooks hosted on Jupyter Hub, all which was hosted using Jetstream2 virtual instances. Publically available immunology datasets were used for both projects. 

## Methods
### Datasets
#### AI & Machine Learning
CoV-AbDab database, .csv format. [CoV-AbDab](https://opig.stats.ox.ac.uk/webapps/covabdab/) is a public database documenting all published/patented antibodies and nanobodies able to bind to coronaviruses, including SARS-CoV2, SARS-CoV1, and MERS-CoV. Entries were highly annotated and indicated neutralizing ability, receptor type (antibody, nanobody), data pairing information (heavy and light chains, just heavy, etc.), epitope-binding information, structure information, and virus reactivity among others. Datasets still required time-intensive data processing, however, as they were not in a format conducive to our workflow. The data had ambiguity, potential errors, and non-standardized data entry that needed to be reformatted.
* **Dataset:** CoV-AbDab_240208 (~13,000 Ab seq)
#### Gene Expression & Immuneprofiling
Publically available gene expression data in .csv, .txt format from [NCBI](https://www.ncbi.nlm.nih.gov):
* **GEO accession:** GSE123813
* **BioProject:** PRJNA509910
* **SRA:** SRP173389
### Software
#### AI & Machine Learning
* [RFdiffusion](https://github.com/RosettaCommons/RFdiffusion), an open-source structure generator
* [ProteinMPNN](https://github.com/dauparas/ProteinMPNN?tab=readme-ov-file), a deep learning protein sequence generator
#### Gene Expression & Immuneprofiling
* Python libraries: Pandas (for data manipulation and tabular work), Scanpy (for scRNA processing and cluster plotting), and Anndata (for annotations on top of Scanpy work).
* IDE: R Studio initially, switch to Jupyter Hub ([see Approach](#gene_approach)).

## Approach
### AI & Machine Learning
#### Workflow Chart for AI-Driven Antibody Design: Enhancing CoV-AbDab with Diffusion Models and Machine Learning

```mermaid
graph TD
    A[Start] --> B[Input: CoV-AbDab Dataset]
    B --> C[Module 1: ML Modeling]
    B --> F[Module 2: Sequence Diversification]
    
    C --> D[Pre-trained Ablang2 Model]
    D --> E{Predict: Neutralizing or Non-neutralizing}
    
    F --> G[Select Neutralizing Antibody]
    G --> H[RFDiffusion: Partial Diffusion: Diversify Structure]
    H --> I[ProteinMPNN: Generate Sequences]
    
    I --> E
    E -->|Neutralizing| M[Candidate for Screening]
    E -->|Non-neutralizing| N[Discard]
    M --> O[Output: Neutralizing Antibody Candidates]
    O --> P[End]

    classDef module fill:#f9f,stroke:#333,stroke-width:2px;
    class C,F module;
```
The AI & ML team built off past hackathon work and focused on further filtration and utilizing new [technology repositories]. Two goals were introduced: to see what data the AI trains on best and to see what data makes sense to include versus exclude. They decided upon including data of human origin with the RBD epitope and excluding data that did not have heavy and light chain pairs. Past code was cleaned, and annotations were added to provide educational clarity for future undergraduate researchers using this resource.

In Module 2, another task was implemented - designing an antibody using a diffusion model. The goal of Module 2 was to introduce sequence diversity to the paratope (antigen-binding site on antibody) to optimize the binding affinity between antibody and antigen. The first step was selecting neutralizing antibodies from CovDaB and downloading the corresponding crystal structure from the Protein Data Bank. Then the specified CDR3 region underwent Partial Diffusion to select for similar antibodies that could also improvie binding affinity via spike protein binding. RFdiffusion was used for this but the team discovered that it could only generate protein structure, but not protein sequence. ProteinMPNN was then used to generate protein sequences using the partially diffused structures made in the prior step. 

The protein sequences generated from Partial Diffusion and Sequence Generation were then fed into the cleaned-and-annotated Hackathon script to screen for neutralizing antibodies. All non-neutralizing antibodies were discarded. After the neutralizing antibodies were selected for, AlphaFold was used to predict and visualize structures using the ProteinMPNN-generated sequences as input. The resulting structures were compared to the crystal structures from the Protein Data Bank to assess accuracy. 

Work will build on:
- [A Gentle Introduction to ML/AI as Applied to Antibody Engineering](https://github.com/NCBI-Codeathons/mlxai-2024-team-smith)
- [2023 Immune-profiling](https://github.com/AntibodyEngineers/2023-immune-profiling)
- [2022 COVID-not-COVID](https://github.com/AntibodyEngineers/2022-covid-not-covid)

For getting started with Jetstream see: [getting started](/getting-started.md)  
For adventures after getting started see: [caveats](/caveats.md)  

<a name="gene_approach"></a>
### Gene Expression & Immunoprofiling
```mermaid
  journey
    title Hackathon 2024 Work Log
    section August 5, 2024
      Scanpy Tutorial: 1: Jack
      TCR Dataset Processing: 1: Ben
      Patient Dataset Processing: 1: Samhita
    section August 6, 2024
      Documentation: 3: Ben
    section August 7, 2024
      Clone ID (TCR): 3: Ben
      scRNA Pre-processing: 3: Jack
    section August 8, 2024
      Presentations: 5: Jack, Ben, Samhita
      Documentation: 5: Samhita
```
As an alternative to Seurat (R package), the team used Scanpy and Anndata to process single cell RNA sequencing data in Python via Jupyter Notebooks. This was a calculated decision based off the team's general inexperience with R Studio and the amount of prep work that was needed to: 1) use Scanpy/pre-process scRNA 2) familiarize themselves with tabular data processing 3) understand the current science behind biomarker identification in cancer research. 

## Projects
```mermaid
block-beta
    columns 2
    A["Immune Profling & Gene Expression"]  B["ML-base Receptor Classification"]
 
```
## Results & Future Work
### AI & ML
* N/A
### Gene Expression & Immunoprofiling
The Gene Expression team used Pandas, Numpy, and Scanpy to isolate and select for desired data in the given TCR text file. Further extracting resulted in usable table data in the form of viable Post-treatment clones and CD8+ positive response counts. 
  
## Citations
Hackathons are funded by the National Science Foundation DUE 2055036.

Work utalized the Jetstream2 resource:  
David Y. Hancock, Jeremy Fischer, John Michael Lowe, Winona Snapp-Childs, Marlon Pierce, Suresh Marru, J. Eric Coulter, Matthew Vaughn, Brian Beck, Nirav Merchant, Edwin Skidmore, and Gwen Jacobs. 2021. “Jetstream2: Accelerating cloud computing via Jetstream.” In Practice and Experience in Advanced Research Computing (PEARC ’21). Association for Computing Machinery, New York, NY, USA, Article 11, 1–8. DOI: https://doi.org/10.1145/3437359.3465565

Timothy J. Boerner, Stephen Deems, Thomas R. Furlani, Shelley L. Knuth, and John Towns. 2023. ACCESS: Advancing Innovation: NSF’s Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support. “In Practice and Experience in Advanced Research Computing (PEARC ’23)”, July 23–27, 2023, Portland, OR, USA. ACM, New York, NY, USA, 4 pages. https://doi.org/10.1145/3569951.3597559

This work used Jetstream2 at Indiana University through allocation BIO220105 from the Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) program, which is supported by National Science Foundation grants #2138259, #2138286, #2138307, #2137603, and #2138296
