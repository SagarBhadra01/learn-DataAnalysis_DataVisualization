<div align="center">

# <span style="color:#0A2FA8">Data Visualization</span>


</div>



## <span style="color:#1565C0">1. Introduction to Data Visualization</span>

> **Definition:** Data Visualization is the graphical representation of information and data using visual elements like charts, graphs, and plots to make patterns, trends, and insights easier to understand.

### <span style="color:#2E86AB">Why Visualize Data?</span>

| Reason | Description |
|:---|:---|
| Pattern Recognition | Spot trends and anomalies quickly |
| Communication | Convey complex insights simply |
| Exploration | Understand data distributions and relationships |
| Decision Making | Support data-driven conclusions |

### <span style="color:#2E86AB">Core Python Libraries</span>

| Library | Purpose |
|:---:|:---|
| `matplotlib` | Low-level, full-control plotting |
| `seaborn` | High-level statistical visualization built on Matplotlib |
| `plotly` | Interactive, web-ready charts |
| `numpy` | Numerical arrays - backbone of plot data |
| `pandas` | DataFrames - the data source |

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## <span style="color:#1565C0">2. Matplotlib - The Foundation</span>

> **Definition:** Matplotlib is Python's foundational plotting library that provides complete control over every element of a figure - from axis ticks to colors, line styles, and layout.

### <span style="color:#2E86AB">2.1 The Figure and Axes Model</span>

Matplotlib operates in two layers:

```
Figure (the whole canvas)
  └── Axes (individual plot area with x-axis, y-axis, title)
```

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">fig, ax = plt.subplots(nrows, ncols, figsize=(w, h))</span>

</div>

```python
fig, ax = plt.subplots(figsize=(10, 5))
ax.plot(x, y)
ax.set_title("My Plot")
ax.set_xlabel("X-axis")
ax.set_ylabel("Y-axis")
plt.show()
```

### <span style="color:#2E86AB">2.2 Two Ways to Plot</span>

#### <span style="color:#5B8DB8">Functional (pyplot) Style</span>

Simple, quick - best for single plots:

```python
plt.plot(x, y)
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Title")
plt.grid()
plt.show()
```

#### <span style="color:#5B8DB8">Object-Oriented (OO) Style</span>

Explicit, powerful - best for complex multi-plot layouts:

```python
fig = plt.figure(dpi=100)
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])  # [left, bottom, width, height]
ax.plot(x, y)
ax.set_title("Title")
plt.show()
```

> **Definition:** `add_axes([left, bottom, width, height])` places an axes at exact proportional coordinates within the figure canvas (values from 0 to 1).

### <span style="color:#2E86AB">2.3 Subplots</span>

Subplots create a grid of multiple plots in a single figure.

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">plt.subplot(nrows, ncols, index)</span>

</div>

```python
x  = np.array([1, 2, 3, 4, 5])
y1 = np.array([2, 3, 5, 7, 11])
y2 = np.array([1, 4, 9, 16, 25])

plt.subplot(1, 2, 1)   # row=1, col=2, position=1
plt.plot(x, y1)
plt.title("Line Plot 1")

plt.subplot(1, 2, 2)   # row=1, col=2, position=2
plt.plot(x, y2)
plt.title("Line Plot 2")

plt.tight_layout()
plt.show()
```

Nested axes example - plot inside plot:

```python
fig = plt.figure(dpi=100)
ax1 = fig.add_axes([0.1, 0.1, 0.8, 0.8])   # outer big plot
ax2 = fig.add_axes([0.2, 0.3, 0.4, 0.5])   # inner smaller inset plot
ax1.plot(x, y1)
ax2.plot(x, y2)
plt.show()
```

---

## <span style="color:#1565C0">3. Matplotlib - Plot Types</span>

### <span style="color:#2E86AB">3.1 Line Plot</span>

Best for continuous data, time series, mathematical functions.

```python
plt.plot(x, y)
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Line Plot Example")
plt.grid()
plt.show()
```

### <span style="color:#2E86AB">3.2 Scatter Plot</span>

Best for showing relationships between two continuous variables.

