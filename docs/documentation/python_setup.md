---
Title: Python Setup
---

# Python & Environment Setup Guide

This page covers the basics of Python as a programming language for astrophysics while comparing the two programming environments which are **Google Colab** and **Anaconda** and guides you for light curve analysis.

---

## What is Python?

[Python](https://python.org) is a high-level, interpreted, general-purpose programming language known for its easily readable syntax and extensive scientific ecosystem. 

In astronomical research and data science, Python serves as the standard for:
* **Data Analysis:** Processing sequential photometric data from space missions.
* **Data Visualization:** Generating good quality plots of spectra, light curves, and images.
* **Task Automation:** Scripting complex data reduction pipelines.
* **Open Source Scientific Computing:** Accessing thousands of libraries.

---

## Python in Astrophysics

Python's strength in astronomy comes from its library stack:

| Package | Purpose in Astronomy |
| :--- | :--- |
| **NumPy** | Fundamental package for numerical computing, arrays, and matrix math. |
| **pandas** | Data manipulation and tabular data structuring. |
| **Matplotlib** | Core plotting library for creating 2D graphs and visual figures. |
| **Astropy** | Core astronomy library providing tools for coordinate transformations, FITS file I/O, and celestial calculations. |
| **Lightkurve** | Specialized package built on top of Astropy and Matplotlib specifically for analyzing time-series pixel and light curve data from NASA's Kepler, K2, and TESS missions. |

---

## Execution Environments: Google Colab vs. Anaconda

To run Python code, you need an execution environment. The two most common options for data science are **Google Colab** (cloud-based) and **Anaconda** (local desktop installation).

### Comparison Overview

| Feature | Google Colab | Anaconda (Local Setup) |
| :--- | :--- | :--- |
| **Installation** | Runs in browser | Requires downloading |
| **Execution** | Cloud server | Local machine |
| **Internet Dependency** | Required | Optional (can run offline) |
| **Pre-installed Packages** | Includes NumPy, pandas, Matplotlib, TensorFlow | Includes core packages from which extra packages are installed via Conda or Pip |
| **File Storage** | Google Drive | Local file system |

---

## Google Colab (Recommended)

[Google Colab](https://colab.research.google.com) is a free Jupyter Notebook environment hosted in the cloud and it allows you to write and execute Python code through your web browser.

### Key Features
* **No Setup:** Connects directly via any web browser using a Google Account.
* **Automated Cloud Backup:** All notebooks (`.ipynb` files) save automatically to your Google Drive.
* **Interactive Cells:** Code and text (AKA Markdown) are broken into modular cells for step-by-step execution.

### Getting Started on Google Colab
1. Go to [colab.research.google.com](https://colab.research.google.com).
2. Sign in with your Google Account.
3. Click **New Notebook** (or select **Upload** to load an existing `.ipynb` file).
4. Create code cells and run commands directly in the cloud.

---

## Anaconda (For Local Development)

[Anaconda](https://www.anaconda.com) is a free, open-source distribution of Python made for scientific computing and data science. It includes the Python interpreter, package managers (`conda` and `pip`), and interfaces like **Jupyter Notebook** and **VS Code**.

### Key Features
* **Offline Access:** Process data locally without internet connection.
* **Conda Environment Manager:** Isolate project dependencies into virtual environments to prevent library conflicts.
* **Unrestricted File Access:** Directly access, process, and save large local datasets on your computer.

### Installing Anaconda & Preparing Local Setup
1. Download the installer from the [Anaconda Distribution Page](https://www.anaconda.com/download).
2. Run the installer.
3. Open **Anaconda Navigator** (or launch your system terminal / Anaconda Prompt).
4. Launch **Jupyter Notebook** or **JupyterLab** to begin working.

---

## Workspace Preparation Code

Whether you choose Google Colab or Anaconda, your environment must have the necessary packages installed before starting analysis of lightcurves.

### Installation & Initialization Script

Below is the complete setup script to verify your workspace and load essential libraries:

```python
# 1. Install Lightkurve (Run in terminal/command prompt, or directly in Colab with !)
# For terminal: pip install lightkurve
# For Google Colab: !pip install lightkurve

# 2. Import core libraries
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
import lightkurve as lk

