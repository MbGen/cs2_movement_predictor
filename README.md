# CS2 Player Movement Prediction (Experimental)

## ⚠️ Disclaimer

This is a **purely experimental amateur project** designed to explore whether CS2 players move in predictable patterns that a neural network could learn to forecast. This is NOT a production-ready system or a serious research project - just a fun experiment to satisfy curiosity!

## 📊 Dataset

- **Size**: ~80 demo replays
- **Purpose**: Testing feasibility of movement prediction
- **Scope**: Limited dataset for proof-of-concept only

## 🎯 Project Goal

The main question I wanted to answer: **Do players move in template-like patterns that a model can predict?**

Turns out... sometimes yes! The model can capture certain movement tendencies, though with limited data, the predictions are far from perfect.

## 🗺️ Visualization

Currently, only the **de_inferno** map is available for visualization. However, you can easily add your own maps!

### Adding Custom Maps

To add a new map, you need to:

1. Get a top-down map image (PNG format recommended)
2. Find the world coordinate boundaries (min/max X and Y)
3. Add the configuration to `MAP_CONFIGS` dictionary

**Example:**
```python
MAP_CONFIGS = {
    7: {  # de_inferno
        'name': 'de_inferno',
        'image_path': r"path/to/INFERNO.png",
        'bounds': {'xmin': -1861, 'ymin': -833, 'xmax': 2897, 'ymax': 3660}
    },
    1: {  # de_dust2
        'name': 'de_dust2',
        'image_path': r"path/to/DUST2.png",
        'bounds': {'xmin': X, 'ymin': Y, 'xmax': N, 'ymax': M}
    },
    # Add more maps here...
}
```

### How to Find Map Boundaries (My approach)

1. Spawn two bots into the game.
2. Enter spectator mode and open the map.
3. Locate the bottom-left corner and the top-right corner of the map area.
4. Place one bot at the bottom-left corner and the other bot at the top-right corner. Use the bots as visual markers.
5. While still in spectator mode, look at the area containing both bots and, using the console, type the command getpos.
6. Take a screenshot of the view showing both the map area and the two bots marking the corners.

> If I haven't changed the Demo GIF, the two blue dots you see are the bots positioned in the corners (bottom-left and top-right).

## 🎬 Demo

![Movement Prediction Demo](https://raw.githubusercontent.com/MbGen/cs2_movement_predictor/master/demo_gifs/demo.gif)

### with disabled noisy path

![Movement Prediction Demo without path](https://raw.githubusercontent.com/MbGen/cs2_movement_predictor/master/demo_gifs/without_full_path.gif)

### manual mode

![Manual mode](https://raw.githubusercontent.com/MbGen/cs2_movement_predictor/master/demo_gifs/manual.gif)

The visualization shows:
- 🔴 **Red (and other colors)**: Actual path taken by the player
- 🔵 **Blue**: Model predictions (dashed lines and points)
- Player nicknames are displayed at their current position

## 🚀 Features

- **Interactive UI**: Select maps, games, rounds, and specific players
- **Multi-player visualization**: View multiple trajectories simultaneously
- **Prediction metrics**: Real-time accuracy statistics
  - Mean error distance
  - Median error
  - Min/Max error
  - Standard deviation
- **Animation mode**: Watch predictions unfold step-by-step
- **Flexible filtering**: Filter by team (CT/T) or individual players

## 📈 Model Accuracy

The model's prediction accuracy is displayed in real-time, showing:
- Average distance error between predicted and actual positions
- Per-player statistics
- Overall performance metrics

Keep in mind: with only ~80 replays, the model has limited learning capacity. More data would significantly improve predictions!

## 🛠️ Technical Stack

- **Framework**: PyTorch
- **Model**: Trajectory Predictor (custom architecture)
- **Visualization**: PIL (Pillow), IPython widgets
- **Data Processing**: Pandas, NumPy

## 📦 Requirements
```python
demoparser2 (https://github.com/LaihoE/demoparser)
torch
pandas
numpy
pillow
ipywidgets
tqdm
```

## 🎮 Usage

1. All usage in DemoAI.ipynb file
2. Run `data loader cell` -> then model `architecure cell` -> in the end of file bottom `UI cell`

4. Use the UI to:
   - Select a map
   - Choose a game and round
   - Pick players to visualize
   - Toggle animation on/off
   - View prediction accuracy

## 🔍 How It Works

1. **Data Collection**: Extract player positions from CS:GO demo files
2. **Training**: Feed historical movement sequences to predict future positions
3. **Prediction**: Model forecasts the next 24 movement points
4. **Visualization**: Overlay predictions on the map alongside actual paths

## 🎓 What I Learned

- Players DO have movement patterns, especially in certain areas (common angles, rotation paths)
- Limited data means limited generalization
- Map-specific patterns emerge (site executes, retake routes)
- Prediction accuracy varies heavily based on situation (structured vs. chaotic moments)

## 🚧 Limitations

- Very small dataset (~80 demos)
- Only one map fully configured (de_inferno)
- Amateur implementation (not optimized for production)
- Predictions work better for "expected" movements (rushes, rotations) than unpredictable fights
- No consideration of game state context (bomb plant, player count, economy, etc.)

## 🔮 Future Ideas

If I continue this experiment:
- Gather more data (hundreds of demos)
- Add game state features (HP, equipment, teammates alive, etc.)
- Implement attention mechanisms to focus on critical moments
- Multi-map training
- Team coordination patterns

## 📝 License

This is an experimental project for educational purposes. Feel free to use, modify, or learn from it!

## 🤝 Contributing

This is a personal experiment, but if you find it interesting and want to add features or maps, feel free to fork and experiment!

---

**Remember**: This is just for fun and learning! Don't expect state-of-the-art predictions from 80 demos 😄