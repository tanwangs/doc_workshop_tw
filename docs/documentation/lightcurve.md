---
title: Lightcurve Analysis
---

<!-- ============================================================
     📝 BLANK DOCUMENTATION TEMPLATE
     
     HOW TO USE:
     1. Copy this file and rename it (e.g., "my-topic.md")
     2. Replace the placeholder content below
     3. Add your new file to mkdocs.yml under the Documentation nav
     4. Run `mkdocs serve` to preview
     ============================================================ -->

# Light Curve Analysis

> **Date:** 2026-08-02  
> **Author:** Tandin Wangyel 
> **Tags:** `Python`, `Astrophysics`, `Light Curve`

---

# Stellar Light Curve Analysis Guide

This page is a complete reference for querying, downloading, normalizing, and phase-folding exoplanet transit light curves using Python and the [`lightkurve`](https://docs.lightkurve.org/) library.

---

## 1. Prerequisites & Environment Setup

Before running the data pipeline, ensure your Python environment has the necessary libraries installed and imported. 

### Installing Dependencies
* **Google Colab:** Install `lightkurve` directly using the `!` shell operator:
  ```bash
  !pip install lightkurve

---

## 2. Astrophysical Concepts

### What is a Light Curve?

A light curve is a time series plot displaying the brightness (flux) of a star over time. When an exoplanet orbits in front of its host star in accordance to our line of sight (a transit), it blocks a portion of the star's light, creating a dip in the light curve.

### Finding Target System Parameters

Target host stars are indexed in celestial catalogs such as the **TIC ID** (TESS Input Catalog ID).

Before running the phase-fold pipeline, obtain the following target parameters from the [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu/):

* **TIC ID:** The unique star catalog identifier.
* **Orbital Period( $P$ ):** The duration of one complete exoplanet orbit expressed in days.
* **Epoch / Mid-Transit Reference( \$t_0\$ ):** The reference time of a transit dip, expressed in offset Barycentric Julian Date( $BJD$ ).

The reference mid-transit time is calculated using $t_0 = \text{BJD} - 2457000$

---

## 3. Light curve Analysis

The complete process executes four core operations:

* **Archive:** Search NASA repositories for available TESS observation sectors.
* **Data Download:** Extract light curve flux arrays.
* **Flux Normalization:** Scale median brightness counts to `1.0` to standardize transit depths.
* **Phase Folding:** Slice continuous time series observations into segments of length $P$ and stack them centered around $t_0$.

## Full Python Implementation

Below is the full Python script executing the full end-to-end light curve analysis workflow:

<!-- Uncomment and replace YOUR_FILE_ID:
![Description](https://drive.google.com/thumbnail?id=YOUR_FILE_ID&sz=w800)
<p class="drive-image-caption">Figure 1: Describe the image</p>
-->

```python
# STEP 1: Get Target Star Data from NASA TESS Archive
# Specify target star TIC ID (Example: WASP-12 / TIC 25145339)
TIC_ID = "TIC 25145339"

# Search for available TESS observation sectors
search_result = lk.search_lightcurve(TIC_ID)
print(search_result)

# STEP 2: Download Raw Light Curve Data
# Download the first available sector dataset "0"
lc_raw = search_result[0].download()

# Plot flux over time
lc_raw.plot(linewidth=0, marker='.', color='midnightblue', alpha=0.8)
plt.title(f"Raw Light Curve - {TIC_ID}")
plt.xlabel("Time (BJD - 2457000)")
plt.ylabel("Raw Flux (e-/s)")
plt.show()

# STEP 3: Normalize Flux Measurements
# Scale median flux to 1.0 to standardize transit depth measurements
lc_norm = lc_raw.normalize()

# Plot normalized light curve
lc_norm.plot(linewidth=0, marker='.', color='palevioletred', alpha=0.8)
plt.title(f"Normalized Light Curve - {TIC_ID}")
plt.xlabel("Time (BJD - 2457000)")
plt.ylabel("Normalized Flux")
plt.show()

# STEP 4: Phase Fold Light Curve Around Orbital Period
# Define target system parameters from NASA Exoplanet Archive(defining is optional)
epoch = 1354.0   # Calculated Epoch (BJD - 2457000)
period = 3.52     # Orbital period in days

# Fold the light curve to stack transit events
lc_folded = lc_norm.fold(period=period, epoch_time=epoch)

# Plot phase-folded data
lc_folded.plot(linewidth=0, color='darkslateblue', marker='.', alpha=0.8)
plt.title(f"Phase-Folded Transit Profile - {TIC_ID}")
plt.xlabel("Orbital Phase")
plt.ylabel("Normalized Flux")
plt.show()
```

---

## About the Results

* Raw Light Curve: Shows photoelectron counts per second ($e^-/s$), often containing background noise or stellar flare activity.
* Normalized Light Curve: Centers baseline flux around `1.0`. A transit dip that drops from `1.0` to `0.98` indicates that the planet blocks $2\%$ of the star's total surface area.
* Phase Folded Transit Profile: Combines dozens of separate orbit cycles into a single visual window. The distinct U-shaped dip confirms an exoplanet transit signal.