```python
plt.scatter(x, y1, color='red', label='y1')
plt.scatter(x, y2, color='blue', label='y2')
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Scatter Plot Example")
plt.legend()
plt.show()
```

### <span style="color:#2E86AB">3.3 Histogram</span>

> **Definition:** A Histogram shows the frequency distribution of a single continuous variable by dividing data into bins and counting occurrences.

```python
data = np.random.randn(1000)
plt.hist(data, bins=30, color='blue', edgecolor='black')
plt.title("Histogram Example")
plt.show()
```

| Parameter | Purpose |
|:---:|:---|
| `bins` | Number of bars (intervals) |
| `color` | Fill color of bars |
| `edgecolor` | Border color of bars |

### <span style="color:#2E86AB">3.4 Box Plot</span>

> **Definition:** A Box Plot (Box-and-Whisker) shows the five-number summary - minimum, Q1, median, Q3, maximum - and highlights outliers.

```python
data = np.random.randn(100)
plt.boxplot(data)
plt.title("Box Plot Example")
plt.show()
```

```
Box Plot Anatomy:

  |---[ Q1 |  Median  | Q3 ]---|
  min                         max
  Points beyond whiskers = Outliers
```

### <span style="color:#2E86AB">3.5 Saving Plots</span>

```python
fig = plt.figure(dpi=100)
fig.add_axes([0.1, 0.1, 0.8, 0.8])
plt.plot(x, y)
plt.title("My Plot")
plt.savefig("my_plot.png")   # Save as PNG
plt.savefig("my_plot.pdf")   # Save as PDF
```

### <span style="color:#2E86AB">3.6 Working with Images</span>

```python
import matplotlib.image as mpimg

img = mpimg.imread("line_plot.png")   # Load image
imgplot = plt.imshow(img)             # Display image
plt.axis("off")                       # Hide axes
plt.show()
```

---

## <span style="color:#1565C0">4. Matplotlib - Styling and Design</span>

### <span style="color:#2E86AB">4.1 Line Styles and Widths</span>

| `linestyle` | Symbol | Appearance |
|:---:|:---:|:---|
| Solid | `'-'` | Continuous line |
| Dashed | `'--'` | Regular dashes |
| Dash-dot | `'-.'` | Dash then dot |
| Dotted | `':'` | Dotted line |

| `linewidth` | Result |
|:---:|:---|
| `0.25` | Very thin |
| `0.50` | Thin |
| `1.00` | Normal |
| `2.00` | Thick |

```python
fig, ax = plt.subplots(figsize=(10, 4))
xaxis = np.arange(0, 10, 0.8)

# Line widths
ax.plot(xaxis, xaxis+1, color="red", linewidth=0.25)
ax.plot(xaxis, xaxis+2, color="red", linewidth=0.50)
ax.plot(xaxis, xaxis+3, color="red", linewidth=1.00)
ax.plot(xaxis, xaxis+4, color="red", linewidth=2.00)

# Line styles
ax.plot(xaxis, xaxis+5, color="green", lw=3, linestyle='-')
ax.plot(xaxis, xaxis+6, color="green", lw=3, ls='-.')
ax.plot(xaxis, xaxis+7, color="green", lw=3, ls=':')
```

### <span style="color:#2E86AB">4.2 Custom Dashes</span>

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">line.set_dashes([line_len, space_len, line_len, space_len, ...])</span>

</div>

```python
line, = ax.plot(xaxis, xaxis+8, color="black", lw=1.50)
line.set_dashes([5, 50, 15, 50])   # [dash, gap, dash, gap]
```

### <span style="color:#2E86AB">4.3 Markers</span>

| Marker Symbol | Shape |
|:---:|:---|
| `'+'` | Plus sign |
| `'o'` | Circle |
| `'*'` | Star |
| `'s'` | Square |
| `'.'` | Point |
| `'1'` | Tri-down |
| `'2'` | Tri-up |

