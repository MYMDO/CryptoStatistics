# Bitcoin 3D Activity Visualization

Professional 3D visualization of Bitcoin trading activity based on historical data from CoinGecko API. The dashboard analyzes activity patterns across three dimensions: **Day of Week**, **Day of Month**, and **Price Change %**.

## Features

### 3D Visualization
- **Interactive 3D Scatter Plot**: Daily price changes with volume-based marker sizing
  - Green markers: Price increased (bought)
  - Red markers: Price decreased (sold)
  - Marker size represents trading volume

### Activity Zones with Gaussian Smoothing
- **Professional Activity Detection**: Uses Gaussian Smoothing (σ=1.5) to identify natural activity peaks
- **3×3 Grid Method**: For each (day_of_week, day_of_month) combination, analyzes neighboring activity within a 3×3 grid
- **Smooth Surfaces**: Green (bought activity) and Red (sold activity) surfaces show activity zones

### Anomaly Reduction (Winsorization)
- **Interactive Clip Slider**: Reduce impact of outliers (e.g., Feb 6-7, 2026)
- **Multiple Clip Levels**: 0% (no clip), 1%, 5%, 10%
- **Professional Method**: Winsorization clips extreme values instead of removing them, preserving data structure

### Adaptive UI/UX
- **CSS Grid Layout**: Controls on edges, 3D visualization fills the center
- **Responsive Design**: Adapts to different screen sizes
- **Real-time Statistics**: Date range, average price, total volume
- **Top Peaks Display**: Shows top 5 bought/sold activity zones
- **Mode Toggle**: Daily Data / All Zones / Hide All

## Technology Stack

- **Frontend**: Pure HTML + CSS + JavaScript (no build tools required)
- **3D Visualization**: Plotly.js (WebGL-based, hardware accelerated)
- **Data Source**: CoinGecko API (free, no API key required)
- **Analysis Methods**:
  - Gaussian Smoothing (scipy.ndimage.gaussian_filter)
  - Winsorization for outlier treatment
  - 3×3 Grid Activity Zone Detection

## Quick Start

### Option 1: Direct Use (Simplest)
1. Download `bitcoin_3d_viz.html`
2. Open in any modern browser
3. Data fetches automatically from CoinGecko API

```bash
# Just open the file
open bitcoin_3d_viz.html  # macOS
xdg-open bitcoin_3d_viz.html  # Linux
start bitcoin_3d_viz.html  # Windows
```

### Option 2: Python Data Generation
If you want to generate static HTML files with pre-embedded data:

```bash
pip install requests pandas plotly python-dateutil numpy scipy
python crypto_3d_viz.py
```

Generated files:
- `bitcoin_dashboard.html` - Adaptive dashboard
- `bitcoin_heatmaps.html` - 2D heatmaps
- `bitcoin_activity_zones.html` - Activity zones heatmap

## Usage Guide

### Display Modes
- **Daily Data**: Shows individual daily price changes
- **All Zones**: Shows daily data + activity zone surfaces
- **Hide All**: Clears visualization

### Anomaly Clip Slider
Adjust the clip level to reduce outlier impact:
- **0%**: Raw data (shows all anomalies like Feb 6-7, 2026)
- **1%**: Light filtering
- **5%**: Moderate filtering
- **10%**: Strong filtering (reveals true activity patterns)

### Interactive Features
- **Rotate**: Click and drag the 3D plot
- **Zoom**: Scroll wheel or pinch
- **Hover**: Show detailed info (date, price, change %, volume)
- **Toggle surfaces**: Use slider to switch between clip levels

## Data Analysis Methodology

### Activity Score Calculation
```
Activity Score = Volume × |Price Change %|
```

### 3×3 Grid Method
For each intersection (day_of_week, day_of_month):
- Consider days of week: [dow-1, dow, dow+1] (with wrap-around)
- Consider days of month: [day-1, day, day+1]
- Sum activity scores for all 9 combinations
- Separate into "bought" (price up) and "sold" (price down)

### Gaussian Smoothing
- Applies 2D Gaussian filter with σ=1.5
- Creates smooth activity surfaces
- Day-of-week axis uses circular wrap-around
- Identifies natural activity peaks vs. noise

### Winsorization
- Clips extreme values at specified percentiles
- Preserves data structure (unlike trimming)
- Reduces impact of market anomalies
- Standard method in quantitative finance

## Project Structure

```
CryptoStatistics/
├── bitcoin_3d_viz.html      # Standalone HTML (fetches data via API)
└── README.md               # This file
```

**Thats it!** One HTML file contains everything:
- Complete UI/UX with adaptive layout
- All visualization code (Plotly.js)
- Data fetching logic (CoinGecko API)
- Gaussian smoothing & Winsorization algorithms
- No dependencies to install, no build tools needed

## Data Source

**CoinGecko API** (Free tier)
- Endpoint: `/api/v3/coins/{id}/market_chart`
- Parameters: `vs_currency=usd`, `days=365`, `interval=daily`
- Data: Price, volume, market cap for the last 365 days
- No API key required
- Rate limit: ~10-50 calls/minute

## Key Findings (Based on Last 365 Days)

### Highest Activity Zones (No Clip)
**Bought (Price Up):**
1. Saturday the 7th - Score: 170.3B
2. Friday the 7th - Score: 160.7B
3. Saturday the 8th - Score: 156.0B

**Sold (Price Down):**
1. Friday the 6th - Score: 236.9B
2. Thursday the 6th - Score: 215.1B
3. Friday the 5th - Score: 206.1B

### After 10% Winsorization (True Patterns)
**Bought:**
1. Wednesday the 3rd - Score: 95.6B
2. Thursday the 3rd - Score: 94.1B
3. Wednesday the 10th - Score: 92.2B

## Browser Compatibility

- ✅ Chrome/Chromium 60+
- ✅ Firefox 55+
- ✅ Safari 11+
- ✅ Edge 79+
- ⚠️ Internet Explorer not supported (uses modern ES6+ features)

## Contributing

This is a research/visualization project. Feel free to:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

Potential improvements:
- Add more cryptocurrencies (Ethereum, etc.)
- Implement additional smoothing methods
- Add time-of-day analysis (requires paid API for hourly data)
- Create export functionality (PNG, SVG, CSV)

## License

MIT License - feel free to use this project for:
- Personal research
- Educational purposes
- Commercial analysis (with attribution)

## Acknowledgments

- **CoinGecko** for providing free, reliable cryptocurrency data
- **Plotly** for the excellent 3D visualization library
- **SciPy** team for Gaussian smoothing implementation

## Contact & Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Include browser version and error details

---

**Note**: This is a visualization/analysis tool. Not financial advice. Always do your own research before making investment decisions.
