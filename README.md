## iris-dataset-countries
This repository contains a class and data of countries. The data is represented by [countries.csv](https://github.com/intersystems-community/iris-dataset-countries/blob/master/data/countries.csv)


## Motivation

Even it's relatively easy to import csv file in IRIS there could be errors.
This project helps to install with one ZPM command, that will create and compile a class and imports the data.

## Sources and Licenses

The [countries](https://github.com/intersystems-community/iris-dataset-countries/blob/master/data/countries.csv) datataset is taken from [the repo](https://github.com/google/dspl/blob/master/samples/google/canonical/countries.csv)
It is licensed under the [BSD 3-Clause "New" or "Revised" License](https://github.com/google/dspl/blob/master/LICENSE)

All other files of the repository are licensed under [MIT License](https://github.com/intersystems-community/iris-dataset-countries/blob/304f9d57e53cc3e8de1147974ef2a96c31f24888/LICENSE)


## Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.

## Installation 

zpm "install dataset-countries"

## Development

Clone/git pull the repo into any local directory

```
$ git clone https://github.com/intersystems-community/objectscript-docker-template.git
```

Open the terminal in this directory and run:

```
$ docker-compose up -d
```

If you want to change csv and update the class along with the data in the global uncomment the following lines in iris.script:
```
//zpm "install csvgen"
//d ##class(community.csvgen).GenerateFromURL("https://raw.githubusercontent.com/google/dspl/master/samples/google/canonical/countries.csv",",","dc.data.Country")
```
and comment the zpm module import line:
```
zpm "load /opt/irisbuild/ -v":1:1
```

csvgen will generate a new class and import the data. 
you can export the class manually (right-click/Export in Server code view) - make sure then to move the generated file to a proper place in the directory (replace the previous dc/data/Country.cls)
 and export globals with the following line:
```
d $System.OBJ.Export("dc.data.CountryD.GBL","/irisrun/repo/data/dc.data.CountryD.xml")
```

Comment csvgen and GenerateFromURL lines and uncomment the zpm line and rebuild the image to test (see below)whether the new data is in place with the package. If yes - well done, you've updated the package successfully!

## How to Test it

In IRIS terminal:

```
$ docker-compose exec iris iris session iris
USER>D $System.SQL.Shell()
[SQL]USER>>Select * from dc_data.Country
...
241     YE      15.5527 48.5164 Yemen
242     YT      -12.8275        45.1662 Mayotte
243     ZA      -30.5595        22.9375 South Africa
244     ZM      -13.1339        27.8493 Zambia
245     ZW      -19.0154        29.1549 Zimbabwe

245 Rows(s) Affected
statement prepare time(s)/globals/cmds/disk: 0.0913s/40,537/191,996/0ms
          execute time(s)/globals/cmds/disk: 0.0133s/246/24,849/0ms
                          cached query class: %sqlcq.USER.cls8
---------------------------------------------------------------------------
[SQL]USER>>
```

## In InterSystems SQL Tools in VSCode
Open repo in VSCode (see develoment above)
Install [InterSystems SQLTools](https://marketplace.visualstudio.com/items?itemName=intersystems-community.sqltools-intersystems-driver)

Use the connection "iris-dataset-country"

Open dc_data.Country table and see the records:
<img width="1078" alt="Screenshot 2021-01-24 at 16 26 41" src="https://user-images.githubusercontent.com/2781759/105631746-0abe1480-5e61-11eb-8265-734a02b68aef.png">


## How to start coding
This repository is ready to code in VSCode with ObjectScript plugin.
Install [VSCode](https://code.visualstudio.com/), [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) and [ObjectScript](https://marketplace.visualstudio.com/items?itemName=daimor.vscode-objectscript) plugin and open the folder in VSCode.
Open /src/cls/PackageSample/ObjectScript.cls class and try to make changes - it will be compiled in running IRIS docker container.
![docker_compose](https://user-images.githubusercontent.com/2781759/76656929-0f2e5700-6547-11ea-9cc9-486a5641c51d.gif)

Feel free to delete PackageSample folder and place your ObjectScript classes in a form
/src/Package/Classname.cls
[Read more about folder setup for InterSystems ObjectScript](https://community.intersystems.com/post/simplified-objectscript-source-folder-structure-package-manager)

The script in Installer.cls will import everything you place under /src into IRIS.

