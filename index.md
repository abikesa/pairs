# Python | AI | R | Stata

```bash
rm -rf myenv
python 0m venv myenv
```

Running cells with `myenv (Python 3.11.4)` requires the `ipykernel` package

It seems like your `pip` installation is pointing to a different Python environment (`/usr/local/anaconda3/lib/python3.11/site-packages`), but your current Python interpreter is not using this environment. 

To resolve this issue, you need to ensure that you are using the same Python interpreter where `networkx` is installed. Here are a few steps to help you align your environment:

### Check Python Interpreter
1. **Check the Python interpreter**:
   ```shell
   which python
   ```

2. **Check Python version**:
   ```shell
   python --version
   ```

### Ensure Correct Environment Activation
If you are using a virtual environment, ensure it's activated correctly. If not, you may want to use `conda` to manage your environment since you have Anaconda installed.

#### Using Conda Environment
1. **Create a new Conda environment (if needed)**:
   ```shell
   conda create -n myenv python=3.11
   ```

2. **Activate the Conda environment**:
   ```shell
   conda activate myenv
   ```

3. **Install `networkx` in the Conda environment**:
   ```shell
   conda install networkx matplotlib
   ```

4. **Run your script**:
   ```shell
   python your_script.py
   ```

### Verify Installation in Current Environment
1. **Check installed packages**:
   ```shell
   pip list
   ```

2. **Install `networkx` again**:
   ```shell
   pip install networkx matplotlib
   ```

### Running the Script
Ensure you are in the correct environment and run your script. Here's the complete script you provided for reference:

```python
import networkx as nx
import matplotlib.pyplot as plt

G = nx.DiGraph()
G.add_node("Audio/Vision", pos=(-2500, 700))
G.add_node("Text/Language", pos=(-4200, 0))
G.add_node("Frailty", pos=(-1000, 0))
G.add_node("Haptic/Robot", pos=(-2500, -700))
G.add_node("Real-Time", pos=(1500, 0))
G.add_node("Outcome", pos=(4000, 0))

G.add_edges_from([("Audio/Vision", "Frailty")])
G.add_edges_from([("Text/Language", "Frailty")])
G.add_edges_from([("Haptic/Robot", "Frailty")])
G.add_edges_from([("Frailty", "Real-Time")])
G.add_edges_from([("Real-Time", "Outcome")])

pos = nx.get_node_attributes(G, 'pos')
labels = {"Frailty": "Frailty\n(Phenotype)",
          "Audio/Vision": "Audio/Vision",
          "Text/Language": "Text/Language",
          "Haptic/Robot": "Haptic/Robot",
          "Real-Time": "Real-Time",
          "Outcome": "Outcome\n(Hard Endpoints)"}

# Update color for the "Scenarios" node
node_colors = ["lightblue", "lightblue", "lavender", "lightblue", "lightblue", "lightblue"]

# Suppress the deprecation warning
import warnings
warnings.filterwarnings("ignore", category=DeprecationWarning)

plt.figure(figsize=(10, 8))
nx.draw(G, pos, with_labels=False, node_size=20000, node_color=node_colors, linewidths=2, edge_color='black', style='solid')
nx.draw_networkx_labels(G, pos, labels, font_size=14)
nx.draw_networkx_edges(G, pos, edge_color='black', style='solid', width=2)
plt.xlim(-5000, 5000)
plt.ylim(-1000, 1000)
plt.axis("off")
plt.show()
```

Make sure to execute the script within the environment where `networkx` and `matplotlib` are installed. If you encounter any further issues, please let me know!
