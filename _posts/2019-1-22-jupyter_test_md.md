---
mathjax: true
title:  "Testing Jupyter Embedding in Jekyll for Markdown"
search: false
categories: 
  - Jekyll
last_modified_at: 2019-1-22
---


```python
%load_ext watermark
%watermark -u -n -t -z
print()
%watermark -v -m -p requests,pandas,numpy,seaborn,folium,requests
```

    The watermark extension is already loaded. To reload it, use:
      %reload_ext watermark
    last updated: Tue Jan 22 2019 22:20:14 CET
    
    CPython 3.6.5
    IPython 7.2.0
    
    requests 2.21.0
    pandas 0.23.4
    numpy 1.15.2
    seaborn 0.9.0
    folium 0.7.0
    requests 2.21.0
    
    compiler   : GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.57)
    system     : Darwin
    release    : 18.2.0
    machine    : x86_64
    processor  : i386
    CPU cores  : 4
    interpreter: 64bit


# Testing Jupyter embedded in Jekyll


```python
import pandas as pd
import numpy as np
import scipy as sp
import plotly.plotly as py
import plotly.figure_factory as ff
```


```python
import json
with open("./credential.txt") as f:
    credential = json.load(f)
plotly.tools.set_credentials_file(username=credential['username'], api_key=credential['api_key'])
```


```python
df = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/school_earnings.csv")

table = ff.create_table(df)
py.iplot(table, filename='jupyter-table1')
```

    High five! You successfully sent some data to your account on plotly. View your plot in your browser at https://plot.ly/~yoonoh930/0 or inside your plot.ly account where it is named 'jupyter-table1'


    /Users/yoonseokoh/.local/share/virtualenvs/Python-DL3NB1tv/lib/python3.6/site-packages/IPython/core/display.py:689: UserWarning:
    
    Consider using IPython.display.IFrame instead
    





<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~yoonoh930/0.embed" height="710px" width="100%"></iframe>




```python
s = np.linspace(0, 2 * np.pi, 240)
t = np.linspace(0, np.pi, 240)
tGrid, sGrid = np.meshgrid(s, t)

r = 2 + np.sin(7 * sGrid + 5 * tGrid)  # r = 2 + sin(7s+5t)
x = r * np.cos(sGrid) * np.sin(tGrid)  # x = r*cos(s)*sin(t)
y = r * np.sin(sGrid) * np.sin(tGrid)  # y = r*sin(s)*sin(t)
z = r * np.cos(tGrid)                  # z = r*cos(t)

surface = go.Surface(x=x, y=y, z=z)
data = [surface]

layout = go.Layout(
    title='Parametric Plot',
    scene=dict(
        xaxis=dict(
            gridcolor='rgb(255, 255, 255)',
            zerolinecolor='rgb(255, 255, 255)',
            showbackground=True,
            backgroundcolor='rgb(230, 230,230)'
        ),
        yaxis=dict(
            gridcolor='rgb(255, 255, 255)',
            zerolinecolor='rgb(255, 255, 255)',
            showbackground=True,
            backgroundcolor='rgb(230, 230,230)'
        ),
        zaxis=dict(
            gridcolor='rgb(255, 255, 255)',
            zerolinecolor='rgb(255, 255, 255)',
            showbackground=True,
            backgroundcolor='rgb(230, 230,230)'
        )
    )
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='jupyter-parametric_plot')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~yoonoh930/2.embed" height="525px" width="100%"></iframe>




```python
import folium


