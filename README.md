# IPTV Stream Checker

## Overview

IPTV Stream Checker is a command-line tool originally by <a href="https://github.com/NewsGuyTor/IPTVChecker">NewsGuyTor</a> designed to check the status of channels in an IPTV M3U8 playlist. It verifies if the streams are alive, captures screenshots, provides detailed information about video and audio streams, and identifies any potential issues like low framerates or mislabeled channels. 

<strong>It also has some minor additions by Ron Mexico to include bitrate on channels utilizing ffmpeg to profile a channel over 10 seconds to capture an average variable bit-rate (VBR).</strong>

<img width="794" alt="screenshot" src="https://i.imgur.com/y1beux6.png">

## Features

- **Check Stream Status:** Verify if IPTV streams are alive or dead.
- **Split Playlist:** Split into separate playlists for working and dead channels.
- **Capture Screenshots:** Capture screenshots from live streams.
- **Group Filter:** Option to check specific groups within the M3U8 playlist.
- **Detailed Stream Info:** Retrieve and display video codec, resolution, framerate, and audio bitrate.
- **Low Framerate Detection:** Identifies and lists channels with framerates at 30fps or below.
- **Mislabeled Channel Detection:** Detects channels with resolutions that do not match their labels (e.g., "1080p" labeled as "4K").
- **Custom User-Agent:** Ron Mexico's version uses VLC as the user agent for HTTP requests.
- **BitRate Average Calculator:** Added by Ron Mexico, this will now profile and add an average of the variable bit-rate of the channel (VBR) utilizing ffmpeg to profile it over 10 seconds.
  

## Installation

### Prerequisites

- **Python 3.6+**
- **ffmpeg** and **ffprobe**: Required for capturing screenshots and retrieving stream information.

### Clone the Repository

```bash
git clone https://github.com/sudo-ronmexico/IPTVChecker-BitRate.git 
cd IPTVChecker-BitRate 
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

## Usage

### Basic Command

```bash
python IPTV_checker.py /path/to/your/playlist.m3u8
```

### Options

- **`-group` or `-g`**: Specify a group title to check within the playlist.
- **`-output` or `-o`**: Output file path e.g. ~/output/results.csv.
- **`-timeout` or `-t`**: Set a timeout in seconds for checking the channel status.
- **`-extended` or `-e [seconds]`**: Enable an extended timeout check for channels detected as dead. If specified without a value, defaults to 10 seconds. This option allows you to retry dead channels with a longer timeout.
- **`-split` or `-s`**: Create separate playlists for working and dead channels.
- **`-rename` or `-r`**: Rename alive channels to include video and audio information in the playlist.
- **`-skip_screenshots`**: Skip capturing screenshots.
- **`-v`**: Increase output verbosity to `INFO` level.
- **`-vv`**: Increase output verbosity to `DEBUG` level.

### Examples

1. **Standard Check with Default Settings**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8
   ```

2. **Check a Specific Group**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8 -group "SPORT HD"
   ```

3. **Check with Extended Timeout**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8 -extended 30
   ```

4. **Split Playlist into Working and Dead Channels**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8 -split
   ```

5. **Rename Working Channels with Video and Audio Info**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8 -rename
   ```

6. **Split Playlist and Rename Working Channels**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8 -split -rename
   ```

7. **Enable Debug Mode for Detailed Output**:
   ```bash
   python IPTV_checker.py /path/to/your/playlist.m3u8 -vv
   ```
   
### Output Format

The script will output the status of each channel in the following format:

```bash
1/5 ✓ Channel Name | Video: 1080p60 H264 - Audio: 159 kbps AAC
```

### Low Framerate Channels

After processing, the script lists any channels with framerates of 30fps or below:

```bash
Low Framerate Channels:
1/5 EGGBALL TV HD - 25fps
```

### Mislabeled Channels

The script also detects channels with incorrect labels:

```bash
Mislabeled Channels:
3/5 Sports5 FHD - Expected 1080p, got 4K
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an issue if you have any ideas or feedback.
