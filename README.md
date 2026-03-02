# Learn ML - Python Data Science Learning Repository

## Overview
A comprehensive learning repository covering essential Python data science and machine learning concepts through practical examples and projects. This repository includes lessons on NumPy, Pandas, and data visualization techniques with real-world projects.

## Repository Structure

### 1. **NumPy/**
Fundamental numerical computing library fundamentals
- **Array.ipynb** - Introduction to NumPy arrays and basic operations
- **Array_IndexingandSlicing.ipynb** - Array indexing, slicing, and fancy indexing techniques
- **Array_Operations.ipynb** - Mathematical and logical operations on arrays
- **Topics Covered**: Arrays, dimensions, dtypes, reshaping, broadcasting, mathematical functions

### 2. **Pandas/**
Data manipulation and analysis with DataFrames and Series
- **Series.ipynb** - Pandas Series fundamentals (1D labeled arrays)
- **dataframe.ipynb** - DataFrame operations and manipulations (2D labeled data structures)
- **Operations.ipynb** - Basic arithmetic and logical operations on data
- **MissingData.ipynb** - Handling missing values and data cleaning
- **MergingJoiningconcatination.ipynb** - Combining multiple DataFrames
- **GroupByAggregation.ipynb** - Grouping data and aggregate functions
- **PivotTables.ipynb** - Creating pivot tables and cross-tabulations
- **Topics Covered**: Data selection, cleaning, transformation, aggregation, and reshaping

### 3. **Data Visualization/**
Creating meaningful visualizations with plotting libraries
- **Matplotlib.ipynb** - Matplotlib fundamentals for static visualizations
- **CategoricalPlot.ipynb** - Visualizations for categorical data
- **DistributionPlots.ipynb** - Distribution analysis and visualization
- **RegressionPlot.ipynb** - Regression visualization and trend analysis
- **MatrixPlot.ipynb** - Heatmaps and matrix visualizations
- **PlotlyandCufflinks.ipynb** - Interactive visualizations with Plotly
- **Topics Covered**: Line plots, bar charts, histograms, scatter plots, heatmaps, interactive charts

### 4. **DataVisualization_Project1-IPL/**
Real-world data visualization project analyzing Indian Premier League cricket data
- **IPL.ipynb** - Complete analysis notebook
- **IPL.csv** - Dataset with match information
- **Analysis Includes**:
  - Team performance metrics
  - Impact of toss on match outcomes
  - Player of the Match statistics
  - Top scorers and bowlers analysis
  - Venue-based statistics
- **Skills Applied**: Data cleaning, GroupBy operations, multiple visualization techniques

### 5. **Pandas_Project1/**
Data exploration and feature extraction project
- **FeatureExtraction.ipynb** - Feature engineering and extraction techniques
- **anime.csv** - Anime dataset with various attributes
- **Skills Applied**: Data filtering, sorting, feature creation, data aggregation

### 6. **Pandas_Project2/**
Geographic and economic data analysis project
- **Countries.ipynb** - Country-level data analysis
- **Countries.csv** - Dataset with country demographics and statistics
- **Skills Applied**: Data grouping, merging, statistical analysis

## Prerequisites

### System Requirements
- Python 3.x
- Jupyter Notebook or JupyterLab
- Windows/Mac/Linux

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/SagarBhadra01/learn-ml.git
   cd learn-ml
   ```

2. **Install Python packages**:
   ```bash
   pip install numpy pandas matplotlib seaborn jupyter plotly cufflinks
   ```

   Or using conda:
   ```bash
   conda install numpy pandas matplotlib seaborn jupyter plotly cufflinks
   ```

3. **Launch Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```

## Learning Path

**Recommended progression for beginners**:
1. Start with **NumPy/** to master array operations
2. Move to **Pandas/** to learn data manipulation
3. Progress to **Data Visualization/** to create insightful charts
4. Apply skills with **Projects** (IPL, Pandas_Project1, Pandas_Project2)

## Library Reference

| Library | Purpose | Notebooks |
|---------|---------|-----------|
| **NumPy** | Numerical computing | NumPy/ |
| **Pandas** | Data manipulation | Pandas/, Projects |
| **Matplotlib** | Static visualizations | Data Visualization/ |
| **Seaborn** | Statistical visualizations | Data Visualization/ |
| **Plotly** | Interactive visualizations | Data Visualization/PlotlyandCufflinks.ipynb |

## Key Concepts Covered

### Data Structures
- NumPy arrays (ndarrays)
- Pandas Series
- Pandas DataFrames

### Data Operations
- Indexing and slicing
- Filtering and selection
- Merging and concatenation
- GroupBy and aggregation
- Pivot tables

### Data Visualization
- Line plots and scatter plots
- Bar charts and histograms
- Heatmaps and matrix plots
- Categorical plots
- Distribution plots
- Interactive charts

### Data Cleaning
- Handling missing values
- Data type conversion
- Removing duplicates
- Outlier detection

## Project Details

### IPL Project
Analysis of Indian Premier League cricket matches with 10+ visualizations covering team performance, player statistics, and venue analysis.

### Country Data Analysis
Exploration of country-level statistics with data merging, grouping, and comparative analysis.

### Anime Dataset Analysis
Feature extraction and exploration of anime characteristics and ratings.

## Using the Notebooks

1. **Open a notebook**:
   ```bash
   jupyter notebook NumPy/Array.ipynb
   ```

2. **Run cells sequentially** (Shift + Enter) to see outputs

3. **Modify and experiment** with code cells to deepen understanding

4. **Read markdown cells** for explanations and concepts

## Tips for Learning

- Run each notebook cell-by-cell and observe outputs
- Modify examples and see how outputs change
- Use Python comments to document your understanding
- Practice with your own datasets
- Review multiple notebooks to see different approaches

## Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| `ModuleNotFoundError` | Install missing package using `pip install <package>` |
| CSV file not found | Ensure CSV is in the same directory as notebook |
| Warnings in output | Already suppressed in notebooks; safe to ignore |
| Jupyter not starting | Run `pip install jupyter` then `jupyter notebook` |

## Future Enhancements

- Machine Learning algorithms and implementations
- Statistical hypothesis testing
- Time series analysis
- Natural Language Processing (NLP)
- Deep Learning with TensorFlow/PyTorch
- Advanced data visualization dashboards

## Resources

### Official Documentation
- [NumPy Documentation](https://numpy.org/doc/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [Seaborn Documentation](https://seaborn.pydata.org/)
- [Plotly Documentation](https://plotly.com/python/)

### Learning Resources
- Data manipulation concepts in Pandas notebooks
- Visualization best practices in Data Visualization notebooks
- Real-world application examples in project notebooks

## License
Open source - Feel free to use and modify for educational purposes

## Author
Created as a comprehensive learning resource for Python data science fundamentals

## Contributing
Improvements, bug fixes, and additional examples are welcome!

---

**Happy Learning!** Start with NumPy basics and progressively build your data science skills through practical projects.
