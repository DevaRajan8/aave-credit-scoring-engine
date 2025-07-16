# Aave V2 Credit Scoring System

## Overview

This system assigns credit scores (0-1000) to Aave V2 protocol wallets based on their historical transaction behavior. The model identifies reliable, responsible users versus risky, bot-like, or exploitative behavior patterns.

## Architecture

### Core Components

1. **Data Preprocessing**: Normalizes transaction amounts, handles different token decimals, calculates USD values
2. **Feature Engineering**: Extracts 20+ behavioral features per wallet
3. **Credit Scoring**: Hybrid approach combining rule-based (40%) and ML-based (60%) scoring
4. **Analysis & Visualization**: Comprehensive score distribution analysis and behavioral insights

### Processing Flow

```
Raw JSON Data → Data Preprocessing → Feature Engineering → Credit Scoring → Analysis & Output
```

## Features Engineered

### Transaction Metrics
- **Total transactions**: Volume of activity
- **Unique assets**: Diversification indicator
- **Total volume USD**: Financial scale
- **Average/median transaction size**: Typical behavior patterns
- **Activity duration**: Time span of engagement

### Behavioral Patterns
- **Action ratios**: Deposit, borrow, repay, redeem, liquidation proportions
- **Transaction regularity**: Consistency of timing patterns
- **Volume consistency**: Stability of transaction amounts
- **Borrow-repay ratio**: Debt management behavior
- **Bot score**: Automated behavior detection

### Risk Indicators
- **Liquidation count/ratio**: Direct risk measure
- **Has liquidations**: Binary risk flag
- **Transaction frequency**: Potential manipulation detection

## Scoring Methodology

### Rule-Based Component (40% weight)
- **Base score**: 500 points
- **Positive factors**: High volume, long activity, good repayment, deposits, diversification
- **Negative factors**: Liquidations, bot behavior, irregular patterns

### ML Component (60% weight)
- **Model**: Random Forest Regressor
- **Training**: Synthetic target based on risk/reward factors
- **Features**: All engineered features with automatic importance weighting

### Final Score Calculation
```python
final_score = 0.4 * rule_score + 0.6 * ml_score
scaled_score = normalize_to_0_1000(final_score)
```

## Usage Instructions

### For Google Colab:
1. Upload the JSON file when prompted
2. Run the complete script
3. View analysis plots and statistics

### For Local Environment:
1. Update `file_path` variable with your JSON file location
2. Install required dependencies: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`
3. Run the script

## Model Validation

### Score Distribution Analysis
- Histogram of credit scores across all wallets
- Breakdown by score ranges (0-100, 100-200, etc.)
- Feature importance ranking

### Behavioral Insights
- **Low Score Wallets (< 300)**: High liquidation rates, bot-like behavior, irregular patterns
- **High Score Wallets (> 700)**: Consistent activity, good repayment history, diverse asset usage

## Key Assumptions

1. **Liquidations are negative**: Indicates poor risk management
2. **Regular repayments are positive**: Shows responsible borrowing
3. **Diverse asset usage is positive**: Indicates sophisticated users
4. **Bot-like behavior is negative**: Suggests potential manipulation
5. **Volume and duration matter**: Larger, longer-term users are more reliable

## Extensibility

The system is designed for easy extension:

- **New features**: Add to `_calculate_wallet_features()` method
- **Different scoring weights**: Modify rule-based scoring parameters
- **Alternative ML models**: Replace RandomForestRegressor in `_calculate_ml_scores()`
- **Custom risk factors**: Update synthetic target creation logic

## Output

1. **CSV file**: `wallet_credit_scores.csv` with wallet addresses and scores
2. **Visualizations**: Score distribution, feature importance, behavioral analysis
3. **Statistics**: Comprehensive analysis of scoring patterns

## Score Interpretation

- **800-1000**: Excellent - Highly reliable, sophisticated users
- **600-799**: Good - Responsible users with minor risks
- **400-599**: Average - Typical DeFi users
- **200-399**: Poor - Risky behavior patterns
- **0-199**: Very Poor - High risk, potential bots/exploiters

## Technical Notes

- Handles different token decimals (USDC: 6, ETH: 18, etc.)
- Robust to missing data and edge cases
- Scalable to large datasets
- Provides interpretable results with feature importance

