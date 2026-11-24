# Forex Session Liquidity Ranges

![TradingView](https://img.shields.io/badge/platform-TradingView-131722?logo=tradingview&logoColor=white)
![Pine Script](https://img.shields.io/badge/Pine%20Script-v5-2962FF)
![License](https://img.shields.io/badge/license-Unlicensed-lightgrey)

A TradingView overlay indicator that highlights the Asia, London, and New York forex sessions and tracks each session's high and low liquidity levels.

The indicator draws a labeled box around the active session range, updates that range on every bar in the session, and optionally extends dashed lines to the right with the session's evolving high and low.

## Features

- **Three configurable forex sessions:** Asia, London, and New York
- **Custom session schedules:** Use TradingView session-string syntax
- **Timezone support:** New York, UTC, London, and Dhaka
- **Dynamic session ranges:** Boxes expand as session highs and lows change
- **Liquidity level lines:** Optional dashed extension of session high and low
- **Independent session colors:** Customize the fill and line color for every session
- **Overlay design:** Compatible with any chart while remaining on top of the price action
- **Resource limits:** Configured for up to 500 boxes, lines, and labels

## Preview

Add a TradingView chart screenshot here:

```text
![Forex Session Liquidity Ranges](docs/screenshot.png)
```

## Installation

1. Open [TradingView](https://www.tradingview.com/) and open a chart.
2. Open **Pine Editor** at the bottom of the chart.
3. Create a new indicator.
4. Copy the contents of [`si.pine`](./si.pine) into the editor.
5. Click **Save**, then **Add to chart**.

## Configuration

Open the indicator's **Settings** panel on the chart to configure it.

| Setting | Default | Description |
| --- | --- | --- |
| Timezone | `America/New_York` | Timezone used to determine session boundaries |
| Extend High/Low Liquidity Lines | `true` | Draws and extends dashed lines for the session high and low |
| Show Asia Session | `true` | Enables the Asia range |
| Asia Session | `2000-0000` | Asia session hours |
| Asia Color | Blue | Session box, border, label, and liquidity-line color |
| Show London Session | `true` | Enables the London range |
| London Session | `0200-0500` | London session hours |
| London Color | Teal | Session box, border, label, and liquidity-line color |
| Show New York Session | `true` | Enables the New York range |
| New York Session | `0700-1000` | New York session hours |
| New York Color | Purple | Session box, border, label, and liquidity-line color |

## Session Behavior

At the first bar of a configured session:

- A colored box is created for that session.
- The box starts at the current bar's high and low.
- A label is placed in the upper-left side of the box.
- Optional dashed liquidity lines are initialized at the same high and low.

While a session remains active:

- The box updates to include the highest high and lowest low reached so far.
- The box right edge follows the most recent session bar.
- Dashed liquidity lines follow the updated session high and low.

After a session ends, the lines continue only as needed. The script extends them while the session is active and for up to 150 bars after the session, but does not extend the box beyond the session.

## Supported Timezones

The indicator provides these timezone choices:

- `America/New_York`
- `UTC`
- `Europe/London`
- `Asia/Dhaka`

Changing the timezone shifts the interpretation of the configured session times. A timezone that follows daylight-saving time, such as `America/New_York` or `Europe/London`, is converted by TradingView according to exchange/timezone rules.

## Session Time Format

Session inputs use TradingView's `HHMM-HHMM` format:

```text
0200-0500
```

This example runs from 02:00 through 05:00 in the selected timezone.

Use `2000-0000` for a session that crosses midnight. A Sunday-through-Friday or other restricted weekday schedule can be entered with TradingView session syntax, for example:

```text
0200-0500:12345
```

In TradingView session syntax, the weekday suffix digits represent Monday (`1`) through Friday (`5`).

## Usage Tips

- Apply it to forex pairs or any intraday market that you want to analyze.
- Lower-timeframe charts produce narrower session ranges and more frequent updates.
- The default times represent a practical split of the major forex sessions, not trading recommendations.
- Use a timezone consistent with your strategy and broker session.
- Custom colors can visually distinguish overlapping sessions.

## Compatibility

- TradingView Pine Script `@version=5`
- Overlay indicator
- Intended for all chart timeframes
- Maximum object counts:
  - 500 boxes
  - 500 lines
  - 500 labels

The chart may remove older objects automatically when the configured limits are reached.

## Alerts

This version does not define `alertcondition()` events or pop-up alerts. It is a visual indicator only.

## Project Structure

```text
.
├── si.pine     # TradingView Pine Script indicator
└── README.md   # Documentation
```

## Contributing

Contributions are welcome. When proposing a change:

1. Fork the repository.
2. Create a focused feature or fix branch.
3. Test the Pine Script in TradingView on several symbols and timeframes.
4. Document any new inputs or changed behavior.
5. Open a pull request with a screenshot or short description of the result.

## Risk Disclaimer

This indicator is provided for educational and analytical purposes only. It is not financial advice, and it does not guarantee profitable trades. Forex and leveraged trading involve substantial risk. Always test behavior on historical data and demo accounts before using it in live trading.
