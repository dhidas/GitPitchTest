# oscars.bl

An OSCARS Beamline Tutorial

---

### What is oscars.bl

- ID Lookup Tables: Pre-computed and user defined LUTs
- Easily plotting simple spectra, flux, power density
- Access to magnetic field data
- Access to all of OSCARS functionality

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

- For more plotting options use the full version
```python
oscars.plots_mpl.plot_spectrum(s, title='Hello', figsize=[6, 1], color='r')
```

![](assets/image/oscars.bl.spectrum_more.pdf)

---


















---

![Flux Explained](assets/image/Test_EPU60_400eV.pdf)

---


```python
s = "Python syntax highlighting"
print s
```


---

```python
for i in range(10):
    print('bite me')

osr = oscars.sr.sr(gpu=1, nthreads=10)
osr.add_bfield(123)
```
