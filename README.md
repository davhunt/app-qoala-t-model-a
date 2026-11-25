<h1 align="center">Qoala-T Model A</h1>

<p align="center">
  Rates the quality of FreeSurfer segmentations with the Qoala-T supervised model (BrainTime model A) and outputs a PDF rating figure and per-subject predictions.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.386"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.386-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Rates the quality of FreeSurfer segmentations with the Qoala-T supervised model (BrainTime model A) and outputs a PDF rating figure and per-subject predictions.**

Collects aseg and aparc statistics from one or more FreeSurfer subject directories into a table (Stats2Table.R), then applies the pre-trained Qoala-T random-forest model to give each subject a quality score and flag scans that should be excluded or checked manually. Use it for quality control of FreeSurfer output in larger datasets. It needs FreeSurfer stats files (aseg.stats, aparc stats) for each subject.

| | |
|---|---|
| **Inputs** | `neuro/freesurfer` |
| **Outputs** | `report/pdf` |
| **Container** | `davhunt/r-qoala:1.0.1` |
| **Resources** | 1 CPUs · 30 GB memory · 0.17 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.386](https://doi.org/10.25663/brainlife.app.386) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `fs` | `neuro/freesurfer` | yes | FreeSurfer subject directories (one or more) whose segmentations are rated. Each directory needs stats/aseg.stats and lh/rh aparc stats. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `Output_Qoala_T` | `report/pdf` | Qoala-T rating figure (PDF) plus the stats table and Qoala-T prediction CSV. |

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.386](https://doi.org/10.25663/brainlife.app.386), choose `neuro/freesurfer` from your project and press **Execute**. The results are saved to your project as `report/pdf`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `davhunt/r-qoala:1.0.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "output": "/path/to/fs/output"
   }
   ```

3. Run `./main`.

## Sample Datasets

If you don't have your own input file, you can download sample Freesurfer from Brainlife.io, or you can use [Brainlife CLI](https://github.com/brainlife/cli).

```
npm install -g brainlife
bl login
mkdir input
bl dataset download 5a065cc75ab38300be518f51 && mv 5a065cc75ab38300be518f51 input/output1
bl dataset download 5a0662225ab38300be518f53 && mv 5a0662225ab38300be518f53 input/output2
bl dataset download 5a065f995ab38300be518f52 && mv 5a065f995ab38300be518f52 input/output3
bl dataset download 5a06a8d05ab38300be518f54 && mv 5a06a8d05ab38300be518f54 input/output4
```

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Qoala-T Model A. brainlife.io App. [doi:10.25663/brainlife.app.386](https://doi.org/10.25663/brainlife.app.386)
- Klapwijk ET, van de Kamp F, van der Meulen M, Peters S, Wierenga LM. Qoala-T: A supervised-learning tool for quality control of FreeSurfer segmented MRI data. NeuroImage 189:116-129 (2019). [doi:10.1016/j.neuroimage.2019.01.014](https://doi.org/10.1016/j.neuroimage.2019.01.014)
- Klapwijk, E. T., Van De Kamp, F., Van Der Meulen, M., Peters, S., & Wierenga, L. M. (2019). Qoala-T: A supervised-learning tool for quality control of FreeSurfer segmented MRI data. Neuroimage, 189, 116-129. [https://www.sciencedirect.com/science/article/pii/S1053811919300138](https://www.sciencedirect.com/science/article/pii/S1053811919300138)
- Fischl. FreeSurfer. *NeuroImage* 62:774-781 (2012). [doi:10.1016/j.neuroimage.2012.01.021](https://doi.org/10.1016/j.neuroimage.2012.01.021)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- David Hunt

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>
