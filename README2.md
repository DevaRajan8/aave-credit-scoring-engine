# Compound Protocol Wallet Risk Scoring System

## Overview

This comprehensive system assigns risk scores (0-1000) to Compound V2/V3 protocol wallets based on their historical transaction behavior and on-chain activity patterns. The model identifies high-risk wallets that may pose liquidation risks, exhibit bot-like behavior, or demonstrate poor risk management practices in DeFi lending protocols.

## Purpose

- **Risk Assessment**: Evaluate wallet creditworthiness for lending protocols
- **Liquidation Risk Prediction**: Identify wallets with high probability of liquidation events
- **Behavioral Analysis**: Detect automated trading, flash loan exploitation, and manipulation
- **Portfolio Management**: Enable informed decision-making for DeFi lending and borrowing

## Architecture

### Core Components

1. **Data Collection Engine**: Fetches comprehensive transaction data from Etherscan API
2. **Transaction Filter**: Isolates Compound V2/V3 protocol interactions
3. **Feature Engineering Pipeline**: Extracts 25+ behavioral and risk indicators
4. **Multi-Component Risk Scorer**: Hybrid scoring system with weighted risk factors
5. **Analysis & Reporting**: Comprehensive risk distribution analysis and insights

### Processing Flow

```
Wallet Addresses → Etherscan API → Transaction Filtering → Feature Engineering → Risk Scoring → Analysis & Output
```

## Features Engineered

### Transaction Metrics
- **Total transactions**: Volume of protocol activity
- **Account age**: Time since first transaction
- **Transaction frequency**: Activity rate and consistency
- **Volume metrics**: Total ETH volume, average/median transaction sizes
- **Gas analysis**: Usage patterns indicating transaction complexity

### Behavioral Patterns
- **Activity ratios**: Recent vs historical activity patterns
- **Contract diversity**: Interaction with different Compound contracts
- **Token diversification**: Number of unique tokens interacted with
- **Trading patterns**: Rapid trading period detection
- **Temporal consistency**: Regular vs irregular activity timing

### Risk Indicators
- **Failure rate**: Proportion of failed transactions
- **Liquidation risk**: Derived from trading volatility and exposure
- **Concentration risk**: Portfolio and strategy concentration metrics
- **Leverage indicators**: Complex operation patterns and high gas usage
- **Recency risk**: Time since last activity and position staleness

## Scoring Methodology

### Multi-Component Risk Model

The system uses 6 weighted risk components:

| Component | Weight | Description |
|-----------|--------|-------------|
| **Liquidation Risk** | 30% | Position vulnerability and exposure management |
| **Volatility Risk** | 20% | Trading pattern instability and erratic behavior |
| **Concentration Risk** | 15% | Portfolio diversification and strategy concentration |
| **Activity Risk** | 15% | Usage patterns and engagement consistency |
| **Leverage Risk** | 12% | Complex operations and high-leverage indicators |
| **Recency Risk** | 8% | Position staleness and account activity |

### Score Calculation Process

1. **Feature Extraction**: 25+ risk indicators calculated per wallet
2. **Component Scoring**: Each risk component scored 0-100
3. **Weighted Aggregation**: Components combined using predefined weights
4. **Non-linear Scaling**: Enhanced distribution for better risk differentiation
5. **Final Normalization**: Scaled to 0-1000 range with appropriate thresholds


## Usage Instructions

### Prerequisites

```bash
pip install pandas numpy requests matplotlib seaborn scikit-learn
```

### Configuration

1. **Etherscan API Key**: Replace `ETHERSCAN_API_KEY` with your API key
2. **Input File**: Ensure `Wallet id - Sheet1.csv` contains wallet addresses
3. **Rate Limiting**: Adjust API delay if needed for your rate limits


## Model Validation

### Score Distribution Analysis
- **Range**: 0-1000 (lower scores indicate less risk)
- **Distribution**: Realistic spread with concentration in medium-risk categories
- **Outlier Detection**: Identifies extreme risk cases for manual review

### Risk Categories
- **Very Low (0-149)**: Excellent risk profile, minimal liquidation risk
- **Low (150-299)**: Good risk management, stable activity patterns
- **Medium (300-499)**: Average DeFi users with moderate risk factors
- **High (500-699)**: Elevated risk, requires monitoring
- **Very High (700-1000)**: Critical risk, high liquidation probability

## 🔬 Advanced Features

### Sophisticated Risk Detection
- **Rapid Trading Detection**: Identifies high-frequency trading patterns
- **Volume Concentration Analysis**: Measures portfolio concentration using HHI
- **Temporal Pattern Recognition**: Detects irregular activity timing
- **Gas Cost Analysis**: Complex transaction pattern identification
- **Cross-Protocol Analysis**: V2 vs V3 usage pattern comparison

### Robust Data Processing
- **Error Handling**: Comprehensive retry logic and fallback mechanisms
- **Rate Limiting**: Respects API constraints with exponential backoff
- **Data Validation**: Handles missing data and edge cases gracefully
- **Scalability**: Efficient processing of large wallet datasets

## Score Interpretation

| Score Range | Risk Level | Description |
|-------------|------------|-------------|
| 0-149 | Very Low | Highly reliable, sophisticated users with excellent risk management |
| 150-299 | Low | Responsible users with minor risk factors |
| 300-499 | Medium | Typical DeFi users with moderate risk exposure |
| 500-699 | High | Elevated risk requiring monitoring and potential intervention |
| 700-1000 | Very High | Critical risk, high liquidation probability, potential exploitation |

## Key Assumptions

- **Liquidations are negative**: Indicate poor risk management
- **Consistent activity is positive**: Shows engaged, reliable users
- **High failure rates are negative**: Suggest poor transaction management
- **Diverse interactions are positive**: Indicate sophisticated users
- **Volume and duration matter**: Larger, longer-term users are more reliable
- **Bot-like behavior is negative**: Suggests potential manipulation

## Comparison with Aave V2 Method

### Aave V2 Credit Scoring System

The companion Aave V2 system uses a different approach optimized for credit assessment:

#### Key Differences

| Aspect | Compound System | Aave V2 System |
|--------|----------------|----------------|
| **Objective** | Risk Assessment | Credit Scoring |
| **Score Range** | 0-1000 (lower = less risky) | 0-1000 (higher = better credit) |
| **Methodology** | Multi-component risk model | Hybrid rule-based + ML |
| **Primary Focus** | Liquidation risk prevention | Creditworthiness evaluation |
| **ML Integration** | Feature-based scoring | Random Forest + Rule-based |

#### Aave V2 Features
- **Transaction Metrics**: Volume, frequency, asset diversity
- **Behavioral Patterns**: Deposit/borrow ratios, repayment consistency
- **Risk Indicators**: Liquidation history, bot detection
- **Credit Factors**: Debt management, portfolio diversification

### When to Use Each System

- **Compound System**: Risk management, liquidation prediction, portfolio assessment
- **Aave V2 System**: Credit evaluation, loan approval, user classification

Both systems complement each other and can be used together for comprehensive DeFi user analysis.

## Technical Notes

- **Token Decimal Handling**: Properly converts different token decimals (USDC: 6, ETH: 18, etc.)
- **API Rate Limiting**: Implements exponential backoff and retry logic
- **Memory Efficiency**: Processes large datasets without excessive memory usage
- **Cross-Platform**: Compatible with Windows, macOS, and Linux
- **Jupyter Support**: Optimized for notebook environments

## License

This project is open-source and available under the MIT License.
