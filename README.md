# DORNE: Automated Trading & Research System

**DORNE** (Developmental Outlier Recognition Network Engine) is a Python system that researches, runs and reports on an end-of-day U.S. equity strategy. It trades a live Alpaca account every market day from a Linux server and posts its trades and results to a Discord community.

> The source code is private. This page describes how the system is built and how it works.

## At a glance

| | |
|---|---|
| **Status** | Live since October 2026 (v4); project started July 2026 |
| **Language** | Python (pandas, NumPy) |
| **Broker & data** | Alpaca API (orders and market data), Finviz (stock universe) |
| **Hosting** | DigitalOcean Ubuntu server, systemd services, running 24/7 |
| **Alerts** | Discord webhooks |
| **Built with** | Gemini (original model), Claude Code (v4 rebuild) |

## How it works

A scheduler reads each day's market hours from Alpaca's calendar, including holidays and early closes. It starts every job as a separate process, so one failure never stops the schedule.

| Time (ET) | Job |
|---|---|
| 9:10 AM | Sends market-on-open sell orders for the previous day's trades |
| 9:31 AM | Places the day's planned limit buys once the opening sales have filled |
| Every 5 min | Records fills and keeps the system's records in line with the broker |
| 3:45 PM | Takes a market snapshot, computes signals and sends market-on-close orders |
| 4:15 PM | Confirms closing fills, records daily equity and places next-day limit orders |
| 4:30 PM | Posts the daily status and weekly, monthly and yearly reports |
| 4:45 PM | Runs paper-trading copies of the strategy to compare against live results |
| Saturdays | Refreshes the ~900-stock universe and checks every ticker is tradable |

## Risk controls

- **No margin.** A drawdown brake shrinks position sizes as the account falls from its peak.
- **Hard 50% maximum-drawdown limit.** Every strategy change is accepted or rejected against it.
- **Dry-run by default.** Live trading needs an explicit setting, and an emergency stop file blocks all new buys.
- **Safe operations:** one order ID per day to prevent duplicates, job locks and retries, backed-up state files, and stock-split detection.

## Research process

- **75+ rounds of research** on 2008–2026 daily data.
- **Monte Carlo simulation** estimates the range of possible returns and the chance of a deep drawdown.
- **Out-of-sample checks:** an idea must hold up in both 2008–2020 and 2021–2026 before it is adopted. Most ideas are rejected.
- **Live-code verification:** a replay check confirms the live code produces the same signals and portfolio as the research code. A simulation runs the real job scripts against a fake broker.

## Monitoring & community

- **Discord server** with channels for server status, live trade alerts (posted after each fill) and performance reports (percent returns). A private channel holds full details.
- **Live dashboard:** a read-only 3D city view of the account, served over a private network.
- **Live vs. paper tracking:** paper copies of the strategy show whether live fills match what the research expects.

## Project history

- **July 2026:** original model built with Gemini. Daily scans ran on GitHub Actions with Databento market data.
- **October 2026:** rebuilt as DORNE v4 with Claude Code. Moved to a dedicated Linux server and live trading.

## My role

I direct the project. I set the goals and risk limits, propose research ideas, review code changes and approve each release before it goes live. I also deployed and run the server and built the Discord community. The code was written with AI coding tools (Gemini, then Claude Code).

## Join the community

Join the Discord server through the landing page: https://dorne101.carrd.co/

## Disclaimer

DORNE is a personal research project. Nothing here or in the Discord server is investment advice. Backtested and simulated results do not guarantee future performance.

