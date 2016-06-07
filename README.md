# Battery Status Plugin

The BatteryStatus plugin allows you to get battery status information.

## How to use

- Import the plugin to your project as explained [here](https://github.com/cobaltians/cobalt/wiki/Plugins-usage)
- Add the `cobalt.batteryStatus.js` to your web JS folder
- Add a html `<link>` to the `cobalt.batteryStatus.js` file after the cobalt link in the `<head>` tag

## Getting the battery state

Use the `cobalt.batteryStatus.getState` shortcut:

    // Somewhere after cobalt initialized
    cobalt.batteryStatus.getState(function (state) {
      cobalt.log('The battery is currently ', state);

      if (state === cobalt.batteryStatus.state.CHARGING) {
        // Do heavy calculations
      }
    });

Possible battery states are listed in the `cobalt.batteryStatus.state` enum:

| Enum field | Value | Description |
|------------|-------|-------------|
| FULL | `full` | Battery is charging and full |
| CHARGING | `charging` | Battery is charging |
| DISCHARGING | `discharging` | Battery is discharging |
| LOW | `low` | Device is on power saving mode (Android Lollipop, iOS 9 and higher) |
| UNKNOWN | `unknown` | The battery state could not be retrieved |

## Be warned of state changes

The web can also subscribe to battery state changes:

    // First, set the callback function
    cobalt.batteryStatus.onStateChanged = function (state) {
      cobalt.log('Battery state changed: ', state);
    };

    // Then, start listening to changes
    cobalt.batteryStatus.startMonitoring();

    // Later on, you can stop listening
    cobalt.batteryStatus.stopMonitoring();

Alternatively, you can set the callback and start listening at the same time:

    cobalt.batteryStatus.startMonitoring(function (state) {
      cobalt.log('Battery status changed: ', state);
    });

*Note*: you can only have one callback defined for each page. Using the shortcut above will simply set `cobalt.batteryStatus.onStateChanged`.

## Getting the battery level

Additionnaly, you can get the battery level as percentage:

    cobalt.batteryStatus.getLevel(function (level) {
      cobalt.log('Battery level: ', level, '%');
    });

If the battery level could not be retrieved, the value `-1` is returned. Also, on some devices the battery level may be rounded; for example by 5% on iOS 7 devices.

*Note*: you should not rely on the battery level to trigger actions in your application. Instead, use the battery state.

## Want more?

If you have any ideas or improvements to propose, please feel free to do so in the issue tracker!
