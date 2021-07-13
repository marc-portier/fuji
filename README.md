# F-UJI (FAIRsFAIR Research Data Object Assessment Service)
Developers: [Anusuriya Devaraju](mailto:anusuriya.devaraju@googlemail.com), [Robert Huber](mailto:rhuber@marum.de)

## Overview
F-UJI is a web service to programatically assess FAIRness of research data objects based on [metrics](https://doi.org/10.5281/zenodo.3775793) developed by the [FAIRsFAIR](https://www.fairsfair.eu/) project. 
The service will be applied to demostrate the evaluation of objects in repositories selected for in-depth collaboration with the project.  

### Clients and User Interface

A web demo using F-UJI is available at https://www.f-uji.net

An R client package that was generated from the F-UJI OpenAPI definition is available from https://github.com/NFDI4Chem/rfuji.

## Assessment Scope, Constraint and Limitation
The service is **in development** and its assessment depends on several factors. 
- In the FAIR ecosystem, FAIR assessment must go beyond the object itself. FAIR enabling services and repositories are vital to ensure that research data objects remain FAIR over time. Importantly, machine-readable services (e.g., registries) and documents (e.g., policies) are required to enable automated tests. 
- In addition to repository and services requirements, automated testing depends on clear machine assessable criteria. Some aspects (rich, plurality, accurate, relevant) specified in FAIR principles still require human mediation and interpretation. 
- The tests must focus on generally applicable data/metadata characteristics until domain/community-driven criteria have been agreed (e.g., appropriate schemas and required elements for usage/access control, etc.). For example, for some of the metrics (i.e., on I and R principles), the automated tests we proposed only inspect the ‘surface’ of criteria to be evaluated. Therefore, tests are designed in consideration of generic cross-domain metadata standards such as dublin core, dcat, datacite, schema.org, etc.
- FAIR assessment is performed based on aggregated metadata; this includes metadata embedded in the data (landing) page, metadata retrieved from a PID provider (e.g., Datacite content negotiation) and other services (e.g., re3data).

![alt text](https://github.com/pangaea-data-publisher/fuji/blob/master/fuji_server/static/main.png?raw=true)

## Requirements
Python 3.5.2+

In order to deal with 308 redirects, the following patch has to be applied on urrlib:
https://github.com/python/cpython/pull/19588/commits

The service was generated by the [swagger-codegen](https://github.com/swagger-api/swagger-codegen) project. By using the
[OpenAPI-Spec](https://github.com/swagger-api/swagger-core/wiki) from a remote server, you can easily generate a server stub.  
The service uses the [Connexion](https://github.com/zalando/connexion) library on top of Flask.

## Usage
Before running the service, please set user details in the config file, see config/server.ini.

To install F-UJI, you may execute the following python-based or docker-based installation commands from the root directory:

#### Python module-based installation:
```
pip3 install -r requirements.txt
python3 -m fuji_server -c <path_to_server.ini>
```

#### Docker-based installation:
```
docker build -t <tag_name> .
docker run -d -p 1071:1071 <tag_name>
```

To access the Swagger  user interface, open the url below on the browser:

```
http://localhost:1071/fuji/api/v1/ui/
```

Your Swagger definition lives here:

```
http://localhost:1071/uji/api/v1/swagger.json
```


#### Notes

To avoid tika startup warning message, set environment variable TIKA_LOG_PATH. For more information, see [https://github.com/chrismattmann/tika-python](https://github.com/chrismattmann/tika-python)

If you receive the exception 'urllib2.URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] on MacOS, run the install command shipped with Python :
./Install\ Certificates.command


## License
This project is licensed under the MIT License; for more details, see the [LICENSE](https://github.com/pangaea-data-publisher/fuji/blob/master/LICENSE) file.
