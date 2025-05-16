# Calcium-imaging-analysis

## Overview

This toolkit consists of two main scripts:

### Script 1: TIF Frame Extraction

This script extracts the first frames from TIF files, allowing for the analysis of initial frames using Stardist to select Regions of Interest (ROIs). It is designed to prevent computer crashes by processing only the first frames.

### Script 2: Peak Detection

This script is designed for peak detection and analysis within .txt files. It consists of two main cells:

#### Cell 1: Single File Analysis

Analyzes peaks per individual .txt file and provides detailed peak-related statistics.

Calcium Imaging Data Analysis
Overview
This repository contains a comprehensive Python script for analyzing calcium imaging data with robust statistical annotations. The script processes CSV files containing calcium imaging results, calculates kinetic parameters, performs statistical analysis, and generates publication-quality visualizations.
Features

Automated Calcium Transient Detection: Identifies calcium transients using peak detection algorithms
Comprehensive Kinetic Analysis: Calculates key metrics including:

Number of peaks
Signal amplitude
Signal slope
Full width at half maximum (FWHM)


Robust Statistical Analysis:

Normality testing with Shapiro-Wilk
Non-parametric Kruskal-Wallis test for multi-group comparisons
Pairwise comparisons using Mann-Whitney U test
Automatic significance annotation


Intelligent Outlier Handling: Removes outliers using interquartile range (IQR) method
Professional Visualization:

Violin plots with overlaid group means
Sample size annotations
Integrated statistical results


Flexible Data Organization:

Parses experimental conditions from filenames
Processes multiple measurements and replicates
Supports multiple experimental conditions



Requirements

Python 3.7+
Dependencies:

pandas
numpy
matplotlib
seaborn
scipy



Installation
bash# Clone the repository
git clone https://github.com/joepvondervoort/calcium-imaging-analysis.git
cd calcium-imaging-analysis

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy
Usage

Organize your calcium imaging CSV files in a folder
Run the script:
bashpython calcium_imaging_analysis.py

When prompted, enter:

The path to your CSV files folder
The desired output folder path for results



Expected File Naming Convention
The script expects CSV files to follow this naming pattern:
YYYYMMDD_Condition[Replicate].Measurement.Results.csv
Where:

YYYYMMDD: Date in format (e.g., 20230101)
Condition: Experimental condition (e.g., WT, Nav, PTZ, Vera)
Replicate: Optional replicate number
Measurement: Measurement number

Example: 20230101_WT1.1.Results.csv
Output
The script generates:

Violin plots for each metric and measurement (.png format)
Statistical analysis summary for each metric (.txt format)

Example
Show Image
Customization
The script can be modified to accommodate different experimental setups:

Adjust peak detection parameters in the calculate_kinetics_peaks function
Modify the condition list in the plot_data function
Change statistical tests or thresholds in the statistical_analysis function

