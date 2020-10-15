[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/brain-life/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.386-blue.svg)](https://doi.org/10.25663/brainlife.app.386)

# Qoala-T

This app uses a supervised learning model trained on 784 Freesurfer subjects, to rate the quality of novel subjects' Freesurfer segmentations with a "Qoala-T" score, as described [here](https://www.sciencedirect.com/science/article/pii/S1053811919300138) and in the [Github repo](https://github.com/Qoala-T/QC#a-predicting-scan-qoala-t-score-by-using-braintime-model).

Given a set of subjects processed with Freesurfer, Qoala-T gives each subject's segmentations a rating and indicates whether the data should be excluded and/or given manual QC. The tool is ideal then for large datasets where manual QC may be infeasible, and for developmental subjects who may have lower quality scans.

Sample output:
![example_output](example_out.pdf)

### Contributors
- [David Hunt](davhunt@iu.edu)

### Funding Acknowledgement
brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your publications and code reusing this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

### Citations
We kindly ask that you cite the following articles when publishing papers and code using this code. 

1. Klapwijk, E. T., Van De Kamp, F., Van Der Meulen, M., Peters, S., & Wierenga, L. M. (2019). Qoala-T: A supervised-learning tool for quality control of FreeSurfer segmented MRI data. Neuroimage, 189, 116-129. [https://www.sciencedirect.com/science/article/pii/S1053811919300138](https://www.sciencedirect.com/science/article/pii/S1053811919300138)


## Running the App 

### On Brainlife.io

You can submit this App online at [https://doi.org/10.25663/bl.app.386](https://doi.org/10.25663/bl.app.386) via the "Execute" tab.

### Running Locally (on your machine)

1. git clone this repo.
2. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.

```json
{
    "output": [
        "/N/slate/davhunt/workflows/5f878693c7adcb0c7b13a8fb/5f8786a5c7adcba72f13a8ff/5967bffa9b45c212bbec8958/output",
        "/N/slate/davhunt/workflows/5f878693c7adcb0c7b13a8fb/5f8786a5c7adcba72f13a8ff/598a28ec19ee5b6f80cba0b9/output",
        "/N/slate/davhunt/workflows/5f878693c7adcb0c7b13a8fb/5f8786a5c7adcba72f13a8ff/598a2aa44258600aa3128fd1/output"
    ]
}
```

3. Launch the App by executing `main`

```bash
./main
```

### Sample Datasets

If you don't have your own input file, you can download sample Freesurfer from Brainlife.io, or you can use [Brainlife CLI](https://github.com/brain-life/cli).

```
npm install -g brainlife
bl login
mkdir input
bl dataset download 5a065cc75ab38300be518f51 && mv 5a065cc75ab38300be518f51 input/output1
bl dataset download 5a0662225ab38300be518f53 && mv 5a0662225ab38300be518f53 input/output2
bl dataset download 5a065f995ab38300be518f52 && mv 5a065f995ab38300be518f52 input/output3
bl dataset download 5a06a8d05ab38300be518f54 && mv 5a06a8d05ab38300be518f54 input/output4
```

## Output

All output files will be generated under the current working directory (pwd). The main output of this App is a file called `output.mat`. This file contains following object.

Output files are written to "Output_Qoala_T". The main outputs are "Qoala_T_predictions_model_based_Dataset_Name.csv" which contains the model's recommendation on whether to include or exclude the data and whether manual QC is advised, and a pdf that provides a visualization of this information.

```
    ├── Output_Qoala_T
    │   ├── Figure_Rating_model_based_Dataset_Name.pdf
    │   ├── Freesurfer_Output_Dataset_Name.csv			# contains volume, area and thickness data from each FS subject that the model uses
    │   ├── Qoala_T_predictions_model_based_Dataset_Name.csv
```

### Dependencies

This App only requires [singularity](https://www.sylabs.io/singularity/) to run.

#### MIT Copyright (c) 2020 brainlife.io The University of Texas at Austin and Indiana University
