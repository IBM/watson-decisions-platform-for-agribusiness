# IBM Weather Operations Center

Weather and other geospatial data impacts every business, every day. Minimizing the disruption that it can cause requires more than just gathering data — you must employ advanced analytics and intelligent workflows to reimagine processes and better predict how the environment will impact your assets, employees and customers. Fair or foul, when weather strikes, The IBM Weather Operations Center is a suite of applications that provides insight so you can plan for and respond to changing conditions to ensure business continuity.

This github repository contains documentation and API usage examples that can be referenced when interacting with IBM Weather Operations Center.

## Overview Docs

* [Product Page](https://www.ibm.com/products/weather-operations-center)
* [Guide](https://www.ibm.com/downloads/cas/PA6JERGA)
* [Blog](https://www.ibm.com/blogs/internet-of-things/ibm-weather-operations-center/)

## Landing Page

* [weatheroperationscenter.ibm.com](https://weatheroperationscenter.ibm.com)

## API usage examples and Scripts

### Maximo Asset Import

* [Importing Maximo Locations into Weather Operations Center](./maximo-integration-asset-import.md)

### Geospatial Analytics

#### API Authentication

* [How to generate and use access tokens](./geospatial-api.md#authentication)

#### Custom Geospatial Queries

* [Performing Custom Geospatial Queries, Registration and Visualization](./custom-geospatial-query-extension.md)

### Agriculture Add-on Specific Examples and Samples
* [How to generate auth tokens](./api-tokens.md)
* [How admin users can create fields on behalf of regular users](./admin-creating-fields.md)
* [How admin users can upload customer field data to IBM Cloud Object Storage](./admin-upload-files-to-cos.md)
* [Sample Data Query for HDSM/T layer](./sample-queries/hdsmt.md)
* [Generate polygons](./../scripts/generatePolygon.py) - more info at [scripts readme doc](./../scripts/README.md)
* [Access Jupyter Notebooks to Interact with the Watson Decision Platform Layers](./notebooks/notebooks.md)
