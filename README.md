# Slack Exporter 2022

A python slack exporter

- This is an improved fork of [zach-snell/slack-export](https://github.com/zach-snell/slack-export).
- Uses current Slack Bolt API (works as of 2022).
- Offered free of charge!

## Description

The included script _slack_export.py_ works with a provided token to export channels, private channels, direct messages
and multi-person messages.

This script finds all channels, private channels and direct messages that your user participates in, downloads the
complete history for those converations and writes each conversation out to seperate json files.

This user-centric history gathering is nice because the official Slack data exporter only exports public channels.

There may be limitations on what you can export based on the paid status of your Slack account.

This use of the API is blessed by Slack: https://slack.dev/bolt-python/concepts.

To use this script you need to create your own Slack app with proper set of permissions. Once it's done, app bot or user
token may be used as a parameters of this script.

## Dependencies

```
pip3 install -r requirements.txt
```

## Basic Usage

```
# Export all Channels and DMs
python slack_export.py --token xoxp-123...

# List the Channels and DMs available for export
python slack_export.py --token xoxp-123... --dryRun

# Prompt you to select the Channels and DMs to export
python slack_export.py --token xoxp-123... --prompt

# Generate a `slack_export.zip` file for use with slack-export-viewer
python slack_export.py --token xoxp-123... --zip slack_export
```

### Selecting Conversations to Export

This script exports **all** Channels and DMs by default.

To export only certain conversations, use one or more of the following arguments:

* `--publicChannels [CHANNEL_NAME [CHANNEL_NAME ...]]`\
  Export Public Channels\
  (optionally filtered by the given channel names)

* `--groups [GROUP_NAME [GROUP_NAME ...]]`\
  Export Private Channels and Group DMs\
  (optionally filtered by the given group names)

* `--directMessages [USER_NAME [USER_NAME ...]]`\
  Export 1:1 DMs\
  (optionally filtered by the given user names)

* `--prompt`\
  Prompt you to select the conversations to export\
  (Any channel/group/user names specified with the other arguments take precedence.)

### Examples

```
# Export only Public Channels
python slack_export.py --token xoxp-123... --publicChannels

# Export only the "General" and "Random" Public Channels
python slack_export.py --token xoxp-123... --publicChannels General Random

# Export only Private Channels and Group DMs
python slack_export.py --token xoxp-123... --groups

# Export only the "my_private_channel" Private Channel
python slack_export.py --token xoxp-123... --groups my_private_channel

# Export only 1:1 DMs
python slack_export.py --token xoxp-123... --directMessages

# Export only 1:1 DMs with jane_smith and john_doe
python slack_export.py --token xoxp-123... --directMessages jane_smith john_doe

# Export only Public/Private Channels and Group DMs (no 1:1 DMs)
python slack_export.py --token xoxp-123... --publicChannels --groups

# Export only 1:1 DMs with jane_smith and the Public Channels you select when prompted
python slack_export.py --token xoxp-123... --directMessages jane_smith --publicChannels --prompt
```

This script is provided in an as-is state and I guarantee no updates or quality of service at this time.

# Recommended related libraries

This is designed to function with [slack-export-viewer](https://github.com/hfaran/slack-export-viewer).

```
pip install slack-export-viewer
```

Then you can execute the viewer as documented

```
slack-export-viewer -z exports.zip
```
