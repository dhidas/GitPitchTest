# oscars.th

Information on the oscars.th module

---

### What is oscars.th

- Theoretical calculations for
  - Bending Magnet radiation
  - Wiggler radiation
  - Undulator radiation
- Includes Brightness calculations

---

## Properly setup with oscars.th
- Import the module, setup a beam
```python
import oscars.th

oth = oscars.th.th(gpu=1, nthreads=8)
oth.set_particle_beam(beam='NSLSII-ShortStraight')
```

- Useful for plotting:
```python
from oscars.plots_mpl import *
```

---


### oscars.th.undulator_flux_onaxis()

