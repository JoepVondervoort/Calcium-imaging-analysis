# Calcium-imaging-analysis

## Overview

Welcome to the Image Analysis Toolkit, a collection of Python Jupyter Notebook scripts for various image analysis tasks. This toolkit consists of two main scripts:

### Script 1: TIF Frame Extraction

This script extracts the first frames from TIF files, allowing for the analysis of initial frames using Stardist to select Regions of Interest (ROIs). It is designed to prevent computer crashes by processing only the first frames.

### Script 2: Peak Detection

This script is designed for peak detection and analysis within .txt files. It consists of two main cells:

#### Cell 1: Single File Analysis

Analyzes peaks per individual .txt file and provides detailed peak-related statistics.

#### Cell 2: Batch Analysis

Analyzes all .txt files in a specified folder and creates a summary Excel file containing the following information:

- Total peaks detected
- Active cells (cells with at least 2 peaks)
- Total peaks in active cells
- Average peaks per active cell
- Percentage of active cells
- Total cells
- Source file

Peak detection is performed using a formula based on SciPy.

## Getting Started

Follow these steps to get started with the Image Analysis Toolkit:

1. Clone this repository to your local machine.
2. Ensure you have Python and Jupyter Notebook installed on your system.
3. Install the required Python libraries as listed in the `requirements.txt` file.
4. Run the Jupyter Notebook scripts, providing the necessary input parameters.
5. Explore the generated results and summary Excel files for peak analysis.

For detailed usage instructions, refer to the Jupyter Notebook documentation within the respective scripts.

## Dependencies

- Python 3.x
- Jupyter Notebook

