<img align="left" width="90" height="100" src="icon/IA_logo.png">

# Tubeup on Github

A GitHub template for automatic VOD archiving to IA using Tubeup on Github, powered by GitHub Actions

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
[![Archive Video to IA](https://github.com/Andres9890/Tubeup-on-Github/actions/workflows/tubeup.yml/badge.svg)](https://github.com/Andres9890/Tubeup-on-Github/actions/workflows/tubeup.yml)

## Features

- Archive videos from various platforms to IA
- Manual workflow dispatch with custom URL input
- Automatic retry mechanism for failed uploads
- Metadata preservation
- Support for all yt-dlp compatible platforms
- Easy setup

## Quick Start

1. **Use this template** to create your own repository
2. **Add IA credentials** as repository secrets
3. **Run workflow** with video URL to archive
4. **Check Internet Archive** for the video

## Supported Video Platforms

Tubeup supports all platforms compatible with yt-dlp, including:

- YouTube
- Vimeo
- Twitch VODs
- X
- Instagram
- TikTok
- Dailymotion
- Facebook
[And a lot more](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md)

## How to Use

### start by

1. Create an Internet Archive account at [archive.org](https://archive.org)
2. Add your credentials as repository secrets:
   - `IA_EMAIL`: Your Internet Archive email
   - `IA_PASSWORD`: Your Internet Archive password

### Archiving Videos

1. Go to the "Actions" tab in your repository
2. Select "Archive Video to IA"
3. Click "Run workflow"
4. Enter the video URL you want to archive
5. Click "Run workflow" again

The workflow will:
- Download the video using yt-dlp
- Upload it to Internet Archive
- Preserve metadata and descriptions
- Create a permanent archive link

## Workflow Details

The GitHub Action workflow:

- Triggers on manual dispatch
- Can be triggered with custom video URLs
- Uses Python to install and run tubeup
- Installs ffmpeg for videos
- Caches dependencies for faster execution
- Authenticates with IA using secrets

## Configuration

### Required Secrets

Add these secrets in your repository settings:

```
IA_EMAIL=your_ia_email
IA_PASSWORD=your_ia_password
```

### Modifying the Workflow

Edit `.github/workflows/tubeup.yml` to customize:

- Add automatic triggering
- Modify tubeup parameters
- Add additional processing steps
- Change dependencies

### Default URL

The workflow uses this default URL for testing:
```yaml
default: 'https://youtu.be/dQw4w9WgXcQ'
```

You can change it by editing the workflow file

## Repository Structure

```
├── .github/
│   └── workflows/
│       └── tubeup.yml       # workflow
├── .gitattributes
├── LICENSE
└── README.md
```

## Advanced Usage

### Custom Tubeup Parameters

You can modify the workflow to put additional parameters to tubeup, for example:

```yaml
- name: Run tubeup
  run: |
    tubeup "${{ github.event.inputs.url }}" --metadata="creator:something" --title="something"
```

### Batch Processing

Create a text file with multiple URLs and modify the workflow to process them all:

```yaml
- name: Archive multiple videos
  run: |
    while IFS= read -r url; do
      tubeup "$url"
    done < urls.txt
```

## Troubleshooting

### YouTube Authentication Error

When downloading from YouTube you may see an error such as ``ERROR: [youtube]: Sign in to confirm you’re not a bot.``, YouTube is requesting a logged‑in session  
Pass cookies to **yt‑dlp** with `--cookies-from-browser` (recommended) or `--cookies path/to/cookies.txt`
See the yt‑dlp FAQ on [passing cookies](https://github.com/yt-dlp/yt-dlp/wiki/FAQ#how-do-i-pass-cookies-to-yt-dlp) and the guide on [exporting YouTube cookies](https://github.com/yt-dlp/yt-dlp/wiki/Extractors#exporting-youtube-cookies) for details

### Authentication Errors

- Verify your IA credentials
- Ensure secrets are properly set in the repo settings

### Download Failures

- Verify that the video URL is accessible
- Check if the platform is supported by yt-dlp
- Some websites may require cookies or authentication

### Upload Failures

- Internet Archive may have rate limits
- Large videos may or may not timeout

### Workflow Errors

- Check the workflow logs in the Actions tab
- [Submit an issue](https://github.com/Andres9890/Tubeup-on-Github/issues/new/choose)

## Content Guidelines

When using this tool, please:

- Respect copyright and platform terms of service
- Archive only content you have permission to preserve
- Follow Internet Archive's content guidelines
- Be mindful of privacy and sensitive content
Any videos uploaded with this tool are NOT my responsbility in any way

## Contributing

All contributions to the repo are welcome

## License

Tubeup on Github is licensed under the MIT License, see [`LICENSE`](LICENSE) for more details

## People of Honor

- [tubeup](https://github.com/bibanon/tubeup)
- [Internet Archive](https://archive.org)
- [GitHub Actions](https://github.com/features/actions)

## Support

If issues happen:

- Check the [Troubleshooting section](#troubleshooting) section
- Check the workflow logs
- Check the [tubeup documentation](https://github.com/bibanon/tubeup)
- Create an issue with the detailed error logs

---

Made with ❤️ and 🧻 by Andres99 using GitHub Actions
