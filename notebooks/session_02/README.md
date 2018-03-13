# Applied Data Analytics - Data and Databases

<!-- TOC -->

# Data and Databases

## How it works:

- 1) First, use the `data_and_databases-01-Database_clients.ipynb` notebook to survey your options for running SQL in the ADRF, and choose one (when in doubt, use pgAdmin) and get it connected.
- 2) work through `data_and_databases-02-Intro_to_SQL.ipynb`, trying out the exercises as you go.
- 2) as you work, check for answers to problems and exercises in the `data_and_databases-03-exercise_answers.ipynb`

## Learning Objectives:

- **Basic understanding of SQL.**  Includes learning basic SQL syntax, and then common SQL needed to answer questions about data that require querying a single table and joining multiple tables together.
- **Understand options for using SQL to analyze data stored in a relational database.** Survey of using an SQL client, running SQL queries via Python, including aggregation queries and spatial analysis with PostGIS, and then different ways you can use SQL to aggregate and pull data into environments where you can work with it, including python in general (jupyter, or any script), pandas, and R, and why you might want to use each of these options.
- **Chance to play with SQL.** Use SQL statements (including JOINS) executed using Python to answer questions about the class data.

## Topics:

- Databases and Python - connecting to a database, using and closing a connection.
- SQL basics - SELECT, WHERE, ORDER BY, JOIN, GROUP BY and aggregate functions.
- PostGIS queries
- Addendum - More advanced code samples:

    - Listing tables and columns
    - Modifying the database with INSERT and UPDATE.

## Directory Contents

- README.md - this file, an introduction and setup guide for the Data and Databases workbooks.
- requirements.txt - list of Python packages used in the Data and Database notebooks.  These can be installed together using conda or pip (if you use Anaconda, install with conda whenever you can, then fall back to install with pip only if you have to).  To do this, in a command shell, go to the module directory, then:

    - for conda: `conda install --file requirements.txt`
    - for pip: `pip install -r requirements.txt`

- archive folder: Holds full copies of some old versions of these files.
- images folder: Holds images that are used in notebooks in this module.
- ipython notebooks:

    - `data_and_databases-01-Database_clients.ipynb`
    - `data_and_databases-02-Intro_to_SQL.ipynb`
    - `data_and_databases-03-exercise_answers.ipynb`


## Setup

### Required Python packages

The packages used in this module are listed below, and they are also in the file `requirements.txt`, located in the same directory as this file.  They should already be installed in your Python environment.

When a package can be installed with `conda` or `pip`, it is a good idea to install with `conda` since Continuum, the makers of Anaconda, do considerable work to pre-compile and make sure the packages they provide work no matter your system configuration.

The following packages can be installed with either `conda` or `pip`:

- psycopg2
- sqlalchemy
- pandas