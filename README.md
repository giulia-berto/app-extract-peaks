<h1 align="center">Peaks extraction with MRtrix</h1>

<p align="center">
  Computes fibre orientation distributions from DWI with MRtrix3 constrained spherical deconvolution (CSD, multi-shell or 5TT) and extracts the peaks with sh2peaks, using TractSeg's code.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.172"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.172-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Computes fibre orientation distributions from DWI with MRtrix3 constrained spherical deconvolution (CSD, multi-shell or 5TT) and extracts the peaks with sh2peaks, using TractSeg's code.**

Uses TractSeg's MRtrix wrapper to estimate the response function and FODs with the selected CSD type, then extracts the FOD peaks at each voxel with sh2peaks; the peaks image is the input expected by TractSeg. A brain mask is computed from the T1w with FSL bet when none is given. The T1w must be skull-stripped and aligned with the DWI; multi-shell DWI is needed for the msmt options.

| | |
|---|---|
| **Inputs** | `neuro/dwi` · `neuro/anat/t1w` · `neuro/mask` (optional) |
| **Outputs** | `neuro/peaks` |
| **Container** | `giuliaberto/extract-peaks:1.1` |
| **Resources** | 16 CPUs · 10 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.172](https://doi.org/10.25663/brainlife.app.172) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `0` | `neuro/dwi` | yes | Dwi raw data |
| `1` | `neuro/anat/t1w` | yes | T1w image. It should be aligned with the dwi data and all non-brain tissue should be removed. |
| `2` | `neuro/mask` | no | Brain mask. It should be aligned with the dwi data. If not provided, the BET algorithm will be used for brain extraction. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/peaks` | CSD peaks |

<details>
<summary><b>Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `csd` | enum |  | CSD type Options: `csd_msmt_5tt`, `csd_msmt`, `csd`. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.172](https://doi.org/10.25663/brainlife.app.172), choose `neuro/dwi`, `neuro/anat/t1w`, `neuro/mask` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/peaks`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `giuliaberto/extract-peaks:1.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "dwi": "/path/to/0/dwi",
       "bvecs": "/path/to/0/bvecs",
       "bvals": "/path/to/0/bvals",
       "t1": "/path/to/1/t1",
       "mask": "/path/to/2/mask",
       "csd": ""
   }
   ```

3. Run `./main`.

## On [Brainlife.io](http://brainlife.io/)

You can submit this App online at https://doi.org/10.25663/brainlife.app.172 via the “Execute” tab.

Inputs: \
Mandatory inputs are (i) the dwi data (multi-shell and not nomalized) and (ii) the T1 anatomical image. Optionally, you can provide also the brain mask (if not provided, it will be computed using the BET command from FSL).

Output: \
The CSD peaks.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Peaks extraction with MRtrix. brainlife.io App. [doi:10.25663/brainlife.app.172](https://doi.org/10.25663/brainlife.app.172)
- Tournier J-D, Calamante F, Connelly A. MRtrix: Diffusion tractography in crossing fiber regions. Int J Imaging Syst Technol 22:53-66 (2012). [doi:10.1002/ima.22005](https://doi.org/10.1002/ima.22005)
- Wasserthal J, Neher P, Maier-Hein KH. TractSeg - Fast and accurate white matter tract segmentation. NeuroImage (2018). [doi:10.1016/j.neuroimage.2018.07.070](https://doi.org/10.1016/j.neuroimage.2018.07.070)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Tournier et al. MRtrix3: A fast, flexible and open software framework for medical image processing and visualisation. *NeuroImage* 202:116137 (2019). [doi:10.1016/j.neuroimage.2019.116137](https://doi.org/10.1016/j.neuroimage.2019.116137)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Giulia Bertò

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
