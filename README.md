# Calcium Imaging Analysis Pipeline

## Overview

This Python pipeline analyzes calcium imaging data from fluorescence microscopy experiments. It processes CSV files containing calcium traces, detects peaks in neural activity, performs statistical analyses, and generates comprehensive visualizations and reports.

The pipeline is specifically designed to analyze "Measurement 1" data from two types of experiments:
- **RNA Interference experiments** (siRNA/saRNA treatments)
- **Chemical treatment experiments** (various pharmacological compounds)

## Key Features

### 1. Peak Detection Algorithm
- Uses prominence-based peak detection with specific parameters:
  - Prominence threshold: > 0.2
  - Minimum peak separation: 5 frames
  - Minimum peak width: 1 frame
- Cells are classified as "active" if they exhibit ≥ 2 peaks

### 2. Data Processing
- Calculates ΔF/F (change in fluorescence over baseline)
- Removes outliers using z-score method (threshold = 3.0)
- Extracts multiple kinetic parameters:
  - Number of peaks
  - Peak amplitude
  - Slope of calcium trace
  - Full Width at Half Maximum (FWHM)

### 3. Statistical Analysis
- Normality testing using Shapiro-Wilk test
- Appropriate statistical tests based on data distribution:
  - Normal data: Independent t-test
  - Non-normal data: Mann-Whitney U test
- Effect size calculation (Cohen's d)
- Multiple comparison corrections

### 4. Visualization Outputs
- **Violin plots** with individual data points for kinetic parameters
- **Activity bar charts** showing percentage of active cells per condition
- **Individual calcium traces** with marked peaks (PDF format)
- **Summary reports** with comprehensive statistics

## Input Requirements

### File Structure
- CSV files with calcium imaging data
- First column: Frame numbers
- Subsequent columns: ROI (Region of Interest) intensity values

### Naming Conventions
#### RNA Experiments
- Must contain "Meas1" in filename
- Condition identifiers: "Scr" (control), "siRNA", "saRNA"

#### Chemical Experiments
- Must contain "1001" in filename
- Condition identifiers: "WT", "Nav", "PTZ", "Vera"

## Output Structure

```
CalciumImaging_Measurement1_Results_[timestamp]/
├── RNA_Interference/
│   ├── Figures/
│   │   ├── analysis_measurement1.png/pdf
│   │   └── activity_measurement1.png/pdf
│   ├── Statistics/
│   │   └── measurement_1_stats.txt
│   ├── Data/
│   │   ├── measurement1_data.csv
│   │   └── file_parsing_log_measurement1.csv
│   └── Calcium_Traces/
│       └── [Condition folders with trace PDFs]
└── Chemical_Treatments/
    └── [Same structure as RNA_Interference]
```

## Dependencies

```python
- pandas
- numpy
- matplotlib
- seaborn
- scipy
```

## Usage

1. Update the file paths in the script:
```python
rna_path = r'path/to/RNA/data'
chem_path = r'path/to/chemical/data'
```

2. Run the script:
```python
python calcium_imaging_analysis.py
```

## Analysis Workflow

1. **File Discovery**: Recursively searches directories for CSV files
2. **File Parsing**: Extracts condition and measurement information from filenames
3. **Kinetic Analysis**: Processes each ROI to detect peaks and calculate parameters
4. **Quality Control**: Removes outliers using z-score method
5. **Statistical Testing**: Compares all conditions to control
6. **Visualization**: Generates plots and trace PDFs
7. **Reporting**: Creates comprehensive statistical reports

## Key Functions

### Core Analysis
- `calculate_kinetics_peaks()`: Detects peaks and calculates kinetic parameters
- `remove_outliers_zscore()`: Removes statistical outliers
- `parse_filename()`: Extracts experimental metadata from filenames

### Statistical Analysis
- `perform_statistical_analysis()`: Comprehensive statistical testing
- `generate_stats_report()`: Creates detailed statistical reports

### Visualization
- `create_analysis_plots()`: Generates violin plots for kinetic parameters
- `create_activity_plot()`: Creates bar charts for cell activity
- `plot_calcium_traces()`: Generates PDFs of individual calcium traces

### Pipeline Control
- `analyze_experiment_measurement1()`: Main analysis pipeline
- `collect_measurement1_data()`: Data collection and organization

## Output Interpretation

### Activity Classification
- **Active cells**: ≥ 2 detected peaks
- **Inactive cells**: < 2 detected peaks

### Statistical Significance
- `*`: p < 0.05
- `**`: p < 0.01
- `***`: p < 0.001
- `ns`: not significant

### Effect Size (Cohen's d)
- Small: |d| < 0.5
- Medium: 0.5 ≤ |d| < 0.8
- Large: |d| ≥ 0.8

## Customization

### Modifying Peak Detection Parameters
```python
peaks, properties = find_peaks(dff, prominence=0.2, distance=5, width=1)
```

### Changing Outlier Threshold
```python
df_clean = remove_outliers_zscore(df, metric, threshold=3.0)
```

### Adding New Conditions
Update the condition mappings in the analysis functions:
```python
condition_order = ['Control', 'Treatment1', 'Treatment2']
color_map = {'Control': '#1f77b4', 'Treatment1': '#ff7f0e'}
```

## Notes

- The pipeline only analyzes "Measurement 1" files to ensure consistency
- Dose-response files (containing µM, µL markers) are automatically excluded
- All outputs include both PNG and PDF formats for publication flexibility
- Statistical tests are automatically selected based on data distribution

## Citation

If you use this pipeline in your research, please cite:
[Your citation information here]

## License

[Your license information here]

## Contact

[Your contact information here]
