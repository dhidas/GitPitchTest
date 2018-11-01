# oscars.bl

An OSCARS Beamline Tutorial





---
### What is oscars.bl
These slides contain information on the oscars.bl module:
- ID Lookup Tables: Pre-computed and user defined LUTs
- Easily plotting simple spectra, flux, power density
- Access to magnetic field data
- Access to all of OSCARS functionality

Where to find more help:
- Email: [oscars@bnl.gov](mailto:oscars@bnl.gov)
- Website: [https://oscars.bnl.gov](https://oscars.bnl.gov)
- GitHub: [https://github.com/dhidas/OSCARS](https://github.com/dhidas/OSCARS)





---
### Setup oscars.bl
- Import the oscars.bl module.  With no beamline given it will print available options
- Choose your nthreads and gpu options

```python
import oscars.bl
obl = oscars.bl.bl(nthreads=10, gpu=1)
```


```
You can select from the available facility, beamline, and device list:
    Beamline     Device           Modes
    --------     ------           -----

NSLSII
    HXN          IVU20            planar
    AMX          IVU21            planar
    SST          EPU60            planar
    SST          U42              planar
    FMX          IVU21            planar
    SRX          IVU21            planar
    NYX          IVU18            planar
```
If using a non-standard data directory:
```python
obl = oscars.bl.bl(base_path='/Users/dhidas/OSCARSDATA', nthreads=10, gpu=1)
```





---
### Setup beamline
- Select facility, beamline, device when creating the oscars.bl object

```python
obl = oscars.bl.bl(facility='NSLSII', beamline='SST', device='U42', nthreads=10, gpu=1)
```
- Get a summary
```python
obl.summary()
```

![Summary](assets/image/oscars.bl.summary.pdf)





---
### Find Gaps for Given Energy
- Get gaps for desired energy

```python
obl.get_gaps(energy_eV=2500)
```

```
[[3, 20.41260062528832, 232409062443786.88],
 [5, 15.3509438307999, 200487396194740.56],
 [7, 12.511593639705136, 144330373520935.03]]
```
- Each element is [harmonic, gap, flux]





---
### Show Plot and set Gap
- Use the 'show' argument too produce a nice plot
- Can save plots
- Set the gap based on result with highest flux (list is ordered)

```python
harmonics = obl.get_gaps(energy_eV=2500, show=True, ofile='oscars.bl.get_gaps.pdf')
obl.set_gap(gap=harmonics[0][1])
```

![](assets/image/oscars.bl.get_gaps.pdf)





---
### Get Spectrum
- Easy to plot and save spectra.  Example of single-electron spectrum.  Any of the following will work
```python
s = obl.spectrum()
s = obl.spectrum(gap=20.412)
s = obl.spectrum(fofile='oscars.bl.spectrum.pdf')
```

![](assets/image/oscars.bl.spectrum.pdf)

- s is the spectrum as a python list





---
### More plotting options
- For any oscars.bl plot more plotting options exist in the full version, for example

```python
oscars.plots_mpl.plot_spectrum(s, title='Hello', figsize=[12, 2], color='r', ylabel='Intensity [a.u.]')
```

![](assets/image/oscars.bl.spectrum_more.pdf)

- see documentation for [oscars.plots_mpl](https://oscars.bnl.gov/doc/latest/Modules.html#oscars-plots-mpl)





---
### Calculate Single and Multi-Particle spectra
- Zoom in on a harmonic, calculate the single and multi-particle spectra
```python
s_se = obl.spectrum(energy_range_eV=[2400, 2600], show=False)
s_me = obl.spectrum(energy_range_eV=[2400, 2600], show=False, nparticles=500)
```
- Plot them togetner for comparison
```python
obl.plot_spectra(spectra=[s_se, s_me], label=['single-electron', 'multi-electron'])
```

![](assets/image/oscars.bl.spectra.pdf)





---
### Calculate Flux
- Calculate the single particle flux and save to file

```python
f_se = obl.flux(energy_eV=2500, fofile='oscars.bl.flux_se.pdf')
```

![](assets/image/oscars.bl.flux_se.pdf)





---
### Calculate Flux - Multi-Particle
- Need only to add 'nparticles' argument

```python
f_me = obl.flux(energy_eV=2500, nparticles=3, fofile='oscars.bl.flux_me.pdf')
```

![](assets/image/oscars.bl.flux_me.pdf)

- You should use more particles.  These calculations can be time consuming.





---
### Power Density
- Calculate the power density on a plane
- Most beamlines will not need multi-particle simulation for this

```python
pd = obl.power_density(fofile='oscars.bl.power_density.pdf')
print('Total Power', obl.total_power(), '[W]')
```

![](assets/image/oscars.bl.power_density.pdf)

```
Total Power 862.3209364892316 [W/mm^2]
```





---
### Power Density
- Each beamline is setup with defaults, but everything is configurable, for instance changing width and resolution

```python
pd = obl.power_density(width=[0.05, 0.05], npoints=[101, 201], fofile='oscars.bl.power_density_width.pdf')
```

![](assets/image/oscars.bl.power_density_width.pdf)

- Details of the calculations are in [oscars.sr](https://oscars.bnl.gov/doc/latest/Modules.html#oscars-sr)





---
### Configuration
- Default configuration is stored within the file tree at self.base_path in config.ini files
- All default configuration can be overridden by user input
- Can print current cinfiguration

```python
obl.info()
```
```
***BEGIN CONFIG***
beam
  type electron
  current 0.500
  energy_gev 3
  sigma_energy_gev 0.00267
  emittance 0.9e-9 0.008e-9
...
```





---
### Showing Plots and Return Objects
- If you don't want to 'show' the plots
```python
obl.show_all = False
```
- If you don't want return objects
```python
obl.return_all = False
```





---
### Importing a User LUT
- Import your own LUT (example structure next page)

```python
obl.read_file_lut1d('/Users/dhidas/OSCARSDATA/Facilities/NSLSII/SST/U42/bfield/planar/lut1d.txt')
obl.name = 'MYBL UF42'
obl.get_gaps(show=True)
```

![](assets/image/oscars.bl.example.lut1d.pdf)





---
### Example LUT 1D
- List harmonics
- Each row is then: energy gap flux

```
harmonic 1
 313.3 11.5 175950363894016.0
 402.0 13.5 215719549781888.0
 764.9 19.5 327973629641984.0
1574.0 31.0 263515296448896.0
2008.3 55.0  10694510247968.0

harmonic 3
 941.4 11.5 212151858914304.0
1440.8 15.0 257096550147072.0
1890.4 17.5 262521650105344.0
2409.0 20.0 237708903371776.0
5033.1 33.0  17420581029248.0
```





---
### Saving Calculation Data
- For any calculation you can save the raw data in text format by simply adding the 'ofile' argument

```python
obl.spectrum(energy_range_eV=[2400, 2600], ofile='oscars.bl.spectrum.txt')
```
- Which gives in text format
```
2.400000e+03 1.155150e+12
2.401000e+03 1.318041e+12
2.402000e+03 1.445257e+12
2.403000e+03 1.525704e+12
2.404000e+03 1.551536e+12
2.405000e+03 1.519291e+12
2.406000e+03 1.429881e+12
2.407000e+03 1.289482e+12
2.408000e+03 1.108632e+12
2.409000e+03 9.024489e+11
2.410000e+03 6.889639e+11
2.411000e+03 4.885630e+11
...
```





---
### Comments or Suggestion
- Please email us at [oscars@bnl.gov](mailto:oscars@bnl.gov)

- And visit [https://oscars.bnl.gov](https://oscars.bnl.gov)

Thank you for stopping by!
