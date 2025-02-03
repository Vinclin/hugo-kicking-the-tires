# hugo-kicking-the-tires

# Hugo Portfolio Site

This repository demonstrates how to build a basic portfolio website using [Hugo](https://gohugo.io/). The instructions below are based on the "Kicking the Tires" chapter and will guide you through installing Hugo, creating your site, building layouts, and generating content.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Creating Your Site](#creating-your-site)
- [Configuration](#configuration)
- [Building the Home Page](#building-the-home-page)
- [Running the Development Server](#running-the-development-server)
- [Creating Content Using Archetypes](#creating-content-using-archetypes)
- [Creating a Single Page Layout](#creating-a-single-page-layout)
- [Generating the Final Site Output](#generating-the-final-site-output)
- [Additional Experimentation](#additional-experimentation)
- [Wrapping Up](#wrapping-up)

---

## Prerequisites

- A basic understanding of the command line and text editors.
- [Hugo](https://gohugo.io/getting-started/installing/) installed on your system (the **extended** version is recommended for asset management).

---

## Installation

Hugo is available as a single binary and can be installed using a package manager or manually.

### Using a Package Manager

- **macOS (with Homebrew):**

  ```bash
  brew install hugo

 • Windows (with Chocolatey):

choco install -y hugo-extended

 • Linux (with Linuxbrew/Homebrew):

brew install hugo

Manual Installation

 1. Download the extended version for your operating system from the Hugo Releases page.
 2. Place the binary in a global location:
 • macOS/Linux: Copy the executable to /usr/local/bin.
 • Windows: Create a directory (e.g., C:\hugo\bin), copy hugo.exe there, and add that folder to your PATH.
 3. Verify your installation:

hugo version

Creating Your Site

Generate a new Hugo site with the following command: `hugo new site portfolio`

This command creates a portfolio directory with the following structure:

portfolio/
├── archetypes
│   └── default.md
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes

Directory Overview

- archetypes: Contains Markdown templates (archetypes) used when generating new content.
- config.toml: The main configuration file for site-wide settings.
- content: Stores all Markdown (or HTML) content pages.
- data: Holds auxiliary data files in YAML, JSON, or TOML.
- layouts: Contains templates that define the look and feel of your pages.
- static: For static assets such as CSS, JavaScript, and images.
- themes: For downloaded or custom themes.

Configuration

Open config.toml in your text editor and update it to reflect your site’s information. For example:

baseURL = "<http://example.org/>"
languageCode = "en-us"
title = "Brian's Portfolio"

The baseURL is used to build absolute URLs, while the title is available to your layouts via .Site.Title.

Building the Home Page

Creating the Layout

Hugo uses layouts to avoid duplicating common HTML code. Create a layout for the home page at layouts/index.html:

<!DOCTYPE html>
<html lang="en-US">
<head>
  <meta charset="utf-8">
  <title>{{ .Site.Title }}</title>
</head>
<body>
  <h1>{{ .Site.Title }}</h1>
  {{ .Content }}
</body>
</html>

Adding Content

Hugo will use the special file content/_index.md to provide content for the home page. Create this file with some sample Markdown content:

This is my portfolio.

On this site, you'll find:

- My biography
- My projects
- My résumé

Running the Development Server

Hugo includes a live-reloading development server. Run the following command to start it:

hugo server

Visit <http://localhost:1313> in your browser to see your site. Hugo automatically updates the browser when you modify any content or layout files.

Creating Content Using Archetypes

Hugo’s archetypes provide default front matter for new content files.

Example: Creating an “About” Page

 1. Generate the new page:

hugo new about.md

 2. Open content/about.md and update it. Change the draft status to false and add your content:

---

title: "About"
date: 2020-01-01T12:40:44-05:00
draft: false
---

This is my About page.

Creating a Single Page Layout

For individual content pages (like the About page), create a default single page layout.

 1. Create the directory:

mkdir -p layouts/_default/

 2. Copy the home page layout to a new file for single pages:

cp layouts/index.html layouts/_default/single.html

 3. Edit layouts/_default/single.html to include the page title:

<!DOCTYPE html>
<html lang="en-US">
<head>
  <meta charset="utf-8">
  <title>{{ .Site.Title }}</title>
</head>
<body>
  <h1>{{ .Site.Title }}</h1>
  <h2>{{ .Title }}</h2>
  {{ .Content }}
</body>
</html>

Now, when you navigate to <http://localhost:1313/about>, the About page will be rendered using this layout.

Generating the Final Site Output

When you’re ready to build your site’s static files for production, run: `hugo`

This command generates the site into a new directory called public/. If you need to clean out old files, use: `hugo --cleanDestinationDir`

To further optimize your site, you can minify the generated files: `hugo --cleanDestinationDir --minify`

Additional Experimentation
    • Draft Management: Change the draft field in your content files (or archetypes) to control which pages are built. For example, set draft: true to exclude a page from the build.
    • Creating More Content: Generate additional pages like a résumé: `hugo new resume.md`

Then, update content/resume.md by changing the title from “Resume” to “Résumé”, marking it as not a draft, and adding your content.

Wrapping Up

You have now:
- Installed and configured Hugo.
- Created a new site with a basic directory structure.
- Built a custom layout for the home page and single content pages.
- Generated content using Hugo’s archetypes.
- Launched a live-reloading development server.
- Generated your static site files ready for deployment.

For further customization and to reduce code duplication, consider extracting common elements into a reusable theme or partial templates. For more detailed information, refer to the Hugo Documentation.

Happy building with Hugo!
