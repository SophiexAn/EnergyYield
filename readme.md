# Energy Yield Software

This software aims to simulate the energy yield of single-junction and multi-junction solar cells. In contrast to the power conversion efficiency (PCE), the energy yield (EY) accounts for environmental conditions, such as constantly changing irradiation conditions or the ambient temperature.

This software allows a rapid simulation of complex architectures and was developed with the aim to handle  textured perovskite-based multi-junction devices. However, it is possible to simulate any combination of thin-film architecture with incoherent photovoltaic materials (e.g., crystalline silicon).

By making use of pre-simulated textures (e.g., inverted pyramids, regular upright pyramids, random pyramids) by geometrical ray tracing, any incoherent interface within the architecture can also be textured. 

The software is available as source code and a simple to use graphical user interface (GUI), which requires either a Matlab installation or the Matlab runtime.

### Basic Features

The basic features of the energy yield software are:

* Spectral and angular-resolved realistic (1020 locations in the USA) irradiance data is used
* A simple cloud model is used to adjust the diffuse irradiation
* Fast optical simulations, combining the transfer matrix method and geometric ray tracing
* Optics can handle arbitrary combinations of thin (coherent) and thick (incoherent) layers, which also can be textured
* Single- and multi-junction solar cells can be simulated
* No limitation of number of absorbers
* Energy yield is computed for different electrical interconnection schemes (e.g. 2T, 3T, 4T)
* Energy yield can be derived for constant tilt (and constant rotation) angle
* Energy yield can be derived for various tracking algorithms (e.g. 1-axis, 2-axis)
* Bifacial solar cells solar cells can be simulated
* Albedo can be considered by choosing one out of 3400 spectra of natural and man-made materials from the [ECOSTRESS spectral library](https://speclib.jpl.nasa.gov/)

### Modular framework

The software is divided in individual modules, which handle the irradiation, optics, electrics and energy yield simulations. Those modules can also be operated independently (e.g. calculate the reflectance, transmittance, absorptance of a solar cell architecture).

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFIgXG5cdFRNWTNbTWV0ZXJvbG9naWNhbCBEYXRhIFRNWTNdIC0tPiBJcnJbSXJyYWRpYW5jZSBNb2R1bGVdIC0tPiBFWUNbRW5lcmd5IFlpZWxkIENvcmUgTW9kdWxlXSAtLT4gRVlbRW5lcmd5IFlpZWxkXVxuXHREW0RldmljZSBBcmNoaXRlY3R1cmVdIC0tPiBPW09wdGljcyBNb2R1bGVdIC0tPiBFWUNcblx0RVlDIC0tPiBFW0VsZWN0cmljcyBNb2R1bGVdXG5cdEUgLS0-IEVZQ1xuXHRFUFtFbGVjdHJpY2FsIFByb3BlcnRpZXNdIC0tPiBFIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggTFIgXG5cdFRNWTNbTWV0ZXJvbG9naWNhbCBEYXRhIFRNWTNdIC0tPiBJcnJbSXJyYWRpYW5jZSBNb2R1bGVdIC0tPiBFWUNbRW5lcmd5IFlpZWxkIENvcmUgTW9kdWxlXSAtLT4gRVlbRW5lcmd5IFlpZWxkXVxuXHREW0RldmljZSBBcmNoaXRlY3R1cmVdIC0tPiBPW09wdGljcyBNb2R1bGVdIC0tPiBFWUNcblx0RVlDIC0tPiBFW0VsZWN0cmljcyBNb2R1bGVdXG5cdEUgLS0-IEVZQ1xuXHRFUFtFbGVjdHJpY2FsIFByb3BlcnRpZXNdIC0tPiBFIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

* The [**Irradiation Module**](https://github.com/PerovskitePV/EnergyYield/wiki/Irradiance-Module) calculates the spectral and angular-resolved irradiance over the course of one year with a temporal resolution of one hour by applying [SMARTS](https://www.nrel.gov/grid/solar-resource/smarts-register.html) to typical meteorological year ([TMY3](https://nsrdb.nrel.gov/data-sets/archives.html)) data of locations in various climatic zones. A simple model is employed to account for cloud coverage such that realistic direct and diffuse irradiance are derived.
* The [**Optics Module**](https://github.com/PerovskitePV/EnergyYield/wiki/Optics-Module) rapidly calculates the spectrally and angular-resolved absorptance of the non-simplified architecture of multi-junction solar cells. It is able to handle a strong entanglement of multiple planar and textured interfaces with coherent and incoherent light propagation by combining transfer matrix method (TMM) and geometrical ray-tracing.
* The [**Electrical Module**](https://github.com/PerovskitePV/EnergyYield/wiki/Electrics-Module) determines the temperature-dependent current density-voltage (*J*-*V*) characteristics accounting for series and shunt resistances for a given short-circuit current density (*J*<sub>SC</sub>) of the sub-cells forming the multi-junction in either a 2T-, 3T- or 4T-configuration. Furthermore, the maximum power point is determined to calculate the power output of the multi-junction solar module.
* The [**Energy Yield Core Module**](https://github.com/PerovskitePV/EnergyYield/wiki/Energy-Yield-Module) calculates the EY over the course of one year of the sub-cells depending on their orientation (rotation and/or tilt of the module) and location. The EY is computed by combining the spectral and angular resolved solar irradiation (with or without albedo), the absorptance of the multi-junction solar cell and the electrical properties.

### Credits

This software project was initiated by **[Ulrich W. Paetzold](mailto:ulrich.paetzold@kit.edu?subject=[GitHub]%20Question%20on%20Energy%20Yield%20Software)**. The code development was driven by:

* **Jonathan Lehr** (electrics module, albedo)
* **Malte Langenhorst** (optics module, irradiance module)
* **Raphael Schmager** (energy yield core, irradiance module, optics module, electrics module, GUI)
* **Fabrizio Gota** (numerical modelling on 3T interconnection, optics module)

This software uses codes and data from other programmers and resources:

* Parts of the transfer matrix code is taken from [Steven Byrnes](https://github.com/sbyrnes321/)
* Matlab implementation of the [NREL solar position algorithm](https://doi.org/10.1016/j.solener.2003.12.003) by [Vincent Roy](https://de.mathworks.com/matlabcentral/fileexchange/5430-sun-azimuth-data) 
* Logarithmic Lambert W function from [Michael](https://www.mathworks.com/matlabcentral/fileexchange/57239-lambert-w-function-logarithmic-input)
* The [SMARTS](https://www.nrel.gov/grid/solar-resource/smarts-register.html) from Dr. Christian A. Gueymard [see also](https://www.solarconsultingservices.com/smarts.php)
* The [TMY3](https://nsrdb.nrel.gov/data-sets/archives.html) data from the National Solar Radiation Database
* [Reference Air Mass 1.5 Spectra](https://www.nrel.gov/grid/solar-resource/spectra-am1.5.html)
* [ECOSTRESS spectral library](https://speclib.jpl.nasa.gov/) for albedo

### Getting started

Download and extract the project. Open the `main.m`, which contains all definitions and settings to calculate the energy yield (EY) of a perovskite/c-Si multi-junction solar cell. In order to start your simulations, you need to get and add some external files, like the SAMRTS code or the TMY3 data. Please check out our [wiki page](https://github.com/PerovskitePV/EnergyYield/wiki) for some help. You'll find a detailed description of each of the modules as well as a [guide](https://github.com/PerovskitePV/EnergyYield/wiki/Setup) for setting up the required external files.   

### Contributing

If you want to contribute to this project and make it better, your help is very welcome! 

### Contact

For any questions regarding the software, please contact [Ulrich W. Paetzold](mailto:ulrich.paetzold@kit.edu?subject=[GitHub]%20Question%20on%20Energy%20Yield%20Software). See also [here](https://www.lti.kit.edu/mitarbeiter_7254.php).

### Citing

If you use our energy yield software or parts of it in the current or a modified version, please consider citing our publication on the methodology:

[R. Schmager and M Langenhorst et al., Opt. Express, 27, 2019](https://doi.org/10.1364/OE.27.00A507)

### Further reading

This energy yield software has been used in the following publications:

[Lehr et al., Optics Express, 2020](https://doi.org/10.1364/OE.404969)  
[F. Gota et al., Joule, 2020](https://doi.org/10.1016/j.joule.2020.08.021)  
[J. Lehr et al., Sol. Energy Mater. Sol. Cells., 2020](https://doi.org/10.1016/j.solmat.2019.110367)  
[R. Schmager and M Langenhorst et al., Opt. Express, 27, 2019](https://doi.org/10.1364/OE.27.00A507)  
[M. Langenhorst et al., Prog. Photovoltaics Res. Appl. 27, 2019](https://doi.org/10.1002/pip.3091)  
[J. Lehr and M. Langenhorst et al., Sustain. Energy Fuels., 2018](https://doi.org/10.1039/C8SE00465J)  
