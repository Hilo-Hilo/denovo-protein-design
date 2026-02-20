# De Novo Protein Binder Design & Validation Pipeline

This repository contains a two-step computational pipeline for the *de novo* design of novel protein binders and their structural validation. The pipeline leverages deep learning-based generative models for design, and classical physics-based docking for validation.

## Overview

The workflow is split into two primary components:

1. **RFdiffusion Protein Design (`01_RFdiffusion_Protein_Design.ipynb`)**
2. **AutoDock Vina Validation (`02_AutoDock_Vina_Validation.ipynb`)**

---

### 1. RFdiffusion Protein Design

This notebook uses **RFdiffusion** (a diffusion model developed by the Baker Lab) for structure generation. It is specifically tailored for generating novel protein structures conditioned on a target active site motif.

**Key Features:**
- **Conditioned Generation:** Upload a full protein structure and a target active site. The model diffuses novel protein binders/scaffolds around the required catalytic residues.
- **Symmetry & Contig Support:** Supports partial diffusion, fixed contigs, and symmetric generation (cyclic/dihedral via AnAnaS).
- **Sequence Design & Scoring:** Integrates ProteinMPNN for inverse folding (sequence generation) and AlphaFold2 for rapid structure prediction and validation (pLDDT scores).
- **Automated Filtering:** Filters candidates based on minimum pLDDT, active site preservation, and full protein similarity metrics.

### 2. AutoDock Vina Validation

Once novel binder candidates are generated, this notebook performs rigorous structural and binding affinity validation.

**Key Features:**
- **Structural Alignment (PyMOL/TM-align):** Aligns generated designs with the original wild-type protein to verify that essential catalytic/binding residues (e.g., positions 70, 73, 130, 132, 166, 234, 237) are accurately preserved in 3D space.
- **Molecular Docking (AutoDock Vina):** Prepares the novel protein structures and target ligands (SDF files) for docking. Runs Vina to calculate binding affinities, validating that the active site is still functionally viable and capable of binding the target substrate.

## Usage

Both notebooks are optimized to run in Google Colab or on a local machine with GPU support. 

1. **Design:** Open `01_RFdiffusion_Protein_Design.ipynb`. Upload your target PDB and motif constraints. Configure the scoring metrics and run the diffusion process to generate candidate backbones.
2. **Validation:** Take the successfully generated PDBs from step 1 and open `02_AutoDock_Vina_Validation.ipynb`. Upload the candidate PDBs and your target ligand (SDF). The notebook will automatically align the residues and run AutoDock Vina to score the affinity.

## Acknowledgements

- [RFdiffusion (Baker Lab)](https://github.com/RosettaCommons/RFdiffusion)
- [ProteinMPNN](https://github.com/dauparas/ProteinMPNN)
- [AutoDock Vina](https://vina.scripps.edu/)
- Developed as part of the iGEM computational track.