```python
ax.plot(xaxis, xaxis+9,  color="blue", lw=3, ls='-',  marker='+')
ax.plot(xaxis, xaxis+10, color="blue", lw=3, ls='--', marker='o')
ax.plot(xaxis, xaxis+11, color="blue", lw=3, ls='-',  marker='s')

# Marker with custom size and color
ax.plot(xaxis, xaxis+15, color="purple", lw=1, ls='-',
        marker='o', markersize=8, markerfacecolor="red")

# Marker with edge styling
ax.plot(xaxis, xaxis+16, color="purple", lw=1, ls='-',
        marker='s', markersize=8,
        markerfacecolor="yellow",
        markeredgewidth=3,
        markeredgecolor="green")
```

| Parameter | Purpose |
|:---:|:---|
| `markersize` | Size of the marker |
| `markerfacecolor` | Fill color of marker |
| `markeredgecolor` | Border color of marker |
| `markeredgewidth` | Thickness of marker border |

---

## <span style="color:#1565C0">5. Seaborn - Statistical Visualization</span>

> **Definition:** Seaborn is a high-level data visualization library built on top of Matplotlib that provides beautiful default styles and a simple interface for creating complex statistical plots.

### <span style="color:#2E86AB">5.1 Setup and Datasets</span>

```python
import seaborn as sns

# Load built-in practice datasets
df  = sns.load_dataset("tips")       # Restaurant tips data
flights = sns.load_dataset("flights") # Monthly airline passengers
```

The `tips` dataset columns: `total_bill`, `tip`, `sex`, `smoker`, `day`, `time`, `size`

### <span style="color:#2E86AB">5.2 Common Parameters Across Seaborn Plots</span>

| Parameter | Purpose |
|:---:|:---|
| `data` | The DataFrame |
| `x` | Column for x-axis |
| `y` | Column for y-axis |
| `hue` | Separate colors by a categorical variable |
| `palette` | Color scheme (`Set1`, `coolwarm`, `rainbow`, etc.) |
| `ax` | Matplotlib axes object to draw on |

---

## <span style="color:#1565C0">6. Distribution Plots</span>

> **Definition:** Distribution Plots show how a variable's values are spread across its range - revealing shape, central tendency, and spread.

### <span style="color:#2E86AB">6.1 Histogram / Distribution Plot - `displot` / `histplot`</span>

```python
# displot - figure-level
sns.displot(df['total_bill'], kde=True, bins=30)

# histplot - axes-level (preferred in modern Seaborn)
sns.histplot(df['total_bill'], kde=True, bins=30)
```

| Parameter | Purpose |
|:---:|:---|
| `kde=True` | Overlay Kernel Density Estimate curve |
| `bins` | Number of histogram bars |

#### <span style="color:#5B8DB8">Side-by-Side Histograms with Subplots</span>

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.histplot(df['total_bill'], kde=True, bins=30, ax=axes[0])
axes[0].set_title("Distribution of Total Bill")

sns.histplot(df['tip'], kde=True, bins=30, ax=axes[1])
axes[1].set_title("Distribution of Tips")

plt.tight_layout()
plt.show()
```

### <span style="color:#2E86AB">6.2 Joint Plot - `jointplot`</span>

> **Definition:** A Joint Plot shows the relationship between two variables with their individual distributions on the margins.

```python
sns.jointplot(x='total_bill', y='tip', data=df, kind='scatter')
```

| `kind` value | Description |
|:---:|:---|
| `'scatter'` | Scatter in center, histograms on margin |
| `'kde'` | KDE density in center, KDE on margin |
| `'reg'` | Scatter + regression line |
| `'hex'` | Hexbin density map |

```python
sns.jointplot(x='total_bill', y='tip', data=df, kind='kde')
sns.jointplot(x='total_bill', y='tip', data=df, kind='reg')
sns.jointplot(x='total_bill', y='tip', data=df, kind='hex')
```

### <span style="color:#2E86AB">6.3 Pair Plot - `pairplot`</span>

> **Definition:** A Pair Plot creates a grid of scatter plots for every pair of numeric columns, with univariate distributions on the diagonal.

```python
sns.pairplot(df)                                  # Basic pairplot
sns.pairplot(df, hue='sex')                       # Color by sex
sns.pairplot(df, hue='size', palette='rainbow')   # Color by size
```

```
Pairplot Grid:
  col1 vs col1 → histogram/KDE (diagonal)
  col1 vs col2 → scatter plot
  col2 vs col1 → scatter plot (mirrored)
  ...and so on for all numeric columns
