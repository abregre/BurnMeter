# upm - Uptime Monitor (BurnMeter)

## Description

`upm` is a lightweight, dependency-free fun(🥲) Bash script for monitoring system uptime and providing statistical analysis. It's designed to be run as a cron job to periodically log uptime data, which can then be analyzed to show statistics for the current day, week, or month.

## Features

*   **Uptime Logging**: Automatically logs system uptime with timestamps.
*   **Statistical Analysis**: Calculates and displays statistics like minimum, maximum, total, and average uptime.
*   **Burn Level Analysis**: A unique feature that provides a "Burn Level" to gauge system usage intensity over different periods.
*   **Flexible Reporting**: View uptime statistics for today, the last 7 days, or the last 30 days.
*   **Dependency-Free**: A single Bash script with no external dependencies.

## Configuration

The script stores its log and lock files in the `~/.upm` directory in your home folder.

*   **Log File**: `~/.upm/uptime.log`
*   **Lock File**: `~/.upm/uptime_monitor.lock`

## Installation

1.  **Create the log directory and file:**
    The script requires a directory in your home folder to store its data.
    ```bash
    mkdir -p ~/.upm
    touch ~/.upm/uptime.log
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
    @reboot /usr/local/bin/upm
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

*   **`--today`**: Show statistics for the current day.
    ```bash
    upm --today
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
Date       |Time    |Uptime
-----------|--------|------------------------
24/11/2025|10:00:05|1 day, 02:30
25/11/2025|10:00:01|2 days, 02:30
26/11/2025|10:00:06|3 days, 02:30
27/11/2025|09:05:01|00:15
28/11/2025|10:00:02|1 day, 01:10
29/11/2025|10:00:03|2 days, 01:10
30/11/2025|10:00:04|3 days, 01:10

=== UPTIME STATISTICS ===
Sample Size:   7 measurements
Total Uptime:  12 days, 09:45 (309.75h)
Average:       1 day, 18:15 (42.82h)
Minimum:       00:15
Maximum:       3 days, 02:30

=== BURN LEVEL ANALYSIS ===
Burn Level: SlightlyFried 🍳 (309h total uptime)
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