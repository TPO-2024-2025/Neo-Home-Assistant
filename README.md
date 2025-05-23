# NEO Smartbox Integration

This integration allows you to control your NEO Smartbox device through Home Assistant.

## Features

- Remote control of your NEO Smartbox device
- Custom remote control card for easy access to all functions
- Device actions for automation
- Service calls for programmatic control

## Installation

This integration is available through HACS (Home Assistant Community Store). To install:

1. Open HACS in Home Assistant
2. In the top right corner, click on the three dots and select "Custom repositories".
3. Add the repository URL: `https://github.com/TPO-2024-2025/Neo-Home-Assistant`.
4. Select "Integration" as the type.
5. Click "Add" to save the repository.
6. Search for "NEO Smartbox" in HACS and install the integration.
7. Restart Home Assistant to apply the changes.

## Configuration

1. Go to **Settings** > **Devices & services**.
2. Click on "Add Integration" and search for "NEO Smartbox".
3. Follow the prompts to set up the integration, including entering your NEO Smartbox API key. You can find your API key here: [https://neo.io/auth/home-assistant/api-key](https://neo.io/auth/home-assistant/api-key).
4. Once the integration is set up, you will see your NEO Smartbox device listed in Home Assistant.

## Using the Remote Control Card

The integration adds a custom card for your dashboard that provides an intuitive remote control interface.

### Adding the Card to Your Dashboard:

1. Edit your dashboard
2. Click "Add Card"
3. Scroll down to "Custom: NEO Smartbox Remote Card"
4. Configure the card with your remote entity:

```yaml
type: 'custom:neo-smartbox-remote-card'
entity: remote.neo_smartbox_remote
```

### Manual Resource Addition

If the card doesn't appear in your card picker, you may need to add the resource manually:

1. Go to **Configuration** > **Lovelace Dashboards** > **Resources**
2. Add a new resource with:
   - URL: `/static/neo_smartbox-card.js`
   - Type: JavaScript Module

## Device Actions

The integration provides device actions that can be used in automations. Available actions include:

- All remote control buttons (with both normal and long-press variants)
- Power control
- Navigation (up, down, left, right, ok)
- Media control (play, pause, etc.)

## Services

The integration provides the following services:

### `neo_smartbox.remote_key_action`

Send a remote key action to your NEO Smartbox.

| Service Data | Description                                                |
| ------------ | ---------------------------------------------------------- |
| `device_id`  | The ID of the device to control                            |
| `action`     | The action to perform (from the list of available actions) |
| `long_press` | Whether to perform a long press (default: false)           |

Example service call:

```yaml
service: neo_smartbox.remote_key_action
data:
  device_id: your_device_id
  action: POWER
  long_press: false
```

## Technical Details

The NEO Smartbox integration includes:

1. Custom lovelace card: `neo-smartbox-remote-card.js`
2. Frontend resources management
3. Device actions for automation
4. Remote platform implementation

## Troubleshooting

If you encounter issues:

1. Check that the card resource is properly loaded in your Lovelace resources
2. Verify that your device is properly connected and shows as available
3. Check Home Assistant logs for any error messages

## Development

For developers extending this integration:

- Frontend card source is in: `frontend/card/neo-smartbox-remote-card.js`
- Device actions are defined in: `device_action.py`
- Main API implementation is in: `remote.py`
