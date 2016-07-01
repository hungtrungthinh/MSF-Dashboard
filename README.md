MSF-Dashboard v1.0.0
====================

A lightweight and modular data visualization micro-website that can be offlined and adapted to various data-feeds.

Currently in pre-release: [get last release!](https://github.com/MSF-UK/MSF-Dashboard/releases)

Want to contribute to MSF-Dashboard? Please read `CONTRIBUTING.md`.

Example / Templates
-------------------

Here are gathered some use-cases of the MSF-Dashboard and 'online - demo versions' which can help you understand whether it is what you need or not. In the fortunate case it is the solution you need, they can be a good start to help you generate and customize your own MSF-Dashboard.

|Description                                           |Links                                                 |
|------------------------------------------------------|------------------------------------------------------|
|**Outbreak: MSF Lubumbashi Mission** - since December 2015 - offline, data parsed via tsv|[online-demo](http://msf-uk.github.io/MSF-Dashboard/ver_demos/cfg_msf-lubumbashi) / [download]()|
|**Surveillance: MSF Katanga ERU** - since January 2016 - offline, data parsed via excel-spreadsheets|[online-demo](http://msf-uk.github.io/MSF-Dashboard/ver_demos/cfg_eru-katanga/) / [download]()|
|**Surveillance: SRE MOH Tonkolili DHMT** - since April 2016 - offline, data parsed via dedicated datamanager|[online-demo](http://msf-uk.github.io/MSF-Dashboard/ver_demos/cfg_dhmt-tonkolili/) / [download]()|
|**Surveillance: MSF Sud-Kivu ERU** - since June 2016 - offline, data parsed via excel-spreadsheets|[online-demo](http://msf-uk.github.io/MSF-Dashboard/ver_demos/cfg_eru-sudkivu/) / [download]()|
|More to come...| |


Installation and Usage
----------------------

MSF Dashboard can be deployed in a variety of contexts. It is a micro-website which, in its 'essential' version, does not require more than a web browser (Firefox or equivalent or Chrome or equivalent, IE is support is not guaranteed at the moment). It is run offline thanks to nwjs which includes a node instance and allow usage of more advanced file manipulation.

The technical side of a MSF-Dashboard deployment is generally a 4-steps process:
- 1) Workout parsing and formatting data workflow 
- 2) Configuring the MSF-Dashboard
- 3) Deploy the MSF-Dashboard
- 4) Support the end-users

The main constraints for installation are the connexion with data source and specific needs that might not be available yet (get in touch [here](https://github.com/MSF-UK/MSF-Dashboard/issues)). 

The setup that are currently supported and have been tested include:
- Offline implementation with nwjs micro-server (data parsed via excel-spreadsheets, csv, tsv, dedicated datamanager).
- Online implementation without backend (data parsed via json/csv/text file directly uploaded to the website).
- Online implementation with external backend (data parsed via various APIs...).
 
Ready to try? You can start with the ERU versions, here is one page guide -> [X](https://github.com/MSF-UK/MSF-Dashboard/blob/master/cfg_eru-sudkivu/doc-dev/eru_dashboard-deployement_onepage.pdf)


Customize the Dashboard: Get started!
-------------------------------------

The general idea is that the Dashboard relies on:
+ source files: */src_core/* which are both third-party librairies (in */src_core/lib/*) and librairies developped for this MSF-Dashboard (other files in */src_core/*). These files should not be changed for a 'simple' customization (change layout, text and reuse existing charts and functions).
+ configuration files: */cfg_[name-your-custom-version-here]/* which are 3: *index.html* for the layout, *lang/lang.js* for the texts and their translation and *dev/dev-defined.js* to describe the data and the charts + the data files (geojson, population and medical data).

To get started, you can consult the Example / Template section or the implementation examples of different charts (available soon):
+ [Bar Chart](http://braimbault.github.io/NA)
+ [Multi Map](http://braimbault.github.io/NA)


General Architecture
--------------------

```
index.html                                - Defines the layout of the dashboard (charts position and 
|                                           identifiers). 
|                                           @see: Bootstrap grid system: http://getbootstrap.com/css/#grid.  
|
└─ js/main-getlibs.js                     - Loads third-party ibrairies and dashboard sources.
   |                                        @see: Folders are defined in 'index.html'.
   |
   ├─ dev/dev-defined.js                  - Parameters to get and check medical and geometry data, define
   |                                        charts and maps.
   |                                        @see: All the defined parameters are global and members of 'module:g'.
   |
   ├─ lang/module-lang.js                 - Stores texts visible to the end user in available languages.
   |                                        @see: 'module:module_lang'
   |
   ├- js/module-chartwarper.js            - [Optional] Warp charts/containers under tabs.
   |                                        @see 'module:module_chartwarper'
   |
   └─ js/main-getdata.js                  - Loads datafiles.
      |                                     @see: 'module:module_getdata'
      |
      └── js/main-loadfiles.js            - Combines functions of: requesting data from sources, reading
          |                                 and formatting data, connecting with other components.
          |                                 @see: 'module:main_loadfiles'
          |
          ├── js/module-datacheck.js      - Medical data quality check and processing (runs through all
          |                                 the medical records).
          |                                 @see: 'module:module_datacheck'
          |
          └── js/main-core.js             - Central component: setup and pulls the data in the charts and   
              |                             maps. Define the interactions. Connects with other components.
              |                             @see 'module:main_core'
              |
              ├── js/module-interface.js  - A lateral menu and exta functionalities buttons for charts/maps. 
              |   |                         @see 'module:module_interface'
              |   |          
              |   └-- js/module-intro.js  - [Optional] intro.js to access quick interactive help: setup.
              |                             @see 'module:module_intro'
              |
              ├-- js/module-datatable.js  - [Optional] datatables.js to display data: setup, display and 
              |                             interactions.
              |                             @see 'module:module_datatable'
              |
              ├-- js/module-multiadm.js   - [Optional] Maps warper (tabs) and 'Goto' dropdown lists: setup, 
              |                             display and interactions.
              |                             @see 'module:module_multiadm'
              |
              └-- js/module-colorscale.js - [Optional] Provide functions to deal with maps colorscale  
                                            (automatic adaptation, diffrent computing methods - geostats.js -
                                            or color tones...).
                                            @see 'module:module_colorscale'          
    
```

For More Information
--------------------

+ Documentation is available at [Use MSF-Dashboard](https://MSF-UK.github.io/MSF-Dashboard_doc).
+ Report issues or ask for help  at [Issues MSF-Dashboard](https://github.com/MSF-UK/MSF-Dashboard/issues).
+ Track last changes [Releases history MSF-Dashboard](https://github.com/MSF-UK/MSF-Dashboard/releases).

License
-------

MSF-Dashboard is copyright (c) 2015-present, [Contributors to MSF-Dashboard](https://github.com/MSF-UK/MSF-Dashboard/graphs/contributors) for MSF.

MSF-Dashboard is free software, licensed under the MIT License. See the file `LICENSE.md` in this distribution for more details on the license and see `LICENSES-DEP.md` to know more about the dependencies.