m = folium.Map(location=[45.5236, -122.6750])
```


```python
m
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVM9ZmFsc2U7IExfTk9fVE9VQ0g9ZmFsc2U7IExfRElTQUJMRV8zRD1mYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4zLjQvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4zLjQvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdjZG4uZ2l0aGFjay5jb20vcHl0aG9uLXZpc3VhbGl6YXRpb24vZm9saXVtL21hc3Rlci9mb2xpdW0vdGVtcGxhdGVzL2xlYWZsZXQuYXdlc29tZS5yb3RhdGUuY3NzIi8+CiAgICA8c3R5bGU+aHRtbCwgYm9keSB7d2lkdGg6IDEwMCU7aGVpZ2h0OiAxMDAlO21hcmdpbjogMDtwYWRkaW5nOiAwO308L3N0eWxlPgogICAgPHN0eWxlPiNtYXAge3Bvc2l0aW9uOmFic29sdXRlO3RvcDowO2JvdHRvbTowO3JpZ2h0OjA7bGVmdDowO308L3N0eWxlPgogICAgCiAgICA8bWV0YSBuYW1lPSJ2aWV3cG9ydCIgY29udGVudD0id2lkdGg9ZGV2aWNlLXdpZHRoLAogICAgICAgIGluaXRpYWwtc2NhbGU9MS4wLCBtYXhpbXVtLXNjYWxlPTEuMCwgdXNlci1zY2FsYWJsZT1ubyIgLz4KICAgIDxzdHlsZT4jbWFwX2IyNDU3MDJlMTE4ZjQ5MmU5YzEyZjJhOGM0OTJmMmQ1IHsKICAgICAgICBwb3NpdGlvbjogcmVsYXRpdmU7CiAgICAgICAgd2lkdGg6IDEwMC4wJTsKICAgICAgICBoZWlnaHQ6IDEwMC4wJTsKICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgIHRvcDogMC4wJTsKICAgICAgICB9CiAgICA8L3N0eWxlPgo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgPGRpdiBjbGFzcz0iZm9saXVtLW1hcCIgaWQ9Im1hcF9iMjQ1NzAyZTExOGY0OTJlOWMxMmYyYThjNDkyZjJkNSIgPjwvZGl2Pgo8L2JvZHk+CjxzY3JpcHQ+ICAgIAogICAgCiAgICAKICAgICAgICB2YXIgYm91bmRzID0gbnVsbDsKICAgIAoKICAgIHZhciBtYXBfYjI0NTcwMmUxMThmNDkyZTljMTJmMmE4YzQ5MmYyZDUgPSBMLm1hcCgKICAgICAgICAnbWFwX2IyNDU3MDJlMTE4ZjQ5MmU5YzEyZjJhOGM0OTJmMmQ1JywgewogICAgICAgIGNlbnRlcjogWzQ1LjUyMzYsIC0xMjIuNjc1XSwKICAgICAgICB6b29tOiAxMCwKICAgICAgICBtYXhCb3VuZHM6IGJvdW5kcywKICAgICAgICBsYXllcnM6IFtdLAogICAgICAgIHdvcmxkQ29weUp1bXA6IGZhbHNlLAogICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcsCiAgICAgICAgem9vbUNvbnRyb2w6IHRydWUsCiAgICAgICAgfSk7CgogICAgCiAgICAKICAgIHZhciB0aWxlX2xheWVyX2U5ZGFiOGU1Yjc3YTRjMmU4ZDIwYTExNjQ3MDhhOTdmID0gTC50aWxlTGF5ZXIoCiAgICAgICAgJ2h0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nJywKICAgICAgICB7CiAgICAgICAgImF0dHJpYnV0aW9uIjogbnVsbCwKICAgICAgICAiZGV0ZWN0UmV0aW5hIjogZmFsc2UsCiAgICAgICAgIm1heE5hdGl2ZVpvb20iOiAxOCwKICAgICAgICAibWF4Wm9vbSI6IDE4LAogICAgICAgICJtaW5ab29tIjogMCwKICAgICAgICAibm9XcmFwIjogZmFsc2UsCiAgICAgICAgIm9wYWNpdHkiOiAxLAogICAgICAgICJzdWJkb21haW5zIjogImFiYyIsCiAgICAgICAgInRtcyI6IGZhbHNlCn0pLmFkZFRvKG1hcF9iMjQ1NzAyZTExOGY0OTJlOWMxMmYyYThjNDkyZjJkNSk7Cjwvc2NyaXB0Pg==" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>


$$
\begin{equation*}
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0
\end{vmatrix}
\end{equation*}
$$

