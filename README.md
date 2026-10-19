# XLottery 🎲🌐

XLottery is a decentralized, provably fair multi-round lottery protocol built in Solidity. It utilizes **Chainlink VRF V2.5** to ensure verifiable, immutable randomness for winner selection on EVM networks.

---

## 🛠️ Key Features

- **Provable Randomness:** Native integration with Chainlink VRF V2.5 utilizing direct subscription and flexible payment support.
- **Multi-Round Architecture:** Dynamic round management where each cycle retains independent configurations, participation tracking, and state metrics.
- **Tiered Prize Distribution (50 / 30 / 20):** Proportional prize allocations for top three places, with automatic adjustments if unique participant thresholds fall below three.
- **Automated Refund Mechanism:** In the event that the minimum required player count (`minPlayers`) is not met by the end of a round's duration, the contract transitions to a refundable state, allowing participants to claim a full refund.
- **Configurable Parameters:** Flexible admin parameters per round including ticket pricing, round duration, maximum tickets allowed per address, and protocol fee percentage (capped at 10%).

---

## 🏗️ Protocol Architecture & Workflow

1. **Initialization:** The owner triggers `startNewRound()`, snapshotting the latest global configuration settings for the new round.
2. **Participation:** Users purchase tickets via `buyTickets(quantity)`. Any excess ETH sent beyond the required amount is immediately refunded using the Checks-Effects-Interactions (CEI) pattern.
3. **Draw Trigger:** Once a round's duration expires, any user can execute `requestDraw(roundId)`:
   - If `minPlayers` is met, the round enters the `CALCULATING` state and requests random words from Chainlink VRF.
   - If participant conditions are unmet, the round transitions to `CLOSED` with refunds enabled via `claimRefund(roundId)`.
4. **Prize Settlement:** Chainlink VRF invokes `fulfillRandomWords()`, which selects unique winners, deducts protocol fees, and distributes prizes atomically.

---

## 📂 Project Structure

```text
.
├── src/
│   └── XLottery.sol          # Core smart contract
├── test/
│   └── XLottery.t.sol        # Comprehensive unit & integration test suite
├── foundry.toml              # Foundry environment configuration
```

---

## ⚙️ Prerequisites & Installation

Ensure you have [Foundry](https://getfoundry.sh/) installed:

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

Clone the repository and install dependencies:

```bash
git clone [https://github.com/Alexka-Dev/XLottery](https://github.com/Alexka-Dev/XLottery)
cd XLottery
forge install
```

---

## 🧪 Build & Testing

To compile the contracts:

```bash
forge build
```

To run the complete test suite:

```bash
forge test
```

To inspect detailed execution traces or code coverage:

```bash
# Run tests with verbose execution traces
forge test -vvvv

# Generate coverage report
forge coverage
```

---

## 📄 License

Distributed under the **MIT** License. See `LICENSE` for more details.

## Author

AlexkDev