```

### <span style="color:#2E86AB">6.4 Rug Plot - `rugplot`</span>

> **Definition:** A Rug Plot places small tick marks along the axes to show the actual data point positions - useful for visualizing density of observations.

```python
sns.rugplot(x='total_bill', y='tip', data=df)
```

---

## <span style="color:#1565C0">7. Categorical Plots</span>

> **Definition:** Categorical Plots visualize the relationship between a categorical variable (like day, sex, smoker) and a numeric variable (like tip, total_bill).

### <span style="color:#2E86AB">7.1 Count Plot - `countplot`</span>

> **Definition:** A Count Plot shows the count (frequency) of each category - essentially a bar chart of category occurrences.

```python
sns.countplot(x="day", data=df)
sns.countplot(x="sex", data=df, hue="smoker")
```

### <span style="color:#2E86AB">7.2 Bar Plot - `barplot`</span>

> **Definition:** A Bar Plot shows the mean (or other aggregate) of a numeric variable for each category, with error bars representing the confidence interval.

```python
sns.barplot(x="sex", y="total_bill", data=df)

sns.barplot(x="sex", y="total_bill", data=df,
            hue="smoker",
            palette="Set1",
            ci=None)          # ci=None hides confidence interval bars
```

| Parameter | Purpose |
|:---:|:---|
| `ci` | Confidence interval size; `None` to hide |
| `estimator` | Aggregate function (default: `mean`) |
| `palette` | Color scheme |

### <span style="color:#2E86AB">7.3 Box Plot - `boxplot`</span>

> **Definition:** A Seaborn Box Plot visualizes the distribution of a numeric variable across categories, showing median, quartiles, and outliers.

```python
sns.boxplot(x="tip", y="day", data=df)
```

```
Box anatomy:
  Whisker ---|---[ Q1 | Median | Q3 ]---|--- Whisker
             Outliers shown as individual dots
```

### <span style="color:#2E86AB">7.4 Violin Plot - `violinplot`</span>

> **Definition:** A Violin Plot combines a Box Plot with a KDE, showing the full distribution shape of data for each category.

```python
sns.violinplot(x="tip", y="day", data=df)
```

The wider the violin at any point, the more data concentrated there.

### <span style="color:#2E86AB">7.5 Strip Plot - `stripplot`</span>

> **Definition:** A Strip Plot shows individual data points along a categorical axis - a one-dimensional scatter plot per category.

```python
sns.stripplot(x="tip", y="day", data=df, jitter=True)
```

> **`jitter=True`** adds a small random horizontal offset so overlapping points are visible.

### <span style="color:#2E86AB">7.6 Swarm Plot - `swarmplot`</span>

> **Definition:** A Swarm Plot is a non-overlapping version of the Strip Plot - points are arranged so they don't overlap, giving a better view of the true distribution.

```python
sns.swarmplot(x="tip", y="day", data=df)
```

| Plot | Shows Individual Points | Avoids Overlap | Shows Distribution Shape |
|:---:|:---:|:---:|:---:|
| Strip Plot | <span style="color:#27AE60">Yes</span> | <span style="color:#C0392B">No</span> | <span style="color:#C0392B">No</span> |
| Swarm Plot | <span style="color:#27AE60">Yes</span> | <span style="color:#27AE60">Yes</span> | <span style="color:#27AE60">Yes</span> |

### <span style="color:#2E86AB">7.7 Combining Categorical Plots</span>

Plots can be layered on top of each other for richer insight:

```python
# Violin shows distribution, swarm shows actual points
sns.violinplot(x="tip", y="day", data=df)
sns.swarmplot(x="tip",  y="day", data=df, color="black", size=3)
```

---

## <span style="color:#1565C0">8. Regression Plots</span>

> **Definition:** Regression Plots visualize the linear relationship between two continuous variables, automatically fitting and displaying a regression line with a confidence interval band.

### <span style="color:#2E86AB">8.1 lmplot - Linear Model Plot</span>

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">sns.lmplot(x, y, data, hue, col, row)</span>

</div>

```python
# Basic regression plot
sns.lmplot(x="total_bill", y="tip", data=tips)

