# YouthMappers Labs

A GitHub Pages site showcasing public repositories and projects from YouthMappers chapters worldwide.

## Overview

This site automatically displays all public repositories from the [YouthMappers GitHub organization](https://github.com/youthmappers), including:
- Repository names and descriptions
- Programming languages used
- Star and fork counts
- Links to each repository
- Links to project websites (if available)

The site excludes the `.github` and `youthmappers.github.io` repositories from the listing.

## Deployment

The site is automatically deployed to GitHub Pages via GitHub Actions:
- On every push to the `main` branch
- **Weekly** every Monday at 00:00 UTC to refresh repository data
- Manually via workflow dispatch

**Live Site:** https://youthmappers.github.io

> Note: A custom domain (labs.youthmappers.org) can be configured in the future by adding a CNAME file.

## Features

- 📊 Live statistics showing total repositories, stars, and forks
- 🎨 Modern, responsive design that works on all devices
- 🔄 Real-time data fetched from GitHub API
- 🌟 Repositories sorted by popularity (stars)
- 🎯 Filters out archived repositories

## Technology Stack

- **Svelte** - Modern, reactive UI framework
- **Vite** - Fast build tool and dev server
- **GitHub Pages** for hosting
- **GitHub Actions** for automated deployment and weekly builds
- **GitHub API** for repository data

## Local Development

To view the site locally:

1. Clone this repository
2. Install dependencies: `npm install`
3. Run the development server: `npm run dev`
4. Open your browser to the URL shown (typically `http://localhost:5173`)

The site will fetch live data from the GitHub API.

### Build for Production

```bash
npm run build
```

This creates an optimized build in the `dist` directory.

## Contributing

This project is maintained by the YouthMappers organization. For questions or issues, please open an issue on this repository.
