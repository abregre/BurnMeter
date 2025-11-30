# upm - Uptime Monitor (BurnMeter)

## Description

`upm` is a lightweight, dependency-free fun(🥲) Bash script for monitoring system uptime and providing statistical analysis. It's designed to be run as a cron job to periodically log uptime data, which can then be analyzed to show statistics for the current day, week, or month. The script now includes sophisticated tracking across system reboots with daily accumulation and current session state management to provide accurate uptime measurements even across system restarts.

## Features

*   **Uptime Logging**: Automatically logs system uptime with timestamps.
*   **Multi-Boot Tracking**: Maintains uptime tracking across system reboots and multi-day sessions.
*   **Daily Accumulation**: Tracks accumulated uptime for each day, including time from previous boots.
*   **Session State Management**: Maintains state of current session to properly calculate incremental uptime.
*   **Statistical Analysis**: Calculates and displays statistics like daily, weekly, and monthly totals.
*   **Burn Level Analysis**: A unique feature that provides a "Burn Level" to gauge system usage intensity over different periods.
*   **Flexible Reporting**: View uptime statistics for today, the last 7 days, or the last 30 days.
*   **Dependency-Free**: A single Bash script with no external dependencies.

## Features to be Added

*   **Session Counting Daily**: Show total system sessions for the current day.
*   **Session Counting Weekly**: Show total system sessions for each day of the week.
*   **Enhanced Output Styling**: Improved formatting with better colors, tables, and visual indicators for all output types.

## Configuration

The script stores its log and state files in the `~/.upm` directory in your home folder.

*   **Log File**: `~/.upm/uptime.log`
*   **Daily Accumulator**: `~/.upm/daily_accumulator`
*   **Current Session State**: `~/.upm/current_session_state`

## Installation

1.  **Create the log directory and required files:**
    The script requires a directory in your home folder to store its data.
    ```bash
    mkdir -p ~/.upm
    touch ~/.upm/uptime.log
    touch ~/.upm/daily_accumulator
    touch ~/.upm/current_session_state
    ```

2.  **Make the script executable:**
    ```bash
    chmod +x upm
    ```

3.  **Place the script in your PATH:**
    For system-wide access, move the script to a directory in your `$PATH`.
    ```bash
    mv upm /usr/local/bin/
    ```

4.  **Set up a cron job for logging:**
    The script is intended to log uptime automatically. Add a cron job to run the `upm` command at your desired frequency. For example, to log uptime every 5 minutes, edit your crontab (`crontab -e`) and add the following line:

    ```crontab
    */5 * * * * /usr/local/bin/upm
    ```

## Usage

### Logging Uptime

To log the current uptime manually, run the script without any arguments:
```bash
upm
```

### Viewing Statistics

To view uptime statistics, use the following flags:

*   **`--day`**: Show statistics for the current day.
    ```bash
    upm --day
    ```
*   **`--week`**: Show statistics for the last 7 days.
    ```bash
    upm --week
    ```
*   **`--month`**: Show statistics for the last 30 days.
    ```bash
    upm --month
    ```

### Example Output
```
$ upm --week
2025-01-01 02:30:00 FreshUser 🟢
2025-01-02 05:45:30 CoffeeMode ☕
2025-01-03 08:20:15 SlightlyFried 🍳
2025-01-04 01:10:05 FreshUser 🟢
2025-01-05 03:30:45 CoffeeMode ☕
2025-01-06 07:20:30 SlightlyFried 🍳
2025-01-07 12:45:20 BurnoutImminent 🔥

Weekly Total: 39:12:25 - BurnoutImminent 🔥

$ upm --day
Today (2025-01-07): 12:45:20 - BurnoutImminent 🔥

$ upm --month
Week 1: 45:30:15 - SlightlyFried 🍳
Week 2: 62:15:40 - BurnoutImminent 🔥
Week 3: 38:45:25 - CoffeeMode ☕
Week 4: 52:20:35 - BurnoutImminent 🔥

Monthly Total: 198:51:55 - FullyCooked 💀
```

## Burn Levels

The "Burn Level" is a fun, at-a-glance indicator of your system's uptime intensity. It's calculated based on the total uptime over a given period.

| Level | Name              | Daily Threshold | Weekly Threshold | Monthly Threshold |
| :---: | ----------------- | :-------------: | :--------------: | :---------------: |
|   1   | FreshUser 🟢      |     0-2 hrs     |     0-14 hrs     |      0-60 hrs     |
|   2   | CoffeeMode ☕     |     2-6 hrs     |    14-42 hrs     |     60-180 hrs    |
|   3   | SlightlyFried 🍳  |    6-10 hrs     |    42-70 hrs     |    180-300 hrs    |
|   4   | BurnoutImminent 🔥 |    10-14 hrs    |    70-98 hrs     |    300-420 hrs    |
|   5   | FullyCooked 💀    |     >14 hrs     |     >98 hrs      |     >420 hrs      |

## Contributing

Contributions are welcome! Please feel free to open an issue to report a bug or suggest a feature, or submit a pull request with your improvements.

## License

This project is licensed under the MIT License.