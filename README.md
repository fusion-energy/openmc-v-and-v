# openmc-v-v
A document highlighting the various V&amp;V


\section{Existing validation}


Validation of neutronics codes in a fission environment is generally well established procedure, this is partly due to the large quantity of experimental results such as ICSBEP \cite{iscbep} and open access benchmarks.

Criticality experiments calculations provide a particularly precise measurement for comparing codes with experiments as the value is known to a high degree of accuracy and codes can be compared on their prediction of reactivity measured to accuracies of one-thousandth of a percent (pcm).

Validation of neutronics codes in a fusion and accelerator environments is less established as fusion neutrons are generally less available and sources are not characterised to the same degree of accuracy.

Although neutron transport in fission and fusion share many fundamental similarities, the higher energy range of particles results in a larger variety of reactions and therefore merits independent validation.

This is particularly true for DT fusion where the neutron energy is sufficient for additional nuclear reactions that have an energy threshold.  

OpenMC \cite{OpenMC} has been designed with validation in mind with the provision of modern software practices that are not always present in legacy codes. As OpenMC is an open source much of the tests are publicaly available. 
\begin{itemize}
  \item continuous integration \cite{OpenMC_CI}
  \item unit tests \cite{OpenMC_UT} 
  \item regression tests \cite{OpenMC_regT}
  \item analytical benchmarks \cite{openmc_keff_analytical_benchmarks}
  \item validation suite (including ICSBEP and 7 other benchmark series) \cite{OpenMC_benchmark_suite}
\end{itemize}


User driven validation several fission reactor benchmarks have been carried out for specific designs:
\begin{itemize}
    \item \cite{openmc_vera_core_benchmarks}, 
    \item \cite{openmc_burnup_benchmark}
    \item \cite{openmc_beavrs_benchmark}
    \item \cite{openmc_beavrs2_benchmark}
    \item \cite{openmc_beavrs3_benchmark}
    \item \cite{openmc_lwr_benchmark}.
\end{itemize}

There remains a need to add fusion relevant benchmarks (shielding benchmarks with 14MeV neutrons) to the open validation suite which will help further establish OpenMC as a reliable neutronics code.

The benefit of openly accessible validation goes beyond ease of access and the benchmarks are reproducible when possible.

Where the models are open it is entirely (e.g. \cite{Conderc}) possible to reproduce the entire simulations, however in the case of SINBAD and ICSBEP which are NEA licensed then this is not possible.
Share the input and post processing aspects of the benchmark without the specific geometry is the standard approach.
People wishing to reproduce the simulations will have to acquire the geometry and usage license from the NEA to reproduce these proritory benchmarks.


\section{Ongoing validation efforts}



Benchmarking of neutronics codes for shielding is a vital step in validating neutronics codes. The Sinbad suite \cite{Sinbad_benchmark_suite} of shielding benchmarks is available in two formats. The majority of models are available in MCNP constructive solid geometry (CSG) geometry format while some models are just available in diagram form.





This existing distribution suits just one individual code (MCNP). Validating additional codes therefore comes with the overhead of translating the geometry into geometry native to the neutronics code. 



The development of CSG2CSG \cite{CSG2CSG} eases the translation of MCNP formatted CSG geometry into other CSG formats. For example using CSG2CSG one can translate MCNP into OpenMC. OpenMC supports CSG geometry but also supports faceted geometry that can easily be created from CAD geometry. 

mention the oak ridge code that simulates multiple models and pyarc from argonne and Oxford sigmas beast


Currently 6 of Sinbad benchmarks have been converted and simulated using the CSG2CSG approach and produce good agreement between MCNP and OpenMC.


The development of MCNP2CAD \cite{mcnp2cad} can convert MCNP CSG geometry into CAD geometry. CAD geometry can then be faceted and used in neutronics simulations using DAGMC \cite{dagmc}. The benefit of using faceted geometry is that the model could then be run in any DAGMC compatible code (OpenMC, Fluka, MCNP, Tripoli4, Geant4). 


Converting the models in Sinbad that exist only in diagram form into useful formats for neutronics could be performed via two different routes. One could write up the geometry in MCNP format then convert it into other formats using MCNP2CAD and CSG2CSG. Alternatively one could use Opencascade (python or C++) or FreeCAD (python), CAD Query (python) to script the creation of CAD geometry. Both programs allow the creation of CAD geometry from numbers which can be found on the diagrams. Another option is OpenSCAD which could be considered and provides a more CSG friendly input. It is preferential that the creation is performed via script in an opensource CAD tool so that potential users all have the ability to recreate the CAD if they want to tweak parts.


