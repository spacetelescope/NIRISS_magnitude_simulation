Use of the magnitudes.py program:

  The magnitudes.py code allows one to calculate count rates, flux densities,
magnitudes for a variety of input spectral shapes.  The spectral shapes can
be normalized to a selection of magnitudes, or to a specified flux density at
a specific wavelength.

  The methods used in the code are discussed at some length in the documentation
file "niriss_magnitude_simulation.docx".

  The files in the packge are as follows:

alpha_lyr_mod_002.fits           Template Vega spectral shape from Calspec (2014)
alpha_lyr_stis_005.fits          Template Vega spectral shape from Calspec (2012)
amp00cp00op00t10000g40v20modrt0b300000rs.fits  Example BOSZ model file from MAST.
guider1_throughput.fits          Guider 1 total photon response function
guider2_throughput.fits          Guider 2 total photon response function
lte046.0-2.5-0.0a+0.0.BT-Settl.spec.7.xz  Example Phoenix model from France Allard's web pages.
magnitudes.py                    The simulation code
miri_filter_throughputs.out      MIRI standard throughput values
newkurucz.ascii                  Castelli and Kurucz (2003) stellar atmosphere model values
newkurucz.list                   List of Castelli and Kurucz (2003) models
nircam_filter_throughputs.out    NIRCAM module A standard throughput values
niriss_magnitude_simulation.docx Documentation for the code
non_jwst_filters.data            Throughput values for non-JWST filters
oldkurucz.ascii                  Kurucz (1991) stellar atmosphere model values
oldkurucz.list                   List of Kurucz (1991) models
sirius_mod_002.fits              Template Sirius spectral shape from Calspec
smp_lmc_58_model.txt             Sample ascii model spectrum for SMP LMC 58
standard_throughputs             Directory hold NIRISS standard throughput files

See the Calspec web page http://www.stsci.edu/hst/observatory/crds/calspec.html
for more information about the standard Vega and Sirius spectral templates.

  The code simulates magnitudes by comparing the integrated photon count rate
(for JWST instruments) or the integrated wavelength flux density (for non-JWST
filters) of the specified input spectral shape to that of an A0V spectral
template, and uses the relative values to produce simulated magnitudes.  The
only exception to this is the Sloan magnitude simulations, which follow a
perscription from the literature.  This makes the Sloan magnitude simulation
less accurate than the other magnitude simulations, and these should therefore
be used with caution.  One can select either Sirius, magnitude -1.415 at all
wavelengths by assumption, or Vega, magnitude +0.03 or 0.0 at all wavelengths
depending on which set of magnitudes is being calculated, as the A0V spectral
template.  For Vega one can select the current Calspec template (2014) or the
previous Calspec template (2012).  All three of these spectral templates are
from work by Ralph Bohlin.

  To run the code three environment variables need to be defined.  If the
package is unpacked in directory /home/auser/niriss_magnitudes, for example,
and the standard throughput files are left in the standard_througputs directory
below the main directory then the commands would be

export NIRISS_MAGNITUDES_PATH='/home/auser/niriss_magnitudes'
export NIRISS_PHOENIX_PATH='/home/auser/phoenix_grid'
export NIRISS_THROUGHPUT_PATH='/home/auser/niriss_magnitudes/standard_throughputs'

in the bash shell or

setenv NIRISS_MAGNITUDES_PATH '/home/auser/niriss_magnitudes'
setenv NIRISS_PHOENIX_PATH '/home/auser/phoenix_grid'
setenv NIRISS_THROUGHPUT_PATH '/home/auser/niriss_magnitudes/standard_throughputs'

in the C-shell or TC-shell.  The second path is a directory where one can put
the Phoenix grid files from Husser et al. (2013) for use with the program.  The
Phoenix model grid files can be obtainsd from

ftp://phoenix.astro.physik.uni-goettingen.de/v2.0/HiResFITS/

Any models from this grid with names of the form

lte12000-6.00-0.0.PHOENIX-ACES-AGSS-COND-2011-HiRes.fits

found in the specified directory will be avilable for use in the code.  One
also needs the wavelengths file

WAVE_PHOENIX-ACES-AGSS-COND-2011.fits

in the directory.

  The code uses Python 2.7.  Adaptation to Python 3 would require changing a
few of the input statements at the beginning of the file.  Also note that the
first line

#! /usr/bin/env python

may need to be changed on some systems if one wishes the code to be executable
without calling python.  One can always invoke the code with a command such
as

python magnitudes.py

whether or not the first line points to a valid Python installation.

  Packages used by the code are:

matplotlib 
sys
os
math
bisect
Tkinter 
ttk
numpy 
glob
astropy

Depending on one's system type one may need to change the statement on line
106 of the code

matplotlib.use('TkAgg')

to some other plotting "abckend".  See the matplotlib documentation.

  The package includes some sample spectral files for the non-Kurucz options.
These include

amp00cp00op00t10000g40v20modrt0b300000rs.fits  
lte046.0-2.5-0.0a+0.0.BT-Settl.spec.7.xz  
smp_lmc_58_model.txt             

which are used with the "BOSC model", "Phoenix Model" and "Input Spectrum"
options respectively.  The first model is for a star of spectral type A0V,
the second for a star of spectral type K1III, and the third is a model spectrum
for a planetary nebula, to apporximately match source SMP LMC 58.  The latter
model is from the CLOUDY photoionization code, and includes dust emission at
long wavelengths; the dust emission does not match the observed Sptizer spectrum
very well, but it serves for illustration none the less.


