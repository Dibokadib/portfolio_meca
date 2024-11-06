---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: '0.9'
    jupytext_version: 1.5.2
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# What is an inverse problem

## Solving an inverse problem

### Direct methods

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
import matplotlib as mpl
mpl.rcParams['figure.dpi'] = 300
from myst_nb import glue

u1 = np.linspace(0,5,100)
u2 = np.linspace(0,5,100)

fig,ax = plt.subplots(1,1)

alpha = 1e-1

ax.plot(u1,3-u1,'k',label=r'$Ku=f$')
ax.plot(u1,3-(1+alpha)*u1,'r--',label=r'$\widetilde{K}u=f$')
ax.plot(u1,(6-2*u1)/(2+alpha),'r--')

ax.set_xlabel(r'$u_1$')
ax.set_ylabel(r'$u_2$')
ax.set_xlim([0.5,1.5])
ax.set_ylim([1.5,2.5])
ax.set_aspect(1)
ax.legend()
plt.show()
glue("matrix_inversion", fig, display=False)
```

```{glue:figure} matrix_inversion
:figwidth: 300px
:name: "matrix_inversion"

Original and regularized equations. We see that the regularized equations have a unique solution, but this solution is slightly biased towards the origin.
```