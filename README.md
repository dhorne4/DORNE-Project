# DORNE: Automated Trading & Research System

**DORNE** (Developmental Outlier Recognition Network Engine) is a personal project. It's a Python system that researches, runs and reports on a rules-based U.S. equity strategy. It manages a live brokerage account automatically and shares trade alerts and results with a Discord community.

> The source code and strategy details are private.

## At a glance

| | |
|---|---|
| **Status** | Live since October 2026; project started July 2026 |
| **Language** | Python (pandas, NumPy) |
| **Broker** | Alpaca API |
| **Hosting** | Linux cloud server, running 24/7 |
| **Alerts** | Discord webhooks |
| **Built with** | Gemini (original model), Claude Code (current version) |

## What it does

- **Research:** tests trading ideas on many years of historical market data before any of them go live.
- **Trading:** runs on a fixed daily schedule, makes its decisions automatically and places orders through the broker's API.
- **Record-keeping:** records every fill and checks its own records against the broker's.
- **Reporting:** posts trade alerts and regular performance reports to Discord and shows the account on a live dashboard.

## Built to be reliable

- Each job runs on its own, so one failure doesn't stop the rest.
- Safeguards prevent duplicate orders, and the system retries automatically and keeps backups of its records.
- It starts in a safe test mode. Live trading needs an explicit setting, and an emergency stop blocks new trades.
- Built-in risk limits shrink positions during losing stretches.

## Research process

- **75+ rounds of research** so far.
- **Monte Carlo simulation** estimates the range of possible outcomes, including worst-case losses.
- **An idea must hold up across different market periods** before it's adopted. Most are rejected.
- **Checks confirm the live code behaves exactly like the research code.**

## Project history

- **July 2026:** original model built with Gemini, running on GitHub Actions.
- **October 2026:** rebuilt with Claude Code into a live system on a dedicated Linux server.

## My role

I created the original model with Gemini, then rebuilt it into a live system with Claude Code. I propose ideas to test, analyze the results, review any code written for updates, and approve every release before it goes live. I also deployed and run the server, and I built the Discord community.

## Join the community

Join the Discord server through the landing page: https://dorne101.carrd.co/

## Disclaimer

DORNE is a personal research project. Nothing here or in the Discord server is investment advice. Backtested and simulated results do not guarantee future performance.

