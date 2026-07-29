# Light Curve using Google Colab

An introduction to analyzing exoplanet transit light curves using Python and the [`lightkurve`](https://docs.lightkurve.org/) library.

### What is Python?
[Python](https://python.org) is a high-level, general-purpose programming language known for its simple syntax and readability. In astrophysics, it is used for data analysis, automation, and scientific visualization.

### Tools & Libraries
* **Lightkurve:** A Python package for analyzing time-series pixel and light curve data from NASA's Kepler, K2, and TESS space telescopes.
* **Google Colab:** A cloud-based platform hosted by Google for running Python scripts without local setup.

---

## Analysis Pipeline

**TIC IDs** (TESS Input Catalog IDs) and other datas of the stars can be obtained from the [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu/).

Epoch time ($t_0$) is obtained from the Barycentric Julian Date ($\text{BJD}$) using:
$$t_0 = \text{BJD} - 2457000$$

### Complete Code

```python
# 1. Install & import packages
!pip install lightkurve
import lightkurve as lk
import matplotlib.pyplot as plt

# 2. Query target star data from NASA archive
TIC = "TIC 25145339"  # Replace with target TIC ID
sector_data = lk.search_lightcurve(TIC)

# 3. Download raw light curve data
lc = sector_data[0].download()

# Plot raw light curve
lc.plot(linewidth=0, marker='.', color='midnightblue', alpha=0.8)
plt.title("Raw Light Curve")
plt.show()

# 4. Normalize the light curve
lc_norm = lc.normalize()

# Plot normalized light curve
lc_norm.plot(linewidth=0, marker='.', color='palevioletred', alpha=0.8)
plt.title("Normalized Light Curve")
plt.show()

# 5. Phase-fold light curve using target parameters
t0 = 1354.0   # Calculated epoch (BJD - 2457000)
period = 3.52 # Orbital period in days

lc_phased = lc_norm.fold(period=period, epoch_time=t0)

# Plot phase-folded transit profile
lc_phased.plot(linewidth=0, color='darkslateblue', marker='.', alpha=0.8)
plt.title("Phase-Folded Light Curve")
plt.show()
