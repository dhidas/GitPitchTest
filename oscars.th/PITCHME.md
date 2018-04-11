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

$$ J_{(n-1)/2} (\frac{n K^2}{4 + 2 K^2}) - J_{(a + b)} $$
---


### undulator_flux_onaxis()
Calculates the on-axis undulator flux according to 
`$$ \frac{d\Phi_n}{d\Omega} (0, 0, \omega_n, \hat u ) = \alpha \frac{I}{e} N^2 \gamma^2 | \hat u_x \hat u^* |^2 F_n(K) $$`

---

where
`$$F_n(K) = \frac{n^2 K^2}{(1 + (K^2 / 2))^2} ( J_{(n-1)/2}(\frac{nK^2}{4 + 2K^2}) - J_{(n+1)/2} (\frac{nK^2}{4 + 2K^2}))^2$$`