# With hue - separate regression line per group
sns.lmplot(x="total_bill", y="tip", data=tips, hue="sex")
```

The shaded region around the line is the **95% confidence interval** - the uncertainty band of the regression estimate.

```
lmplot output:
  Scatter points → actual data
  Line           → fitted regression line (y = mx + b)
  Shaded band    → 95% confidence interval
```

| Parameter | Purpose |
|:---:|:---|
| `hue` | Separate regression line by category |
| `col` | Create column-wise facet grid by category |
| `row` | Create row-wise facet grid by category |
| `scatter=False` | Show only regression line, no points |
| `ci` | Confidence interval level (default 95) |

---

## <span style="color:#1565C0">9. Matrix Plots</span>

> **Definition:** Matrix Plots visualize 2D data tables as color-encoded grids, making it easy to spot correlations and patterns in tabular data.

### <span style="color:#2E86AB">9.1 Correlation Matrix</span>

> **Definition:** A Correlation Matrix is a table showing the Pearson correlation coefficient between every pair of numeric variables. Values range from -1 to +1.

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">r = +1 → perfect positive | r = 0 → none | r = -1 → perfect negative</span>

</div>

```python
tips_corr = tips[["total_bill", "tip", "size"]].corr()
print(tips_corr)
```

### <span style="color:#2E86AB">9.2 Heatmap - `heatmap`</span>

```python
sns.heatmap(tips_corr, annot=True, cmap="coolwarm")
```

| Parameter | Purpose |
|:---:|:---|
| `annot=True` | Print correlation values inside each cell |
| `cmap` | Color map (`coolwarm`, `viridis`, `Blues`, etc.) |
| `fmt` | Number format for annotations (e.g., `'.2f'`) |
| `linewidths` | Width of lines separating cells |
| `vmin`, `vmax` | Set the color scale range |

### <span style="color:#2E86AB">9.3 Pivot Table for Heatmap</span>

A pivot table reshapes data from long to wide format for matrix plotting:

```python
# Reshape flights data: rows = months, columns = years, values = passengers
pvt_flights = flights.pivot_table(index="month", columns="year", values="passengers")

sns.heatmap(pvt_flights, cmap="coolwarm")
```

```
Pivot Table flow:
  long format (month, year, passengers) → wide matrix (month × year grid)
```

### <span style="color:#2E86AB">9.4 Cluster Map - `clustermap`</span>

> **Definition:** A Cluster Map is a Heatmap with hierarchical clustering - it reorders rows and columns so that similar ones are grouped together, revealed by the dendrograms on the sides.

```python
sns.clustermap(tips_corr, annot=True, cmap="coolwarm")
```

| Feature | Heatmap | Clustermap |
|:---:|:---:|:---:|
| Color grid | <span style="color:#27AE60">Yes</span> | <span style="color:#27AE60">Yes</span> |
| Annotations | <span style="color:#27AE60">Optional</span> | <span style="color:#27AE60">Optional</span> |
| Dendrogram | <span style="color:#C0392B">No</span> | <span style="color:#27AE60">Yes</span> |
| Reordered rows/cols | <span style="color:#C0392B">No</span> | <span style="color:#27AE60">Yes</span> |

---

## <span style="color:#1565C0">10. Plotly - Interactive Visualization</span>

> **Definition:** Plotly is a library for creating interactive, web-ready charts that support zooming, panning, tooltips, and animation - all rendered in the browser.

### <span style="color:#2E86AB">10.1 Setup</span>

```bash
pip install plotly
pip install cufflinks
```

```python
import plotly.express as px
import plotly.offline as py
from plotly.offline import iplot
import cufflinks as cf

cf.go_offline()   # Enable offline mode for Jupyter
```

### <span style="color:#2E86AB">10.2 Plotly Express - Quick Charts</span>

Plotly Express is the high-level Plotly API - one-liners for most charts:

```python
# Line chart
fig = px.line(tips, y='total_bill')
fig.show()

