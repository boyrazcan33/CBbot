# Attention-Bid-Bot

> **Note on Development History:** This repository is a final, refactored, and "clean" version of the bidding agent. The full development lifecycle—including extensive integration testing with the official harness, PvP bot benchmarks, and rigorous category-specific simulations—was conducted in the original development repository: [BotContest](https://github.com/boyrazcan33/BotContest). This codebase was migrated here to provide a streamlined, production-ready version for final review,
> which accounts for the concise commit history in this repository.

A high-performance automated bidding agent designed for real-time "Attention Economy" ad auctions. This project implements a data-driven strategy to maximize Return on Investment (ROI) through predictive modeling, empirical analysis, and adaptive budget management.

## 🧠 Strategic Approach

### 📊 Multi-Factor Value Estimation
The bot calculates the expected value of auction items by synthesizing multiple data points:
- **Demographic Targeting:** Maps viewer profiles (age, gender) against content categories using multi-dimensional multiplier matrices to predict engagement probability.
- **Interest Graph Analysis:** Cross-references viewer interest vectors with video metadata to identify high-affinity targets.
- **Engagement Scaling:** Adjusts base values using non-linear comment-to-view ratios, ensuring bids are prioritized for high-interaction content.

### 💰 Dynamic Bidding Logic
- **Adaptive Multipliers:** Analyzes real-time feedback from auction summaries to dynamically tune bidding aggressiveness (`globalMultiplier`).
- **Liquidity Management:** Implements a calculated "Urgency Factor" to ensure consistent spending and compliance with minimum budget utilization thresholds (35%) without compromising efficiency.
- **Tie-Breaker Optimization:** Utilizes calibrated entry-bid ratios to secure wins in highly competitive segments at the lowest possible cost.

## 🛠 Technical Specifications
- **Language:** Java 21 (LTS)
- **Architecture:** Single-threaded, low-latency event loop
- **Response Time:** Optimized for sub-40ms execution (averaging ~0ms in local benchmarks)
- **Dependencies:** Zero external libraries (Pure JDK implementation)

## 📦 Build & Execution

This project is designed to be built using standard JDK tools to ensure maximum compatibility across different environments.

### Prerequisites
- **JDK 21** or higher.

### Step-by-Step Instructions

1. **Clone the repository:**
   ```bash
   git clone https://github.com/boyrazcan33/CBbot.git
   cd CBbot
Compile the source code:
Using the standard Java compiler (javac):

Bash
javac -d . src/main/java/Main.java
Run the bot:
Provide the initial budget (e.g., 10,000,000) as a command-line argument:

Bash
java Main 10000000
Note: Upon starting, the bot will immediately output its chosen category (Video Games) to stdout as per protocol requirements.

📈 Performance Benchmarks
Through empirical testing and analysis in competitive environments, the agent has demonstrated:

Average ROI: ~0.55 (Value per Ebuck spent)

Target Accuracy: Successfully optimized for high-yield sectors, specifically the Video Games category.

Reliability: 100% compliance with budget utilization guardrails and time constraints.