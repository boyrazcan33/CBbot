git 
```markdown
# Attention-Bid-Bot

> **Note on Development History:** This repository is a final, refactored, and "clean" version of the bidding agent. The full development lifecycle—including extensive integration testing with the official harness, PvP bot benchmarks, and rigorous category-specific simulations—was conducted in the original development repository: [BotContest](https://github.com/boyrazcan33/BotContest). This codebase was migrated here to provide a streamlined, production-ready version for final review, which accounts for the concise commit history in this repository.

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

A pre-built `can-bot.jar` is included in the repository root. No build step is required to run the bot.

### Prerequisites
- **JDK 8** or higher
- **Git**

### Running with the Test Harness

1. **Clone this repository:**
   ```powershell
   git clone https://github.com/boyrazcan33/CBbot.git
   ```

2. **Extract the harness archive.** You should have a structure like:
   ```
   playtech2026-harness\
   └── harness.jar
   ```

3. **Create the bot subdirectory and copy the jar:**
   ```powershell
   mkdir C:\path\to\playtech2026-harness\can-bot
   Copy-Item CBbot\can-bot.jar C:\path\to\playtech2026-harness\can-bot\can-bot.jar
   ```

4. **Run the harness** from the harness directory:
   ```powershell
   cd C:\path\to\playtech2026-harness
   java -jar harness.jar
   ```

5. **View the live dashboard:**
   ```
   http://localhost:2026
   ```

### Building from Source (Optional)

If you wish to recompile the source code:

1. **Compile:**
   ```powershell
   javac -d . src\main\java\Main.java
   ```

2. **Package:**
   ```powershell
   jar cfm can-bot.jar src\main\resources\META-INF\MANIFEST.MF Main.class
   ```

3. **Run standalone:**
   ```powershell
   java Main 10000000
   ```

## 📈 Performance Benchmarks
Through empirical testing and analysis in competitive environments, the agent has demonstrated:

- Average ROI: ~0.55 (Value per Ebuck spent)
- Target Accuracy: Successfully optimized for high-yield sectors, specifically the Video Games category.
- Reliability: 100% compliance with budget utilization guardrails and time constraints.
```