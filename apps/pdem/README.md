pdem
====

Line networks extraction in digital images using geodesic propagation and flow simulation
---

**About**

We implement an improved method for semi-automatic extraction of line networks in digital images that is:
* derived from morphological and hydrological concepts since it consists in minimum cost path estimation and flow simulation,
* fully exploits the local contrast and shape of the target network, as well as its arborescent nature,
* further incorporates local directional information about the structures in the image,

For that purpose, an appropriate anisotropic metric is derived from both the characteristic features of the  network and the gradient information of the image. Following, a geodesic propagation based on this metric is combined with hydrological operators for overland flow simulation to extract the line network from known seeds.

**Usage** 

The documentation of the algorithm, including a full description of the required/optional input/output parameters, is available through function [**pdem**](https://gjacopo.github.io/imtools/surface/pdem.html). The stepwise implementation of the algorithm is further described through function [**pdem_base.m**](https://gjacopo.github.io/imtools/docs/surface/pdem_base.html).

To reproduce the experiments, you will need to:
* install Matlab ad-hoc package [**`imtools`**](https://gjacopo.github.io/imtools/); _e.g._, add the paths of the install to your `pathdef.m` setup file;
* run the function **`pdem.m`** ([source](../../surface/pdem.m)) with desired arguments.

See some examples of generated outputs [here](paper.ipynb).

Details about the actual implementation of the gradient tensor decomposition are given in the documentation of functions [`gstdecomp.m`](https://gjacopo.github.io/imtools/derive/gstdecomp.html) and [`gstfeature.m`](https://gjacopo.github.io/imtools/derive/gstfeature.html). 

**Description**

The developed technique combines, likewise watershed based segmentation, concepts arising from mathematical morphology and hydrology [[SG07]](#SG07). It performs the robust extraction of line networks by applying minimum cost path techniques [[PPKC10](#PPKC10), [Soille94](#Soille94), [IT07](#IT07)] and using directional information about the local structures in the image [[Kothe03]](#Kothe03) so as to look for the path which contains most line evidence. In addition, it fully exploits the fact that the hydrographic network has a tree-like structure (with a root) and the knowledge of arborescent networks [[SG07]](#SG07).

A detailed description of the approach is available on this [**notebook**](paper.ipynb). The generic algorihtm for extracting line networks from a single image can be summarised as follows:
1. define the reference set as the set of outlets and seeds of the target network, _e.g._ pixels belonging most surely to it;
3. incorporate directional information about the local structures in the image through the computation of the eigenvalues of the Gradient Structure Tensor;
5. calculate the local flow directions of the pseudo DEM and use its Contributing Drainage Areas (CDA) as a proxy to evidence the presence of a network, using an improved non-dispersive flow estimation technique;

**<a name="References"></a>References** 

* <a name="IT07"></a>Ikonen L. and Toivanen P. (2007): **Distance and nearest neighbor transforms on
* <a name="Kothe03"></a>Kothe U. (2003): **Integrated edge and junction detection with the boundary
* <a name="PPKC10"></a>Peyre G., Pechaud M., Keriven R., and Cohen L. (2010): [**Geodesic methods in computer vision and graphics**](https://hal.archives-ouvertes.fr/hal-00528999/document), _Foundations and Trends in Computer Graphics and Vision_, 5(3/4):197-397, doi:[10.1561/0600000029](http://dx.doi.org/10.1561/0600000029).
* <a name="Soille94"></a>Soille, P. (1994): **Generalized geodesy via geodesic time**, _Pattern Recognition Letters_, 15(12):1235-1240, doi:[10.1016/0167-8655(94)90113-9](http://dx.doi.org/10.1016/0167-8655(94)90113-9).

