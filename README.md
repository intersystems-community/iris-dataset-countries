## iris-dataset-countries
This repository contains a class and data of countries in a Global

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

## How to Test it

In IRIS terminal:

```
$ docker-compose exec iris iris session iris
USER>D $System.SQL.Shell()
[SQL]USER>>Select * from dc_data.Country
...
165     ZAF     South Africa    Africa  Southern Africa 1221037 1910    40377000        51.1    116729   129092  South Africa    Republic        Thabo Mbeki     716     ZA
166     ZMB     Zambia  Africa  Eastern Africa  752618  1964    9169000 37.2    3377    3922    Zambia   Republic        Frederick Chiluba       3162    ZM
167     ZWE     Zimbabwe        Africa  Eastern Africa  390757  1980    11669000        37.8    5951     8670    Zimbabwe        Republic        Robert G. Mugabe        4068    ZW

167 Rows(s) Affected
statement prepare time(s)/globals/cmds/disk: 0.2921s/57002/303650/0ms
          execute time(s)/globals/cmds/disk: 0.0490s/168/37878/0ms
                          cached query class: %sqlcq.USER.cls6
---------------------------------------------------------------------------
[SQL]USER>>

## In InterSystems SQL Tools in VSCode
Open repo in VSCode (see develoment above)
Install [InterSystems SQLTools](https://marketplace.visualstudio.com/items?itemName=intersystems-community.sqltools-intersystems-driver)

Use the connection "iris-dataset-country"

Open dc_data.Country table and see the records:


## How to start coding
This repository is ready to code in VSCode with ObjectScript plugin.
Install [VSCode](https://code.visualstudio.com/), [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) and [ObjectScript](https://marketplace.visualstudio.com/items?itemName=daimor.vscode-objectscript) plugin and open the folder in VSCode.
Open /src/cls/PackageSample/ObjectScript.cls class and try to make changes - it will be compiled in running IRIS docker container.
![docker_compose](https://user-images.githubusercontent.com/2781759/76656929-0f2e5700-6547-11ea-9cc9-486a5641c51d.gif)

Feel free to delete PackageSample folder and place your ObjectScript classes in a form
/src/Package/Classname.cls
[Read more about folder setup for InterSystems ObjectScript](https://community.intersystems.com/post/simplified-objectscript-source-folder-structure-package-manager)

The script in Installer.cls will import everything you place under /src into IRIS.

