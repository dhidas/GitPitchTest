# oscars.bl

An OSCARS Beamline Tutorial

---

### What is oscars.bl

- ID Lookup Tables
  - Pre-computed and use input
- Plotting spectra, flux, power density
- Access to magnetic field data

---

![Flux Explained](assets/Test_EPU60_400eVa.pdf)


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
