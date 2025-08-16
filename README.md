# Verification and Validation of Neutronics Codes

## Existing Validation

Validation of neutronics codes in a **fission environment** is a well-established procedure, partly due to the large quantity of experimental results such as the International Criticality Safety Benchmark Evaluation Project (ICSBEP) [[1]](#ref1) and other open-access benchmarks.

Criticality experiment calculations provide particularly precise measurements for comparing codes with experiments since reactivity can be measured to accuracies of one-thousandth of a percent (pcm).

By contrast, validation of neutronics codes in **fusion and accelerator environments** is less established, as fusion neutrons are generally less available and sources are not characterized to the same degree of accuracy. Although neutron transport in fission and fusion share many fundamental similarities, the higher energy range of particles in fusion leads to a larger variety of reactions and therefore requires independent validation. This is particularly true for **DT fusion**, where the neutron energy is sufficient to induce additional nuclear reactions above threshold energies.

**OpenMC** [[2]](#ref2) has been designed with validation in mind, providing modern software practices that are not always present in legacy codes. Since OpenMC is open source, many of its tests are publicly available, including:

* continuous integration [[3]](#ref3)
* unit tests [[4]](#ref4)
* regression tests [[5]](#ref5)
* analytical benchmarks [[6]](#ref6)
* validation suite (including ICSBEP and 7 other benchmark series) [[7]](#ref7)

User-driven validation has also resulted in several fission reactor benchmark studies for specific designs, such as:

* VERA core benchmarks [[8]](#ref8)
* Burnup benchmark [[9]](#ref9)
* BEAVRS benchmark series [[10]](#ref10)–[[12]](#ref12)
* Light water reactor (LWR) benchmark [[13]](#ref13)

Despite these advancements, there remains a need to add **fusion-relevant benchmarks** (e.g., shielding benchmarks with 14 MeV neutrons) to the open validation suite, which will further establish OpenMC as a reliable neutronics code.

The benefit of openly accessible validation goes beyond ease of access: benchmarks are reproducible when possible. Where models are open (e.g., CONDORC benchmarks [[14]](#ref14)), it is possible to reproduce entire simulations. However, in the case of SINBAD and ICSBEP, which are NEA-licensed, geometry is not openly available. In such cases, the common practice is to share input and post-processing aspects without specific geometry. Users wishing to reproduce simulations must acquire geometry and licenses from the NEA.

---

## Ongoing Validation Efforts

Benchmarking of neutronics codes for **shielding applications** is a vital step in validation. The **SINBAD suite** [[15]](#ref15) of shielding benchmarks is available in two formats: most in **MCNP CSG** format, and others only as diagrams.

This distribution favors a single code (MCNP). Validating other codes requires geometry translation. The development of **CSG2CSG** [[16]](#ref16) eases this process by converting MCNP CSG geometry into formats compatible with other codes, such as OpenMC.

Currently, six SINBAD benchmarks have been converted and simulated using the CSG2CSG approach, showing good agreement between MCNP and OpenMC.

Additionally, **MCNP2CAD** [[17]](#ref17) converts MCNP CSG geometry into CAD, which can then be faceted for DAGMC [[18]](#ref18). Using faceted geometry enables running models across multiple DAGMC-compatible codes (OpenMC, FLUKA, MCNP, Tripoli-4, Geant4).

For benchmarks available only as diagrams, two routes can be pursued:

1. Write geometry in MCNP format, then convert via MCNP2CAD/CSG2CSG.
2. Script CAD geometry creation using open-source tools such as **OpenCascade**, **FreeCAD** [[19]](#ref19), **CADQuery**, or **OpenSCAD**. Scripted creation is preferred to enable reproducibility and flexibility.

With the recent introduction of **DLopen** in OpenMC [[20]](#ref20), it is now possible to model complex compiled sources such as plasma sources and the Frascati Neutron Generator (FNG).

An open-source **OpenMC workshop** [[21]](#ref21) has already trained \~40 students and provides a foundation for developing the skills needed for validation efforts.

Ideally, the SINBAD suite should exist in both **CSG and CAD formats** for every neutronics code, enabling straightforward comparison across codes and geometry types. In the longer term, initiatives like **European Open Data** could allow shielding benchmarks to be freely distributed, enabling their inclusion in regression testing and continuous integration. An open-source release of a **multi-code, multi-geometry SINBAD suite** could significantly increase the impact of these efforts.

While the target is to eventually cover the entire SINBAD suite, prioritization will be necessary, focusing on benchmarks that provide high value and ease of implementation.

---
## References

<a name="ref1"></a>[1] J. B. Briggs, L. Scott, and A. Nouri, “The International Criticality Safety Benchmark Evaluation Project,” *Nucl. Sci. Eng.*, vol. 145, no. 1, pp. 1–10, 2003.

<a name="ref2"></a>[2] P. K. Romano *et al.*, “OpenMC: A State-of-the-Art Monte Carlo Code for Research and Development,” in *SNA + MC 2013*, 2014, pp. 06016.

<a name="ref3"></a>[3] OpenMC continuous integration server. \[Online]. Available: [https://travis-ci.org/openmc-dev/openmc](https://travis-ci.org/openmc-dev/openmc)

<a name="ref4"></a>[4] OpenMC unit tests repository. \[Online]. Available: [https://github.com/openmc-dev/openmc/tree/develop/tests/unit\_tests](https://github.com/openmc-dev/openmc/tree/develop/tests/unit_tests)

<a name="ref5"></a>[5] OpenMC regression tests repository. \[Online]. Available: [https://github.com/openmc-dev/openmc/tree/develop/tests/regression\_tests](https://github.com/openmc-dev/openmc/tree/develop/tests/regression_tests)

<a name="ref6"></a>[6] A. Sood, R. A. Forster, and D. K. Parsons, “Analytical benchmark test set for criticality code verification,” *Prog. Nucl. Energy*, vol. 42, no. 1, pp. 55–106, 2003.

<a name="ref7"></a>[7] MIT Computational Reactor Physics Group, Collection of models for reactor physics benchmarks. \[Online]. Available: [https://github.com/mit-crpg/benchmarks](https://github.com/mit-crpg/benchmarks)

<a name="ref8"></a>[8] T. J. Labossiere-Hickman and B. Forget, “Selected VERA Core Physics Benchmarks in OpenMC,” *Trans. Am. Nucl. Soc.*, vol. 117, pp. 1520–1523, 2017.

<a name="ref9"></a>[9] K. S. Chaudri and S. M. Mirza, “Burnup dependent Monte Carlo neutron physics calculations of IAEA MTR benchmark,” *Prog. Nucl. Energy*, vol. 81, pp. 43–52, 2015.

<a name="ref10"></a>[10] D. J. Kelly *et al.*, “Analysis of select BEAVRS PWR benchmark cycle 1 results using MC21 and OpenMC,” in *PHYSOR 2014*, vol. 47, 2015.

<a name="ref11"></a>[11] N. Horelik *et al.*, “Benchmark for evaluation and validation of reactor simulations (BEAVRS),” MIT Computational Reactor Physics Group, Tech. Rep., 2013.

<a name="ref12"></a>[12] J. A. Walsh, B. Forget, and K. S. Smith, “Validation of OpenMC Reactor Physics Simulations with the B and W 1810 Series Benchmark,” *Trans. Am. Nucl. Soc.*, pp. 1301–1304, 2013.

<a name="ref13"></a>[13] B. R. Herman *et al.*, “Analysis of tally correlation in large light water reactors,” *JAEA Conf.*, vol. 47, 2015.

<a name="ref14"></a>[14] IAEA, CONDERC open validation benchmarks. \[Online]. Available: [https://www-nds.iaea.org/conderc/](https://www-nds.iaea.org/conderc/)

<a name="ref15"></a>[15] SINBAD Benchmark Suite. \[Online]. Available: [https://inis.iaea.org/search/search.aspx?orig\_q=RN:43000913](https://inis.iaea.org/search/search.aspx?orig_q=RN:43000913)

<a name="ref16"></a>[16] CSG2CSG. \[Online]. Available: [https://github.com/makeclean/csg2csg](https://github.com/makeclean/csg2csg)

<a name="ref17"></a>[17] MCNP2CAD. \[Online]. Available: [https://github.com/svalinn/mcnp2cad](https://github.com/svalinn/mcnp2cad)

<a name="ref18"></a>[18] P. Wilson, T. Tautges, J. Kraftcheck *et al.*, “Acceleration techniques for the direct use of CAD-based geometry in fusion neutronics analysis,” *Fusion Eng. Des.*, pp. 1759–1765, 2010.

<a name="ref19"></a>[19] J. Riegel, W. Mayer, and Y. van Havre, FreeCAD, v0.17. \[Online]. Available: [http://freecadweb.org/](http.freecadweb.org/)

<a name="ref20"></a>[20] OpenMC DLopen pull request. \[Online]. Available: [https://github.com/openmc-dev/openmc/pull/1257](https://github.com/openmc-dev/openmc/pull/1257)

<a name="ref21"></a>[21] OpenMC Workshop. \[Online]. Available: [https://github.com/shimwell/openmc\_workshop](https://github.com/shimwell/openmc_workshop)