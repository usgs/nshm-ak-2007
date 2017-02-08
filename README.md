## NSHMP Alaska 2007
**NOTE: This model is preliminary and for review purposes only. It is intended for use with an updated USGS earthquake hazards codebase: [nshmp-haz](https://github.com/usgs/nshmp-haz). It is currently under review and does NOT represent an official release or product. For official release products please see the [USGS Earthquake Hazards](http://earthquake.usgs.gov/hazards/) website.**

For details on the format of this hazard model, see the [nshmp-haz wiki](https://github.com/usgs/nshmp-haz/wiki).

See also the [2007 USGS Alaska Earthquake Hazard Maps & Data](http://earthquake.usgs.gov/hazards/products/ak/).

### Implementation Details

Notable implementation details (in fortran source and inputs) that set Alaska 2007 apart from later COUS models and this updated nshmp-haz implementation of the Alaska model:

* Grid and slab optimization tables use discretization of 2km out to 200km.
  * nshmp-haz: __discretization = 1km__
* Grid and slab sources use the Wells & Coppersmith (1994) magnitude-length scaling relation.
  * nshmp-haz: __slab sources use Youngs et al. (1997)__ (aka 'geomatrix'; consistent with 2014 COUS NSHM)
* Grid and slab sources randomize strike at M≥6.
  * nshmp-haz: __uses point-source distance corrections for M≥6__ (in relations above; consistent with 2014 COUS NSHM)
* Ground motion models do not impose one-sided 3σ upper truncation on exceedances.
  * nshmp-haz: __no change__
* Other details:
  * nshmp-haz: __grid source maxDepth = 15 km__
* Focal mechansim variations are encoded into coefficients supplied with each input file; flavors for strike-slip and mixed strike-slip/reverse were ported from the 2002 COUS model.
  * nshmp-haz: __point sources generate focal mechanism specific ruptures with appropriate rake that are processed independently, consistent with 2014 COUS NSHM__
* Aleatory uncertainty was added in the 2002 COUS model and was carried over here as a moment-balanced Gaussian distribution on mMax of M±0.15 discretized over 5 values with σ=0.12. The 2008 COUS model increased the width of the distribution to M±2σ and increased the discretization to 11 values. Both implementations require custom code; the more recent approach is more straightforward with the distribution a function of σ.
  * nshmp-haz: __uses more recent (11-point; ±2σ) aleatory uncertainty model__
* Hazard curves are not truncated at 3σ.
  * nshmp-haz: __no change__

### Other Notes

* Consistent with 2008 and 2014 COUS models, slab and grid Gutenberg-Richter MFD magnitudes bins are centered on 0.05; interface MFD bins are centered on 0.1.