# Bar chart
fig = px.bar(tips, x='day', y='total_bill', color='sex')
fig.show()

# Scatter plot
fig = px.scatter(tips, x='total_bill', y='tip', color='sex', size='size')
fig.show()

# Histogram
fig = px.histogram(tips, x='total_bill', nbins=30)
fig.show()

# Box plot
fig = px.box(tips, x='day', y='total_bill', color='smoker')
fig.show()
```

### <span style="color:#2E86AB">10.3 Cufflinks - Pandas + Plotly</span>

Cufflinks bridges pandas DataFrames directly to interactive Plotly charts via `.iplot()`:

```python
cf.go_offline()

# Line chart from grouped data
tips.groupby('day')['tip'].mean().iplot(kind='bar')
```

| `kind` value | Chart Type |
|:---:|:---|
| `'line'` | Line chart |
| `'bar'` | Bar chart |
| `'scatter'` | Scatter plot |
| `'histogram'` | Histogram |
| `'box'` | Box plot |
| `'heatmap'` | Heatmap |

> **Note:** Cufflinks is no longer actively maintained. Prefer `plotly.express` for new projects.

### <span style="color:#2E86AB">10.4 Plotly vs Matplotlib/Seaborn</span>

| Feature | Matplotlib / Seaborn | Plotly |
|:---|:---:|:---:|
| Static images | <span style="color:#27AE60">Yes</span> | <span style="color:#27AE60">Yes</span> |
| Interactive tooltips | <span style="color:#C0392B">No</span> | <span style="color:#27AE60">Yes</span> |
| Zoom / Pan | <span style="color:#C0392B">No</span> | <span style="color:#27AE60">Yes</span> |
| Animations | <span style="color:#C0392B">No</span> | <span style="color:#27AE60">Yes</span> |
| Publication quality | <span style="color:#27AE60">Yes</span> | Moderate |
| Learning curve | Low | Medium |

---

## <span style="color:#1565C0">11. Seaborn Color Palettes</span>

### <span style="color:#2E86AB">Common Palettes</span>

| Palette | Best Use |
|:---:|:---|
| `'Set1'`, `'Set2'`, `'Set3'` | Categorical / qualitative data |
| `'coolwarm'` | Diverging data (correlation maps) |
| `'viridis'` | Sequential, perceptually uniform |
| `'Blues'`, `'Reds'` | Single-hue sequential |
| `'rainbow'` | Multi-category hue distinction |
| `'pastel'` | Soft colors for publications |
| `'dark'` | Dark tones for contrast |

```python
sns.set_palette("Set2")
sns.barplot(x="sex", y="total_bill", data=df, palette="coolwarm")
```

---

## <span style="color:#1565C0">12. Seaborn Themes and Styles</span>

### <span style="color:#2E86AB">Figure Styles</span>

```python
sns.set_style("whitegrid")    # White background with grid lines
sns.set_style("darkgrid")     # Dark background with grid (default)
sns.set_style("white")        # Clean white, no grid
sns.set_style("dark")         # Dark background, no grid
sns.set_style("ticks")        # Minimal with axis ticks only
```

### <span style="color:#2E86AB">Context / Scale</span>

```python
sns.set_context("paper")      # Smallest - for journal papers
sns.set_context("notebook")   # Default - for Jupyter
sns.set_context("talk")       # Larger - for presentations
sns.set_context("poster")     # Largest - for posters
```

---

## <span style="color:#1565C0">13. Complete Plot Reference</span>

### <span style="color:#2E86AB">Matplotlib Plots Summary</span>

| Plot | Function | Use Case |
|:---|:---:|:---|
| Line Plot | `plt.plot()` | Trends over continuous x |
| Scatter Plot | `plt.scatter()` | Relationship between two variables |
| Histogram | `plt.hist()` | Distribution of one variable |
| Box Plot | `plt.boxplot()` | Summary stats + outliers |
| Bar Chart | `plt.bar()` | Category comparison |
| Pie Chart | `plt.pie()` | Proportional composition |
| Image Display | `plt.imshow()` | Show raster images |

### <span style="color:#2E86AB">Seaborn Plots Summary</span>

| Category | Plot | Function |
|:---|:---|:---:|
| **Distribution** | Histogram/KDE | `sns.histplot()` / `sns.displot()` |
| | Joint Plot | `sns.jointplot()` |
| | Pair Plot | `sns.pairplot()` |
| | Rug Plot | `sns.rugplot()` |
| **Categorical** | Count Plot | `sns.countplot()` |
| | Bar Plot | `sns.barplot()` |
| | Box Plot | `sns.boxplot()` |
| | Violin Plot | `sns.violinplot()` |
| | Strip Plot | `sns.stripplot()` |
| | Swarm Plot | `sns.swarmplot()` |
| **Regression** | Linear Model Plot | `sns.lmplot()` |
| | Regression Plot | `sns.regplot()` |
| **Matrix** | Heatmap | `sns.heatmap()` |
| | Cluster Map | `sns.clustermap()` |

---

## <span style="color:#1565C0">14. Quick Code Recipes</span>

### <span style="color:#2E86AB">Full Figure with Title, Labels, Legend, Grid</span>

```python
fig, ax = plt.subplots(figsize=(10, 5))
ax.plot(x, y1, color='blue',  lw=2, label='Line 1')
ax.plot(x, y2, color='red',   lw=2, label='Line 2', linestyle='--')
ax.set_title("Complete Plot", fontsize=16)
ax.set_xlabel("X-axis", fontsize=12)
ax.set_ylabel("Y-axis", fontsize=12)
ax.legend()
ax.grid(True)
plt.tight_layout()
plt.show()
```

### <span style="color:#2E86AB">Seaborn Heatmap from Correlation</span>

```python
corr = df[['total_bill', 'tip', 'size']].corr()
plt.figure(figsize=(8, 6))
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt='.2f', linewidths=0.5)
plt.title("Correlation Heatmap")
plt.show()
```

### <span style="color:#2E86AB">Violin + Swarm Overlay</span>

```python
plt.figure(figsize=(10, 5))
sns.violinplot(x="day", y="total_bill", data=df, palette="muted", inner=None)
sns.swarmplot(x="day",  y="total_bill", data=df, color="black", size=3, alpha=0.6)
plt.title("Tips by Day - Violin + Swarm")
plt.show()
```

### <span style="color:#2E86AB">Faceted Regression by Category</span>

```python
sns.lmplot(x="total_bill", y="tip", data=tips,
           hue="sex", col="time",
           palette="Set1")
