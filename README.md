# Attention-Bid-Bot

A high-performance automated bidding agent for real-time "Attention Economy" ad auctions. The bot competes in a PvP simulation where participants bid on video advertising opportunities to maximize ROI (points earned per ebuck spent).

> **Repository Note:** This is the final, refactored version of the bidding agent. The full development lifecycle — including iterative harness testing, category benchmarking, and parameter calibration — was conducted in the original development repository: [BotContest](https://github.com/boyrazcan33/BotContest). That repository is referenced here solely for context on the development process; everything needed to evaluate and run the bot is contained in this repository.

## Strategic Approach

### Value Estimation

The bot estimates the expected value of each auction round by combining multiple signals from the input data:

- **Category matching:** A cross-reference matrix scores how well the bot's advertising category aligns with the video's category. Weights were derived from observed point yields across harness runs.
- **Viewer demographics:** Age and gender multipliers adjust the estimate based on which demographic segments historically produced higher returns for each video category.
- **Interest alignment:** Viewer interests are weighted by relevance order (primary > secondary > tertiary) and cross-referenced against the video category.
- **Engagement ratio:** Comment-to-view ratio serves as a proxy for viewer engagement, scaling the base value accordingly.
- **View count brackets:** View counts are mapped to non-linear value brackets, reflecting the assignment's hint that "a niche video can be worth more per impression than a viral one."

### Bidding and Budget Management

- **Adaptive multiplier:** After every 100-round summary, the bot adjusts a global bid multiplier based on observed ROI — scaling down if overpaying, scaling up if too conservative.
- **Start bid ratio:** Dynamically tuned based on consecutive win/loss streaks to optimize tie-breaking without overspending.
- **Minimum spend enforcement:** The scoring formula penalizes spending below 30% of the budget. The bot tracks spend rate in real time and applies increasing urgency pressure as rounds progress, with a panic mode that activates if spending falls critically behind schedule.
- **Budget conservation:** When remaining funds drop below safety thresholds (15%, 5%), bid caps are reduced proportionally to avoid early elimination.

## Calibration Methodology

As stated in the assignment: *"Discovering this value curve through experimentation is part of the challenge."* The weight matrices (`VIDEO_CATEGORY_MATCH`, `AGE_MUL_MALE`, `AGE_MUL_FEMALE`) and the view count brackets are not arbitrary — they were calibrated empirically through iterative testing against the provided harness. Python was used as an offline analysis tool to process harness outputs and discover the value curves; the bot itself uses only pure Java with no external dependencies, as required by the assignment:

- **Category selection:** Harness test outputs were analyzed using Python scripts to identify the highest-performing categories. The top 3 candidates were then benchmarked in full-length harness runs, with "Video Games" consistently yielding the best results.
- **Weight tuning:** Starting from uniform weights, each matrix cell was adjusted based on observed win rates and point yields across the harness runs conducted in the [BotContest](https://github.com/boyrazcan33/BotContest) repository.
- **View brackets:** The non-monotonic value curve described in the assignment was mapped by systematically testing bid responses across different view count ranges and recording the resulting point awards.

These parameters are fixed at runtime by design — pre-calibrated weights ensure sub-1ms response times and avoid the risk of overfitting to noise during the live auction.

## Technical Specifications

- **Language:** Java 21
- **Architecture:** Single-threaded, event-loop based on stdin/stdout
- **Response time:** Sub-1ms average (well within the 40ms limit)
- **Dependencies:** None (pure JDK)
- **Heap usage:** Well within the 192MB constraint

## Build and Run

A pre-built `can-bot.jar` is included in the repository root.

### Prerequisites
- JDK 8 or higher

### Running with the Test Harness

1. Clone this repository:
   ```
   git clone https://github.com/boyrazcan33/CBbot.git
   ```

2. Create a bot subdirectory in the harness directory and copy the jar:
   ```
   mkdir /path/to/harness/can-bot
   cp CBbot/can-bot.jar /path/to/harness/can-bot/
   ```

3. Run the harness from its directory:
   ```
   cd /path/to/harness
   java -jar harness.jar
   ```

4. View the dashboard at `http://localhost:2026`

## Performance Benchmarks
Through empirical testing and analysis in competitive environments, the agent has demonstrated:

- Average ROI: ~0.55 (Value per Ebuck spent)
- Target Accuracy: Successfully optimized for high-yield sectors, specifically the Video Games category.
- Reliability: 100% compliance with budget utilization guardrails and time constraints.