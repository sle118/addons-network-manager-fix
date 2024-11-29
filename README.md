# Network Manager Fix Add-on

The **Network Manager Fix Add-on** is designed to address network flooding issues in Home Assistant caused by excessive mDNS traffic. It monitors and ensures the mDNS mode is set to `resolve`, preventing unwanted network activity while maintaining critical functionality for integrations like ESPHome.

## Features

- Automatically monitors and adjusts the mDNS mode for a specified network interface.
- Ensures changes are persistent by resetting mDNS mode if overridden by Home Assistant Supervisor.
- Simple configuration through the Home Assistant add-on interface.

## Why Use This Add-on?

Certain network configurations, such as those using **Unifi mDNS reflectors** or multi-VLAN setups, may lead to name collisions, causing Home Assistant's mDNS system to generate excessive traffic. This add-on ensures your mDNS mode stays in the desired state (`resolve`) to prevent these issues.

## Installation

1. Add this repository to your Home Assistant instance:

   ```text
   https://github.com/sle118/addons-network-manager-fix.git
   ```

2. Install the add-on from the Add-on Store.

3. Configure the add-on through the UI or by editing the options.
4. Start the add-on and check the logs for confirmation of operation.

## Configuration

The following options are available:

```yaml
primary_interface: ""  
check_interval: 30
```

- **`primary_interface`** : Specify the network interface to monitor and adjust (e.g.,`enp0s3`). If left empty, the add-on will attempt to detect the primary interface automatically.
- **`check_interval`** : The interval (in seconds) at which the add-on checks and adjusts the mDNS mode.

## Documentation

For more detailed documentation, including troubleshooting steps and examples, see the [DOCS.md]() file.

## Support

This add-on is provided as-is. If you encounter any issues or have feature requests, please open an issue in the [GitHub repository]().

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.
