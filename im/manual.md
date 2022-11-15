---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# User Manual for IM Tool

This is a shock impedance matching calculator for impact of one material onto 1 to 3 layers of target materials.

The tool includes the ability to plot data from the online Shock Wave Database at http://www.ihed.ras.ru/rusbank/ ({cite}`Levashov2004`). 


## Quick Start
Run the IM Tool:
* As a web app on Heroku (response can be a little slow): <a href="https://impedance-match-app.herokuapp.com/" target="_blank">impedance-match-app.herokuapp.com</a>

* From the Jupyter Book page {ref}`IM_Tool`: Launch CoLab; run the notebook

* On your local computer: <a href="https://github.com/ImpactsWiki/impact-tools-book" target="_blank">Download the repo</a> and run the Jupyter Notebook locally

Select 2, 3, or 4 materials.<br>
Enter impact velocity (hit return or the up/down arrows).<br>
Changing the impact velocity activates a new plot.<br>

## Add New Materials
Add materials on-the-fly in the paramter entry panel.

Alternatively, when running the Jupyter notebook, you can replace the materials-data.csv file with your own database.

(more manual coming soon.....)

## Built-in Functions
The IM_module contains several functions to plot and fit Hugoniot data.

(more manual coming soon.....)

## Equations

The equations used in the impedance matching tool:

(more manual coming soon.....)
