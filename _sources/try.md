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


````{admonition} Example: *Inverting a rank-deficient matrix.*
Consider the matrix 

$$
K = \left(\begin{matrix} 1 & 1\\ 2 & 2 \end{matrix}\right).
$$

Obviously this matrix is singular, so there is no way to define the inverse in the usual sense. However, modifying the matrix slightly

$$
\widetilde{K} = \left(\begin{matrix} 1 + \alpha & 1\\ 2 & 2 + \alpha\end{matrix}\right),
$$

allows us to compute the inverse. Indeed, given $f = K\overline{u}$ with $\overline{u} = (1,2)$ we have $f = (3,6)$. Applying the inverse of $\widetilde{K}$ we get $\widetilde{u} \approx (1,2)$. The corresponding equations are visualized in {numref}`matrix_inversion`.

```{glue:figure} matrix_inversion
:figwidth: 300px
:name: "matrix_inversion"

Original and regularized equations. We see that the regularized equations have a unique solution, but this solution is slightly biased towards the origin.
```

````

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