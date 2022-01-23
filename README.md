# molplot
Plotly scatterplots which show molecule images on hovering over the datapoints!

![Beautiful :)](example.png)

Required packages:
- [pandas](https://pandas.pydata.org/docs/getting_started/index.html)
- [rdkit](http://rdkit.org/docs/Install.html)
- [jupyter_dash](https://github.com/plotly/jupyter-dash)

➡️ See `example.ipynb` for an example :)

## 📜 Usage
---
```python
import pandas as pd
import plotly.express as px

import molplotly

# load a DataFrame with smiles
df_esol = pd.read_csv('esol.csv')
df_esol['y_pred'] = df_esol['ESOL predicted log solubility in mols per litre']
df_esol['y_true'] = df_esol['measured log solubility in mols per litre']

# generate a scatter plot
fig = px.scatter(df_esol, x="y_true", y="y_pred")

# add molecules to the plotly graph - returns a Dash app
app = molplotly.add_molecules(fig=fig, 
                            df=df_esol, 
                            smiles_col='smiles', 
                            title_col='Compound ID', 
                            )

# run Dash app inline in notebook (or in an external server)
app.run_server(mode='inline', port=8011, height=1000)
```
#### Input parameters
* `fig` : plotly.graph_objects.Figure object\
    a plotly figure object containing datapoints plotted from df
* `df` : pandas.DataFrame object\
    a pandas dataframe that contains the data plotted in fig
* `smiles_col` : str, optional\
    name of the column in df containing the smiles plotted in fig (default 'SMILES')
* `show_img` : bool, optional\
    whether or not to generate the molecule image in the dash app (default True)
* `title_col` : str, optional\
    name of the column in df to be used as the title entry in the hover box (default None)
* `show_coords` : bool, optional\
    whether or not to show the coordinates of the data point in the hover box (default True)
* `caption_cols` : list, optional\
    list of column names in df to be included in the hover box (default None)
* `condition_col` : str, optional\
    name of the column in df that is used to color the datapoints in df - necessary when there is discrete conditional coloring (default None)
* `wrap` : bool, optional\
    whether or not to wrap the title text to multiple lines if the length of the text is too long (default True)
* `wraplen` : int, optional\
    the threshold length of the title text before wrapping begins - adjust when changing the width of the hover box (default 20)
* `width` : int, optional\
    the width in pixels of the hover box (default 150)
* `fontfamily` : str, optional\
    the font family used in the hover box (default 'Arial')
* `fontsize` : int, optional\
    the font size used in the hover box - the font of the title line is fontsize+2 (default 12)
    
#### Output parameters
by default a JupyterDash `app` is returned which can be run inline in a jupyter notebook or deployed on a server via `app.run_server()`

### Features to-add:
1. Individual styles for each caption (fonts, colors etc)
2. Some way to save the plot
3. Highlight points by clicking on them
4. SVG image generation
