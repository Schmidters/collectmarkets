# 🚀 Polymarket Collector & Analyzer

**Interactive menu-driven application for collecting and analyzing Polymarket trading activity**

## ✨ Features

### 📊 Data Collection
- Fetch complete trading history from Polymarket wallets
- Automatic pagination and deduplication
- Export to organized CSV files (grouped by market)
- Support for unlimited wallets

### 📈 Visualization
- Interactive market analysis plots
- **Plot 1**: Trade scatter plot
  - X-axis: Price (0.01 - 1.00)
  - Y-axis: Timestamp
  - Point size = USDC amount
  - Green points = UP trades
  - Red points = DOWN trades
- **Plot 2**: Cumulative contract accumulation over time
- Automatic statistics calculation
- **Minimum trades filter**: Markets with <30 trades are not saved (too few for analysis)

### 🎯 Interactive Menu System
```
MAIN MENU
├── [1] Run Wallet Analysis
│   └── Select wallet → Fetch data → Save CSVs
├── [2] Add New Wallet
│   └── Enter name & address → Save to wallets.txt
├── [3] Create Market Plot
│   └── Select blogger → Select market → Generate plot
└── [4] Exit
```

## 🚀 Quick Start

```bash
cd /root/mcollect
python3 collector.py
```

## 📋 Requirements

```bash
pip3 install -r requirements.txt
```

Dependencies:
- `requests` - API communication
- `matplotlib` - Data visualization

## 📁 Project Structure

```
/root/mcollect/
├── collector.py         # Main application (interactive menu)
├── wallets.txt          # Wallet addresses (name,address format)
├── requirements.txt     # Python dependencies
├── README.md            # Documentation
├── LICENSE              # MIT License
├── data/                # Output directory (CSV files)
│   └── {wallet_name}/
│       └── {market_slug}.csv
└── plots/               # Generated plots (PNG files)
    └── {market_slug}.png
```

## 🎮 Menu Navigation

### Main Menu
- **[1] Run Wallet Analysis**: Collect data from Polymarket API
  - Select from existing wallets
  - After completion: automatically returns to wallet list
  - Can run multiple analyses in sequence
  - Press "Back" to return to main menu

- **[2] Add New Wallet**: Add new wallet to collection
  - Enter wallet name (e.g., "myWallet")
  - Enter wallet address (0x...)
  - Automatically saved to `wallets.txt`
  - Returns to main menu after completion

- **[3] Create Market Plot**: Visualize trading activity
  - Step 1: Select blogger (data folder)
  - Step 2: Select market (CSV file)
  - Step 3: Generate dual plot
  - Option: "Create another plot?" (y/N)
  - Navigate back at any step

- **[4] Exit**: Close application

### Navigation Tips
- Each menu has clear back/exit options
- Use numbers to select options
- Press Enter for default choices (where available)
- Can interrupt at any time with Ctrl+C

## 🎯 Market Filtering

**Automatic Quality Control:**
- Markets with **less than 30 TRADE records** are automatically skipped
- These markets are not saved to CSV (insufficient data for analysis)
- Skipped markets are reported after collection with trade counts
- This ensures only meaningful datasets are stored

## 📊 CSV Data Format

Each market CSV contains:
- `timestamp` - Unix timestamp
- `datetime` - Human-readable time
- `type` - Activity type (TRADE, MERGE, SPLIT)
- `outcome` - Trade side (Up/Down)
- `size` - Number of contracts
- `usdcSize` - Trade size in USDC
- `price` - Contract price
- `transactionHash` - Blockchain tx hash
- `title` - Market question
- Plus user/market metadata

## 📈 Plot Features

Generated plots include:

**Top Panel - Purchase Scatter**
- X-axis: Timestamp
- Y-axis: USDC Size
- Point size: Proportional to USDC amount
- Green = UP trades, Red = DOWN trades
- Shows trading intensity and timing

**Bottom Panel - Contract Accumulation**
- X-axis: Timestamp
- Y-axis: Cumulative contracts
- Green line = UP contracts
- Red line = DOWN contracts
- Shows position building over time

**Statistics Box**
- Total trades
- UP: trades, contracts, USDC spent
- DOWN: trades, contracts, USDC spent

## 🔧 Configuration

Edit these variables in `collector.py`:

```python
WALLET_FILE = "/root/mcollect/wallets.txt"  # Wallet storage
OUTPUT_ROOT = "/root/mcollect/data"         # CSV output directory
PLOTS_DIR = "/root/mcollect/plots"          # Plot output directory
```

## 💡 Example Workflow

1. **Initial Setup**
   ```bash
   python3 collector.py
   [2] Add New Wallet → Enter details
   ```

2. **Collect Data**
   ```bash
   [1] Run Wallet Analysis
   Select wallet → Wait for completion
   ```

3. **Visualize Results**
   ```bash
   [3] Create Market Plot
   Select blogger → Select market → View plot
   ```

4. **Analyze Multiple Markets**
   ```bash
   After plot creation: "Create another plot? (y)"
   → Repeat for different markets
   ```

## 🎯 Use Cases

- **Trader Analysis**: Study position building strategies
- **Performance Review**: Analyze entry timing and sizing
- **Market Research**: Compare activity across different markets
- **Portfolio Tracking**: Monitor multiple wallets
- **Strategy Backtesting**: Export data for external analysis

## 📝 Notes

- **Rate Limiting**: 0.5s delay between API requests
- **Max Records**: 10,000 per wallet (configurable)
- **Plot Format**: PNG, 150 DPI, saved to `plots/`
- **CSV Encoding**: UTF-8
- **Timezone**: All timestamps in UTC

## 🐛 Troubleshooting

**No data collected?**
- Verify wallet address (must start with 0x)
- Check internet connection
- Wallet might have no trading activity

**Plot creation fails?**
- Ensure CSV file contains TRADE records
- Check matplotlib installation: `pip3 list | grep matplotlib`
- Verify data integrity in CSV

**Menu navigation issues?**
- Use numeric input (1, 2, 3, etc.)
- Press Enter after each input
- Use Ctrl+C to force exit if stuck

## 📄 License

MIT License - see LICENSE file for details

## 🤝 Support

For issues or questions:
1. Check CSV files in `data/` directory
2. Review plot files in `plots/` directory
3. Check console output for error messages

---

**Made with ❤️ for Polymarket traders**
