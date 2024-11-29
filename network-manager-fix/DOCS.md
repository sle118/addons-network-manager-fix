# Network Manager Fix Add-on for Home Assistant

This Home Assistant add-on was developed to address an issue observed in certain setups where **excessive network activity** is generated by Home Assistant's mDNS system. The problem often arises in networks with **Unifi mDNS reflectors** or other multi-VLAN setups, where mDNS packets are reflected across VLANs, causing **name collisions** and resulting in excessive mDNS traffic.

## Problem Overview

In affected setups, mDNS collisions trigger **frequent requests per second**, causing unnecessary network noise. Analysis revealed that modifying the mDNS mode could mitigate this behavior. However, manual changes to the mDNS mode via `nmcli` or other tools were **not persistent**, as the Home Assistant Supervisor often resets the mDNS configuration.

---

## mDNS Modes of Operation

This add-on leverages the `nmcli` tool to manage mDNS settings. The following modes are available for mDNS:

- **`yes`**: Enables both hostname registration and resolution.
- **`no`**: Disables mDNS completely.
- **`resolve`**: Enables only resolution, without registration.
- **`default`**: Uses the global default setting for mDNS, as determined by the active DNS plugin.

Many users, including myself, have found that setting the mDNS mode to **`resolve`** significantly reduces network activity while preserving essential functionality for integrations like ESPHome.

---

## Add-on Functionality

This add-on monitors the **mDNS mode** on a user-specified network interface. If it detects that the mDNS mode has been reset to `yes`, the add-on:

1. **Changes the mDNS mode back to `resolve`.**
2. **Restarts the NetworkManager service** to apply the change.

The monitoring happens at regular intervals to ensure consistency.

---

## Disclaimer

This add-on is provided as-is and was developed to solve a specific issue in my Home Assistant setup. It may not work for all configurations or network environments. Use at your own discretion.

- Always back up your Home Assistant configuration before installing or modifying add-ons.
- This add-on modifies network settings; ensure you understand the implications for your network setup.
- The add-on requires `nmcli` and assumes your Home Assistant instance uses **NetworkManager** for managing network connections.

---

## Installation and Usage

1. Clone the repository containing this add-on to your Home Assistant environment:

   ```bash
   git clone https://github.com/sle118/network_manager_fix.git
   ```

2. Follow Home Assistant's [Add-on Installation Guide](https://www.home-assistant.io/addons) to install custom add-ons.
3. Configure the add-on by specifying the primary network interface in the add-on's `config.json` file.
4. Start the add-on. It will monitor and adjust the mDNS mode as needed.

---

## Future Enhancements

Planned improvements include:

- None for now.

---

## Credits

This add-on was inspired by community discussions and feedback from other Home Assistant users experiencing similar network flooding issues. Special thanks to the open-source community for their continuous support!