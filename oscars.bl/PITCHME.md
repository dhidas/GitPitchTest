# oscars.bl

An OSCARS Beamline Tutorial

---

### What is oscars.bl

- ID Lookup Tables
  - Pre-computed and user LUTs
- Plotting spectra, flux, power density
- Access to magnetic field data

---

### Setup oscars.bl
- Import, create bl object, and setup your beamline
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

---

### Setup beamline
- Select facility, beamline, device

```python
obl = oscars.bl.bl(facility='NSLSII', beamline='FMX', device='IVU21', nthreads=10, gpu=1)
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
- Use the 'show' argument
- Set gap based on result

```python
harmonics = obl.get_gaps(energy_eV=2500, show=True, ofile='oscars.bl.get_gaps.pdf')
obl.set_gap(gap=harmonics[0][1])
```

![get_gaps](assets/image/oscars.bl.get_gaps.pdf)

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