plt.suptitle("Regression by Time and Sex", y=1.02)
plt.show()
```

---

## <span style="color:#1565C0">15. Key Concepts Glossary</span>

| Term | Definition |
|:---|:---|
| **KDE** | Kernel Density Estimate - smooth curve estimating the probability distribution of a variable |
| **Correlation** | Statistical measure of the strength and direction of the relationship between two variables |
| **Facet Grid** | A grid of plots where each subplot shows a subset of data filtered by a category |
| **Hue** | A third variable encoded as color to add a dimension to a 2D plot |
| **Confidence Interval** | A range that captures the true value with a specified probability (usually 95%) |
| **Pivot Table** | Reshaping of data from long format to a 2D matrix format |
| **Dendrogram** | A tree diagram showing the hierarchical clustering of variables |
| **Jitter** | A small random offset added to points to prevent overlap in strip plots |
| **Palette** | A named set of colors used for consistent, meaningful color encoding |
| **DPI** | Dots Per Inch - controls the resolution of the figure |

---

<div align="center">

<sub>These notes were written and compiled by</sub>

### **Sagar Bhadra**

<sub>Connect with me on</sub>

<br>

[![GitHub](https://img.shields.io/badge/GitHub-SagarBhadra01-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/SagarBhadra01)&nbsp;
[![X (Twitter)](https://img.shields.io/badge/Twitter-SagarBhadra01-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/SagarBhadra01)&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-sagarbhadra01-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sagarbhadra01)&nbsp;
[![Gmail](https://img.shields.io/badge/Gmail-sagarbhadra404@gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:sagarbhadra404@gmail.com)

</div>