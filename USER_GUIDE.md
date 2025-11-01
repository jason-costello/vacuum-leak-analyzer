# Vacuum Leak Analyzer

A web-based tool for analyzing automotive vacuum leaks using fuel trim data from OBD-II logs.

## Live Demo

Access the tool at: `https://[your-username].github.io/[repo-name]/`

## Overview

This analyzer processes fuel trim data at different RPM levels to detect potential vacuum leaks in your vehicle's intake system. It compares short-term and long-term fuel trims between idle and high RPM conditions to identify abnormal changes that indicate a vacuum leak.

## How It Works

The tool analyzes fuel trim data by:
1. Finding stable 30+ second periods at idle and high RPM
2. Calculating average total fuel trims (STFT + LTFT) for each bank during a 15-second window
3. Comparing the difference between idle and high RPM fuel trims
4. Flagging potential leaks when the difference exceeds a configurable threshold

## Usage Instructions

### 1. Prepare Your Data File

Export your OBD-II scan data as a CSV or tab-delimited text file containing the following columns:
- Time (milliseconds)
- RPM
- Short Term Fuel Trim Bank 1 (SHRTFT1)
- Short Term Fuel Trim Bank 2 (SHRTFT2)
- Long Term Fuel Trim Bank 1 (LONGFT1)
- Long Term Fuel Trim Bank 2 (LONGFT2)

**Recommended data collection:**
- Record at idle (600-800 RPM) for at least 30 seconds
- Record at elevated RPM (3000-3500 RPM) for at least 30 seconds
- Ensure engine is at operating temperature
- Data should be logged continuously

### 2. Load Your File

Click "Choose File" and select your data file. The tool will:
- Automatically detect the delimiter (comma, semicolon, or tab)
- Attempt to auto-map column headers
- If headers don't match standard format, a mapping interface will appear

### 3. Configure Parameters (Optional)

Adjust the following settings if needed:

**Idle Configuration:**
- **Idle RPM**: Target idle speed (default: 600)
- **Idle Tolerance**: RPM variance allowed (default: ±100)

**High RPM Configuration:**
- **High RPM**: Target elevated speed (default: 3500)
- **High RPM Tolerance**: RPM variance allowed (default: ±100)

**Analysis Settings:**
- **Leak Threshold (%)**: Sensitivity for leak detection (default: 15%)
    - Lower values = more sensitive
    - Higher values = less sensitive

### 4. Analyze

Click the "Analyze Data" button. Results will appear at the top showing:
- Average total fuel trims at idle RPM
- Average total fuel trims at high RPM
- Vacuum leak analysis for each bank
- Color-coded border (green = no leak, red = leak detected)

### 5. Interpret Results

**No Leak Detected:**
- Fuel trim changes between idle and high RPM are within normal range
- Both banks show similar behavior

**Leak Indicated:**
- Significant difference between idle and high RPM fuel trims
- One or both banks exceed the threshold percentage
- Further diagnostic testing recommended

## Troubleshooting

**"No valid 30+ second period found"**
- Ensure your log contains at least 30 continuous seconds at the target RPM
- Check that RPM values in your log match configured targets
- Try increasing RPM tolerance values

**"Missing required headers"**
- Use the mapping interface to manually match your columns
- Ensure all required data columns are present in your file

**Analyze button remains disabled**
- Verify file loaded successfully (check browser console for errors)
- Ensure all required columns are mapped
- Try reloading the page and selecting the file again

## Debug Mode

Enable "Show Debug Information" to see:
- File parsing details
- RPM group search progress
- Calculation windows and averages
- Detailed diagnostic information

## Data Privacy

All processing happens locally in your browser. No data is uploaded to any server.

## Browser Compatibility

Works with modern browsers supporting HTML5 and ES6:
- Chrome/Edge (recommended)
- Firefox
- Safari

## Technical Notes

- Analysis uses a 15-second sliding window at the midpoint of each RPM period
- Total fuel trim = Short Term FT + Long Term FT
- Threshold percentage is applied to the absolute value of idle fuel trims
- Requires stable RPM (within tolerance) for minimum 30 seconds

## License

[Add your license information here]

## Contributing

[Add contribution guidelines here]

## Support

For issues or questions, please open an issue on the [GitHub repository](https://github.com/[your-username]/[repo-name]).