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
Import the module, setup a beam:

```python
import oscars.th
oth = oscars.th.th(gpu=1, nthreads=8)
oth.set_particle_beam(energy_GeV=3, sigma_energy_GeV=3*0.00089,
                      current=0.5, emittance=[0.55e-9, 8e-12],
                      beta=[1.5, 0.8])
```

Useful for plotting:

```python
from oscars.plots_mpl import *
```

---


### oscars.th.undulator_flux_onaxis()

