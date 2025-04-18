
Our [Run Models CoLab](input/industries) provides Logistic Regression, Support Vector Machines (SVM), MLP, RandomForest, XGBoost 

Our main input is currently industry features by county for exploring environmental impact targets.  
We are also creating [CoLabs for Exiobase International Trade Flow](/OpenFootprint/trade).


[Run-Models-bkup.ipynb](https://github.com/ModelEarth/RealityStream/tree/main/models) is a backup of the [Run Models CoLab](https://colab.research.google.com/drive/1zu0WcCiIJ5X3iN1Hd1KSW4dGn0JuodB8?usp=sharing) that we run locally. We append "-bkup" to indicate it is not the primary source.

## Run Models CoLab

- [Run Models (CoLab)](input/industries) - For features and targets merged on their location columns.
- [Models Overview](models)

In Run Models, the "features" dataset is merged with a 2-column "targets" dataset on-the-fly using either .csv files or Pandas to avoid storing merged .csv files. The location column joins features and targets.

Location column data types:  
World Region (TBD), Country (2-char), State (2-char), County Fips (5-digits for state and county), Zip (5 char, 6 in China), or Brain Voxel (2 char)

## Default Data Sources

Our features-targets merge supports any data with a location column containing multiple locations.  
Our default data will always use County Fips so features and targets align.

**Industries (Features and Targets)** - County Fips
<a href="input/industries/">Industries Input Data</a>

**Bees (Target)** - County Fips
<a href="input/bees/">Random Forest (Bees)</a>

**Trees (Target)** - County Fips
[Tree Targets](input/trees/)

**Blinks** - Location is brain voxel columns - multiple locations have one target column
<a href="models/random-bits-forest/">Random Bits Forest (Blinks)</a><br>


You can add paths to external data by editing a copy of the [parameters.yaml](https://github.com/ModelEarth/RealityStream/blob/main/parameters/parameters.yaml) file.


## Path Parameters

The term "features" is more prevalent in machine learning and data science.
"factors" has a stronger association with statistics and social sciences. The term factors is used for impact attributes like emissions.

TO DO: Add a python command that loads parameters.yaml to run [Run-Models-bkup.ipynb](https://github.com/ModelEarth/RealityStream/tree/main/models) locally, so the user does not need to open a notebook. Pass a parameters.yaml path in. 

Parameters are loaded from the parameters.yaml file:

	python Run-Models-bkup.ipynb [raw path to parameters.yaml]

Some paths - only the first one is ready to use:  
[parameters-simple.yaml](https://raw.githubusercontent.com/ModelEarth/RealityStream/main/parameters/parameters-simple.yaml) - TO DO: Test this simple version and modify CoLab if needed (no years, just Maine)
[parameters.yaml](https://raw.githubusercontent.com/ModelEarth/RealityStream/main/parameters/parameters.yaml) - Predicts bee population growth by industry  
[parameters-years.yaml](https://raw.githubusercontent.com/ModelEarth/RealityStream/main/parameters/parameters-years.yaml) - For testing with multiple years and states (currently same as parameters.yaml)
[parameters-zip.yaml](https://raw.githubusercontent.com/ModelEarth/RealityStream/main/parameters/parameters-zip.yaml) - Needs zip code target  
[parameters-blinks.yaml](https://raw.githubusercontent.com/ModelEarth/RealityStream/main/parameters/parameters-blinks.yaml) - TO DO: Update CoLab for targets with no features.

Example of parameters.yaml format:

	folder: naics6-bees-counties
	features: industries
		startyear: 2017
		endyear: 2021
	 	path: https://raw.githubusercontent.com/ModelEarth/community-timelines/main/training/naics{naics}/US/counties/{year}/US-{state}-training-naics{naics}-counties-{year}.csv
	targets: bees
		path: https://github.com/ModelEarth/RealityStream/raw/main/input/bees/targets/bees-targets.csv
	models: lr, svc, rfc, rbf, xgboost

<!-- For later
	python Run-Models-bkup.ipynb [features] [target] [models]
-->

Each target dataset will contain 2 columns.  
1. The location column with one of the following column names:  
Country (2-char), State (2-char), Fips (5-digits for state and county), Zip (5 char, 6 in China), or Voxel (2 char)
2. The "Target" column containing 1 or 0

### About setting the model in parameters.yaml

Setting the models parameter to "all" would be the equivalent to "lr,rfc,rbf,svm,mlp,xgboost"  

### About path name shortcuts in parameters.yaml

Default features and targets datasets reside in the "input/[data]/features" and "input/[data]/targets" folders for each data source.

The simplest form of the parameters.yaml would be:

	features: industries
	targets: bees

That's the equivalent to:

	features: industries
	 	path: https://github.com/ModelEarth/RealityStream/raw/main/input/industries/features/industries-features.csv
	targets: bees
		path: https://github.com/ModelEarth/RealityStream/raw/main/input/bees/targets/bees-targets.csv
	models: rbf


The features.path and targets.path will have several shorthand versions and a full version from GitHub:

**short** - bees  
**medium** - input/bees/targets  
**long** - input/bees/targets/bees-targets.csv  
**full** - https://github.com/ModelEarth/RealityStream/raw/main/input/bees/targets/bees-targets.csv



**Path processing rules:**
If there's no slash / in a path parameter, start from the root of the RealityStream repo.
If the file extension is omitted from a path, append .csv.
For a target value of "bees" build the path "input/bees/targets/bees-targets.csv"
Replace a space with -targets- in the path.
So for a target value of "bees increase2024" build the path "input/bees/targets/bees-targets-increase2024.csv"

## Projects

Replace TO DO with your name as you work on a project.  
Write Loren when you've submitted a pull request to show your name.  
Update related .ipynb and app.py file to also add your name.

1. TO DO: Generate features-importance reports for available models.
2. TO DO: Load industries-features.ipynb colab output into Run Models using parameters.yaml.
3. TO DO: Find a comparison process or pull accuracy reports (from Ivy's yaml or json files) into one tabulator table for viewing. See our [tabulator sample page](../../data-pipeline/timelines/tabulator/) for merging within javascript.
4. TO DO: Reuse report display process for other models.
5. TO DO: Automate updating "toy" feature data using Github Actions.

## Project Workflow Development Plan

Beyond the machine learning Colab notebook, our goal is to build a complete workflow for this project, featuring a JavaScript user interface for the frontend, a backend service (potentially Flask) to execute the script, and the Colab notebook itself.

**Project Structure**
1. Frontend (JavaScript): A web-based interface that allows users to trigger actions and interact with the workflow.
2. Backend (Flask or similar): A service to process requests from the frontend and execute the Colab notebook's logic.
3. Colab Notebook: A machine learning notebook hosted in Google Colab or converted into an executable Python script for integration.