With the recent creation of the DLopen addition \cite{dlopen} to OpenMC we now have the ability to model complex compiled sources such as a plasma sources and the Frascati neutron generator (FNG). 

An opensource OpenMC training course \cite{openmc_workshop} has now been used to train approximately 40 students and this resource would also be used to facilitate the aquistion of OpenMC skills needed for the project.

Ideally the Sinbad suite would exist in both CSG format for every neutronics code and also in CAD format. One could then easily compare results between codes and geometry types.

In the longer term with initiatives like the European Open Data we could see shielding benchmarks more freely distributed. This would allow them to be included in regression testing and continuous integration. An opensource release of multi code, multi geometry Sinbad benchmark suite is something that could increase the impact any effort spent creating the suite. While the target is to cover the full Sinbad suite we must priorities benchmarks based on ease of geometry, model creation and value. 






@misc{conderc,
  title = {{IAEA Conderc open validation benchmarks}},
  howpublished = {\url{https://www-nds.iaea.org/conderc/}},
}

@article{iscbep,
    author = {J. Blair Briggs and Lori Scott and Ali Nouri},
    title = {The International Criticality Safety Benchmark Evaluation Project},
    journal = {Nuclear Science and Engineering},
    volume = {145},
    number = {1},
    pages = {1-10},
    year  = {2003},
    publisher = {Taylor & Francis},
    doi = {10.13182/NSE03-14},
    URL = {https://doi.org/10.13182/NSE03-14},
    eprint = {https://doi.org/10.13182/NSE03-14}
}

@inproceeding{OpenMC,
	author = {{Romano, Paul K.} and {Horelik, Nicholas E.} and {Herman, Bryan R.} and {Nelson, Adam G.} and {Forget, Benoit} and {Smith, Kord}},
	title = {OpenMC: A State-of-the-Art Monte Carlo Code for Research and Development},
	DOI= "10.1051/snamc/201406016",
	url= "https://doi.org/10.1051/snamc/201406016",
	booktitle = {SNA + MC 2013 - Joint International Conference on Supercomputing in Nuclear Applications + Monte Carlo},
	editor = {Array},
	year = 2014,
	pages = "06016",
}

@misc{OpenMC_CI,
  title = {{OpenMC continuous integration Travis server}},
  howpublished = {\url{https://travis-ci.org/openmc-dev/openmc}},
}

@misc{OpenMC_UT,
  title = {{OpenMC unit tests Github repository}},
  howpublished = {\url{https://github.com/openmc-dev/openmc/tree/develop/tests/unit_tests}},
}

@misc{OpenMC_regT,
  title = {{OpenMC regression tests repository}},
  howpublished = {\url{https://github.com/openmc-dev/openmc/tree/develop/tests/regression_tests}},
}

@misc{OpenMC_benchmark_suite,
  title = {{Massachusetts Institute of Technology, Computational Reactor Physics Group, Collection of models for reactor physics benchmarks}},
  howpublished = {\url{https://github.com/mit-crpg/benchmarks}},
}


@misc{Sinbad_benchmark_suite,
  title = {{Shielding Integral Benchmark Archive and Database (SINBAD)}},
  howpublished = {\url{https://inis.iaea.org/search/search.aspx?orig_q=RN:43000913}},
}

@misc{CSG2CSG,
  title = {{CSG2CSG}},
  howpublished = {\url{https://github.com/makeclean/csg2csg}},
}

@misc{openmc_workshop,
  title = {{OpenMC workshop}},
  howpublished = {\url{https://github.com/shimwell/openmc_workshop}},
}

@misc{dlopen,
  title = {{OpenMC DLopen pull request}},
  howpublished = {\url{https://github.com/openmc-dev/openmc/pull/1257}},
}


@misc{mcnp2cad,
  title = {{mcnp2cad}},
  howpublished = {\url{https://github.com/svalinn/mcnp2cad}},
}

@article{openmc_keff_analytical_benchmarks,
    title = "Analytical benchmark test set for criticality code verification",
    journal = "Progress in Nuclear Energy",
    volume = "42",
    number = "1",
    pages = "55 - 106",
    year = "2003",
    issn = "0149-1970",
    doi = "https://doi.org/10.1016/S0149-1970(02)00098-7",
    url = "http://www.sciencedirect.com/science/article/pii/S0149197002000987",
    author = "Avneet Sood and R.Arthur Forster and D. Kent Parsons",
    keywords = "analytic, benchmark, criticality, code verification",
    abstract = "A number of published numerical solutions to analytic eigenvalue (keff) and eigenfunction equations are summarized for the purpose of creating a criticality verification benchmark test set. The 75-problem test set allows the user to verify the correctness of a criticality code for infinite medium and simple geometries in one-, two-, three-, and six-energy groups, with one-, two-, and four-media. The problems include both isotropic and linearly and quadratically anisotropic neutron scattering. The problem specifications will produce both keff = 1 and the quoted k∞ to at least five decimal places. MCNP (Briesmeister, 1997) and DANTSYS (Alcouff, R.E, et al., 1995) have been verified using these problems. Additional uses of the test set for code verification are also discussed."
}



@article{openmc_vera_core_benchmarks,
    title = "Selected VERA Core Physics Benchmarks in OpenMC",
    journal = "Transactions of the American Nuclear Society",
    volume = "117",
    pages = "1520 - 1523",
    year = "2017",
    issn = "0149-1970",
    url = "https://stuff.mit.edu/~tjlaboss/files/ANS_2017_Winter_Meeting_Summary.pdf",
    author = "Travis J. Labossiere-Hickman and Benoit Forget†",
}

@article{openmc_burnup_benchmark,
    title = "Burnup dependent Monte Carlo neutron physics calculations of IAEA MTR benchmark",
    journal = "Progress in Nuclear Energy",
    volume = "81",
    pages = "43 - 52",
    year = "2015",
    issn = "0149-1970",
    doi = "https://doi.org/10.1016/j.pnucene.2014.12.018",
    url = "http://www.sciencedirect.com/science/article/pii/S0149197015000037",
    author = "Khurrum Saleem Chaudri and Sikander M. Mirza",
    keywords = "OpenMC code, Monte Carlo methods, MTR benchmark, Depletion studies",
    abstract = "In this work, OpenMC code has been used for reactor physics calculations of the IAEA 10 MW MTR benchmark. To perform the burnup dependent studies i.e. Beginning of Life (BOL) and End of Life (EOL) calculations are carried out using OpenMC. The isotopic number densities have been generated using WIMS code and comparison of global core parameters has been performed. Along with the prevalent 9-isotope vector methodology, a set of 16-isotopes, based on their relative importance, have been employed in the whole core calculations and the corresponding computed values of integral parameters been compared. Comparison of effective core multiplication factor is made with studies performed by various organizations, employing different codes based on diffusion theory and Monte Carlo methodologies. The OpenMC predicted values of the multiplication factor and cell averaged thermal fluxes in central flux trap for HEU and LEU cores are found in good agreement with the corresponding published data."
}


@article{openmc_beavrs_benchmark,
    title = "Analysis of select BEAVRS PWR benchmark cycle 1 results using MC21 and OpenMC",
    journal = "Proceedings of the International Conference on Physics of Reactors (PHYSOR 2014)",
    volume = "47",
    year = "2015",
    doi = "http://dx.doi.org/10.11484/jaea-conf-2014-003",
    url = "https://inis.iaea.org/search/search.aspx?orig_q=RN:47042909",
    author = {{Kelly Daniel J.} and {Aviles Brian N.} and {Romano Paul K.} and {Herman Bryan R.} and {Horelik Nicholas E.} and {Forget Benoit}},
}

@article{openmc_lwr_benchmark,
    title = "Analysis of tally correlation in large light water reactors",
    journal = "JAEA-Conf--2014-003",
    volume = "47",
    year = "2015",
    doi = "http://dx.doi.org/10.11484/jaea-conf-2014-003",
    url = "https://inis.iaea.org/search/search.aspx?orig_q=RN:47042909",
    author = {{Herman Bryan R.} and {Forget Benoit} and {Smith Kord} and {Romano Paul K.} and {Sutton Thomas M.} and Kelly Daniel J.} and {Aviles Brian N.}},
}

@article{openmc_beavrs2_benchmark,
    title = {Benchmark for evaluation and validation of reactor simulations (BEAVRS)},
    author = {Horelik, N. and Herman, B. and Forget, B. and Smith, K.},
    abstractNote = {Advances in parallel computing have made possible the development of high-fidelity tools for the design and analysis of nuclear reactor cores, and such tools require extensive verification and validation. This paper introduces BEAVRS, a new multi-cycle full-core Pressurized Water Reactor (PWR) depletion benchmark based on two operational cycles of a commercial nuclear power plant that provides a detailed description of fuel assemblies, burnable absorbers, in-core fission detectors, core loading patterns, and numerous in-vessel components. This benchmark enables analysts to develop extremely detailed reactor core models that can be used for testing and validation of coupled neutron transport, thermal-hydraulics, and fuel isotopic depletion. The benchmark also provides measured reactor data for Hot Zero Power (HZP) physics tests, boron letdown curves, and three-dimensional in-core flux maps from fifty-eight instrumented assemblies. Initial comparisons between calculations performed with MIT's OpenMC Monte Carlo neutron transport code and measured cycle 1 HZP test data are presented, and these results display an average deviation of approximately 100 pcm for the various critical configurations and control rod worth measurements. Computed HZP radial fission detector flux maps also agree reasonably well with the available measured data. All results indicate that this benchmark will be extremely useful in validation of coupled-physics codes and uncertainty quantification of in-core physics computational predictions. The detailed BEAVRS specification and its associated data package is hosted online at the MIT Computational Reactor Physics Group web site (http://crpg.mit.edu/), where future revisions and refinements to the benchmark specification will be made publicly available. (authors)},
    place = {United States},
    year = {2013},
    month = {7}
} 

@article{openmc_beavrs3_benchmark,
    title = {Validation of OpenMC Reactor Physics Simulations with the B and W 1810 Series Benchmark},
    author = {Jonathan A. Walsh and Benoit Forget and Kord S. Smith},
    journal = "Transactions of the American Nuclear Society",
    pages = "1301 - 1304",
    place = {United States},
    year = {2013}
} 

@article{isotopes_in_elelments,
    title = {Isotopic compositions of the elements 2013 (IUPAC Technical Report)},
    author = {Meija Juris and Coplen Tyler B. and Berglund Michael and Brand Willi A. and De Bievre, Paul and Groning Manfred and Holden Norman E. and Irrgeher Johanna and Loss Robert D. and Walczyk Thomas and Prohaska Thomas},
    journal = "Pure and Applied Chemistry",
    pages = "1301 - 1304",
    volume = "88",
    year = {2016},
    url = "http://pubs.er.usgs.gov/publication/70178124",
    doi = "https://doi.org/10.1515/pac-2015-0503",
} 

@article{atomic_mass_evaluation,
	doi = {10.1088/1674-1137/41/3/030003},
	url = {https://doi.org/10.1088%2F1674-1137%2F41%2F3%2F030003},
	year = 2017,
	month = {mar},
	publisher = {{IOP} Publishing},
	volume = {41},
	number = {3},
	pages = {030003},
	author = {Meng Wang and G. Audi and F. G. Kondev and W.J. Huang and S. Naimi and Xing Xu},
	title = {The {AME}2016 atomic mass evaluation ({II}). Tables, graphs and references},
	journal = {Chinese Physics C},
	abstract = {This paper is the second part of the new evaluation of atomic masses, AME2016. Using least-squares adjustments to all evaluated and accepted experimental data, described in Part I, we derive tables with numerical values and graphs to replace those given in AME2012. The first table lists the recommended atomic mass values and their uncertainties. It is followed by a table of the influences of data on primary nuclides, a table of various reaction and decay energies, and finally, a series of graphs of separation and decay energies. The last section of this paper lists all references of the input data used in the AME2016 and the NUBASE2016 evaluations (first paper in this issue). AMDC: http://amdc.impcas.ac.cn/ Contents The AME2016 atomic mass evaluation (II). Tables, graphs and referencesAcrobat PDF (293 KB) Table I. The 2016 Atomic mass tableAcrobat PDF (273 KB) Table II. Influences on primary nuclidesAcrobat PDF (160 KB) Table III. Nuclear-reaction and separation energiesAcrobat PDF (517 KB) Graphs of separation and decay energiesAcrobat PDF (589 KB) References used in the AME2016 and the NUBASE2016 evaluationsAcrobat PDF (722 KB) }
}

@article{Halton_sampling,
    author = {Halton, J. H.},
    title = {Algorithm 247: Radical-inverse Quasi-random Point Sequence},
    journal = {Commun. ACM},
    issue_date = {Dec. 1964},
    volume = {7},
    number = {12},
    month = dec,
    year = {1964},
    issn = {0001-0782},
    pages = {701--702},
    numpages = {2},
    url = {http://doi.acm.org/10.1145/355588.365104},
    doi = {10.1145/355588.365104},
    acmid = {365104},
    publisher = {ACM},
    address = {New York, NY, USA},
} 

@misc{lithium_lead_properties,
  title = {{P. Karditsas and M.J Baptiste Thermal Structural Properties of Fusion related Materials}},
  howpublished = {\url{http://aries.ucsd.edu/LIB/PROPS/PANOS/lipb.html}},
}

@misc{lithium_properties,
  title = {{P. Karditsas and M.J Baptiste Thermal and Structural Properties of Fusion related Materials}},
  howpublished = {\url{http://aries.ucsd.edu/LIB/PROPS/PANOS/li.html}},
}

@misc{flibe_properties,
  title = {{Y. Gohar, Transmutation of Transuranic Elements and Long Lived Fission Products in Fusion Devices}},
  howpublished = {\url{http://aries.ucsd.edu/LIB/MEETINGS/0103-TRANSMUT/gohar/Gohar-present.pdf}},
}

@article{Pearson_correlation,
    author = {Karl Pearson  and Francis Galton },
    title = {VII. Note on regression and inheritance in the case of two parents},
    journal = {Proceedings of the Royal Society of London},
    volume = {58},
    number = {347-352},
    pages = {240-242},
    year = {1895},
    doi = {10.1098/rspl.1895.0041}
    URL = {\url{https://royalsocietypublishing.org/doi/abs/10.1098/rspl.1895.0041}},
    eprint = {https://royalsocietypublishing.org/doi/pdf/10.1098/rspl.1895.0041},
        abstract = { Consider a population in which sexual selection and natural selection may or may not be taking place. Assume only that the deviations from the mean in the case of any organ of any generation follow exactly or closely the normal law of frequency, then the following expressions may be shown to give the law of inheritance of the population. }
}

@misc{spearman_correlation,
  title = {{J. Myers, A. Well, Research Design and Statistical Analysis (2nd ed.) Lawrence Erlbaum. p. 508. ISBN 978-0-8058-4037-7. 2003}},
  howpublished = {\url{http://aries.ucsd.edu/LIB/MEETINGS/0103-TRANSMUT/gohar/Gohar-present.pdf}},
}

@misc{lithium_enrichment,
    author       = {Giegerich, Th. and Day, Chr. and Knitter, R. and Osman, N.},
    year         = {2016},
    title        = {Lithium enrichment issues in the sustainable supply chain of future fusion reactors},
    howpublished = {Vortrag gehalten auf 1st IAEA Technical Meeting on the Safety Design and Technology of {\convertToLaTeXASCII{U+D}}{\convertToLaTeXASCII{U+A}}Fusion Power Plants, Wien, A, May 3-5, 2016},
    note         = {31.03.01; LK 01},
    language     = {english}
}

@Misc{freecad,
author = {J. Riegel and W. Mayer and Y. van Havre},
title =    {FreeCAD Version 0.17},
howpublished = {http://freecadweb.org/},
year = {2001--2018}
}

@Misc{paraview,
author = {J. Ahren and B. Geveci and C. Law},
title =    {ParaView: An End-User Tool for Large Data Visualization, Visualization Handbook},
howpublished = {Elsevier, 2005, ISBN-13: 978-0123875822 \url{https://www.paraview.org} }
}

@inproceeding{OpenMC,
	author = {{Romano, Paul K.} and {Horelik, Nicholas E.} and {Herman, Bryan R.} and {Nelson, Adam G.} and {Forget, Benoit} and {Smith, Kord}},
	title = {OpenMC: A State-of-the-Art Monte Carlo Code for Research and Development},
	DOI= "10.1051/snamc/201406016",
	url= "https://doi.org/10.1051/snamc/201406016",
	booktitle = {SNA + MC 2013 - Joint International Conference on Supercomputing in Nuclear Applications + Monte Carlo},
	editor = {Array},
	year = 2014,
	pages = "06016",
}

@article{dagmc,
title = {{Acceleration techniques for the direct use of CAD-based geometry in fusion neutronics analysis}},
journal = "Fusion Engineering and Design",
year = "2010",
pages = "1759-1765"
author = "P. Wilson and T. Tautgesb and J. Kraftcheck et al."
}

@article{Shimwell_2019,
	doi = {10.1088/1741-4326/ab0016},
	url = {https://doi.org/10.1088%2F1741-4326%2Fab0016},
	year = 2019,
	month = {mar},
	publisher = {{IOP} Publishing},
	volume = {59},
	number = {4},
	pages = {046019},
	author = {Jonathan Shimwell and R{\'{e}}mi Delaporte-Mathurin and Jean-Charles Jaboulay and Julien Aubert and Chris Richardson and Chris Bowman and Andrew Davis and Andrew Lahiff and James Bernardi and Sikander Yasin and Xiaoying Tang},
	title = {Multiphysics analysis with {CAD}-based parametric breeding blanket creation for rapid design iteration},
	journal = {Nuclear Fusion}}
}
