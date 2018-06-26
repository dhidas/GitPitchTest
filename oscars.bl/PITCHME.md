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

---?image=path/to/image.file&position=center&border=0

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
