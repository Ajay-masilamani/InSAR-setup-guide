Tools installing : Miniforge (conda), MintPy, asf_search, HyP3 SDK, SNAPHU, and optionally ISCE2.

MintPy's installation notes are tested on Linux and macOS, and are marked as experimental on Windows. Source: MintPy installation guide
Miniforge officially supports Linux and WSL. Source: Miniforge on GitHub

Before you start: you need Ubuntu installed on Windows through WSL. Source: Microsoft: Install WSL

Step 1: Update Ubuntu
```bash
sudo apt update
sudo apt install -y wget
```
The first line refreshes Ubuntu's list of software.
The second installs `wget`, a tool for downloading files.
Type your Ubuntu password when asked. It will not show while you type. This is normal.
---
Step 2: Download Miniforge (the Python manager)
```bash
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```
Miniforge installs `conda`, a program that downloads and installs scientific tools for you.
Official source: Miniforge on GitHub, section Install, Unix-like platforms (macOS, Linux, & WSL)
---
Step 3: Install Miniforge
```bash
bash Miniforge3-$(uname)-$(uname -m).sh
```
Answer the questions like this:
"Press ENTER to continue": press Enter
Licence text: keep pressing Enter (or press q) to reach the end
"Do you accept the license terms?": type yes
"Press ENTER to confirm the location": press Enter
"Do you wish to update your shell profile to automatically initialize conda?": type yes
Then close Ubuntu and open it again. The line should now start with `(base)`.
Official source: Miniforge on GitHub. The interactive install, which asks to initialize conda, is the recommended way.
---
Step 4: Create a separate environment called "insar"
```bash
conda create -n insar python=3.11
```
Type y when asked "Proceed?". Then switch into it:
```bash
conda activate insar
```
The line will now start with `(insar)`.
An environment is a separate box for your InSAR tools, so they do not disturb anything else.
MintPy's own installation guide also uses an environment named `insar`.
Official source: MintPy installation guide
> **Every time you open Ubuntu in future, type `conda activate insar` first.**
---
Step 5: Install MintPy (InSAR time-series analysis)
```bash
conda install -c conda-forge mintpy
```
Type y when asked. This can take several minutes.
MintPy reads interferogram stacks from ISCE, ARIA, FRInGE, HyP3, GMTSAR, SNAP, GAMMA and ROI_PAC, and produces ground displacement over time in the line-of-sight direction.
Official source: MintPy installation guide and MintPy documentation
---
Step 6: Install asf_search (search and download Sentinel-1 data)
```bash
conda install -c conda-forge asf_search
```
asf_search searches the Alaska Satellite Facility (ASF) data catalog and downloads data.
Official source: ASF: asf_search Basics
---
Step 7: Install HyP3 SDK (free cloud InSAR processing by ASF)
```bash
conda install -c conda-forge hyp3_sdk
```
HyP3 lets you submit InSAR processing jobs to ASF's servers for free and download the results.
Official source: ASF HyP3 SDK documentation
---
Step 8: Install SNAPHU (phase unwrapping)
```bash
conda install -c conda-forge snaphu
```
This conda package is a Python wrapper for SNAPHU, maintained by the ISCE framework team.
Official source: conda-forge: snaphu and snaphu-py on GitHub
---
Step 9 (optional): Install ISCE2
```bash
conda install -c conda-forge isce2
```
ISCE2 is a framework for processing SAR and InSAR data, including Sentinel-1.
This step is optional. If it shows a long error, skip it. Steps 5 to 8 are enough to start.
Official source: conda-forge: isce2 and ISCE2 on GitHub
---
Step 10: Check that everything works
```bash
python -c "import mintpy, asf_search, hyp3_sdk, snaphu; print('All OK')"
```
If you see All OK, the installation worked. Then:
```bash
smallbaselineApp.py -h
```
This should print MintPy's help text.
Official source: MintPy documentation
---

Official sources used
Tool	What it does	Official page
WSL	Runs Ubuntu inside Windows	https://learn.microsoft.com/en-us/windows/wsl/install
Miniforge	Installs conda (Python manager)	https://github.com/conda-forge/miniforge
MintPy	InSAR time-series analysis	https://mintpy.readthedocs.io/
asf_search	Search and download SAR data	https://docs.asf.alaska.edu/asf_search/basics/
HyP3 SDK	Free cloud InSAR processing	https://hyp3-docs.asf.alaska.edu/using/sdk/
SNAPHU	Phase unwrapping	https://anaconda.org/conda-forge/snaphu
ISCE2	InSAR processing (optional)	https://github.com/isce-framework/isce2
