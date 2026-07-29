# Python

-> A popular, high-level, and general-purpose programming language known for its simple, English-like syntax, readability, and versatility ([Python](https://python.org)).

We use Python for many different things such as:
1. Data Analysis
2. Web Development
3. Automation
4. Everyday Tasks

This is possible with the help of libraries that can be imported into Python.

In this documentation, we will be using Python for finding the light curve of a star using a python library called lightkurve in Google Colab

## Google Colab
[Google Colab](colab.research.google.com) is a free, cloud-based Jupyter Notebook environment hosted by Google.

About Google Colab:

- Based on Jupyter Notebook (cells for code, text, visuals).

- Automatically saves your work to Google Drive.

- Great for data science, machine learning, and education.

- Easy to share and collaborate, like Google Docs.

- Pre-installed with popular Python libraries (NumPy, pandas, matplotlib, TensorFlow, etc.).

- Google Colab is connected to your Google account, no need for installation.

## Importing Packages
->Now we will learn how to import packages in [Google Colab](colab.research.google.com)

Create a new notebook and create a code cell.
In the code cell, write 'import library_name', replacing library_name with the name of any Python Package.
Find Python Libraries [here.](https://www.datacamp.com/blog/top-python-libraries-for-data-science?utm_cid=19589720824&utm_aid=152984014214&utm_campaign=230119_1-ps-other~dsa-tofu~all_2-b2c_3-apac_4-prc_5-na_6-na_7-le_8-pdsh-go_9-nb-e_10-na_11-na&utm_loc=1001788-&utm_mtd=-c&utm_kw=&utm_source=google&utm_medium=paid_search&utm_content=ps-other~apac-en~dsa~tofu~blog~python&gad_source=1&gad_campaignid=19589720824&gbraid=0AAAAADQ9WsEh9Tl5syo7KIn4XFmydQYq4&gclid=EAIaIQobChMI-5WTjeb3lQMVIB-DAx06JiElEAAYASAAEgJiTfD_BwE)

Upon entering Google Colab, instead of creating a new notebook, download this [file](https://chat.google.com/u/0/api/get_attachment_url?url_type=DOWNLOAD_URL&attachment_token=AOo0EEXgurZJWliAIk8sHNE6WIO7uJ%2F%2FQZSpufF1X1KWXrTmnywBsIoZUpcpR8kM%2B%2BoFBxDodUw%2FVwfrCRRYY%2Bi3mgA5%2FxBVZjsSRMY4m%2FK0KLK20Y0lVvuLcMjMJwosoViaHJRaNZL78kRf4oZSiAswuaX3AI4Ya2Frerferk7UBgiQMoodGyWAu2QcOR%2Fv29DdXr6Y%2BZP4e4gMpY4UDky37AUKdBwopWKKCyKaFhyMPx%2B3mtv6EmjoofvC%2BuQiF2R9EKskLp70fIGx7Mu06lDS8kFTzyU4yEH%2BPniuXWPfVAK%2FwvxSwa7RvtVKirnmMdIZnfwzMBeDicVib4BSkQpUbHB0DYeKUQFOHsIsMCymveeew6zAj5USKKQbAXwHWiEU94ZZm52omTSC2q0ImvpEPXAPDEpHKAkpsYefmc65gHWb0K%2BJTri700faOKHsBxsiksheOvJGf1JDrx2TcG3Yp27Q5jCQ73zJ3uz5KvLDYUN4RCVOyyqeF8Eq40eEOHZC%2BO9LhxT9%2FfRujIT2NAKR4s86NhBqNQEViOCSXBxuskOOBXTfjPWZQDP7HgOobgasdFohq0eY7PsRhIuhf3xIrU0XuGqu&auto=true) and upload it on Google Colab.

This is a file in which you can explore on how to find light curve using Google Colab.

## Finding Light Curve of a Star Using Google Colab

In order to find light curve of a star using google colab, we need to install a package called "lightkurve" using the following command.

pip install lightkurve

After doing so, execute the following code in order to import lightkurve library and matplotlibrary.

import lightkurve
import matplotlib.pyplot

Select a star of which light curve you want to find from [NASA exoplanet archive](https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=PS) and find their TIC id.

After doing so run the followig command.

TIC = "Enter your TIC id here"
sector_data = lightkurve.search_lightcurve(TIC)
sector_data

This code will generate a list of data products.

## Plotting Data

In order to plot data, we will be using commands from the matplotlibrary.

lc = sector_data[0].download()
lc.plot(linewidth = 0, marker = '.', color = 'midnightblue', alpha = 0.8 ) #Here you can change the linewidth and alpha.

This code will generate a graph for the data of the star you have collected earlier.

## Normalizing the Graph

We normalize data to bring values into a common, predictable scale or structure.
In order to normalize our graph, we will be using the matplotlibrary.

We will need to use the following code:
lc_norm = lc.normalize()
lc_norm.plot(linewidth = 0, marker = '.', color = 'palevioletred', alpha = 0.8 )
plt.show

After doing this, our previous graph will be normalized with the time and flux values being simpler.

## Folding of the Graph

Folding a graph lightcurve or phase folding, stacks repeating periodic cycles on top of each other.

To fold the graph, we have to find the reference mid-transit time or epoch. The reference mid-transit can be found by subtracting the Barycentric Julian Date by 2457000
-> t0 = BJD - 2457000

We also need to find the orbital period of the star which can be found from [here.](https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=PS)

After finding these values, we can use the following code:

t0 = t0 value goes here
period = period of the star
lc_phased = lc_norm.fold(period = period, epoch_time = t0)
lc_phased.plot(linewidth =0, color = 'darkslateblue', marker='.', alpha=0.8 )

After running this code, we get a new graph which clearly shows the light curve of the star we have chosen.
