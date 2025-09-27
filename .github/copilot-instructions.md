# Copilot Coding Agent Instructions

## Repository Summary

This repository hosts a **Hugo-based static website** for "Hard Way Hacking and Coding", a cybersecurity learning community. The site contains educational content including a cybersecurity roadmap and FAQ sections to help newcomers learn security concepts and programming.

## High-Level Repository Information

- **Type**: Static website using Hugo (Go-based static site generator)
- **Size**: Small repository (~20 files, focused on content)
- **Primary Language**: Markdown (content) with Go modules for theme dependencies
- **Framework**: Hugo v0.147.7 with Hextra theme
- **Target Runtime**: Static HTML/CSS/JS served via GitHub Pages
- **Theme**: Hextra (modern documentation theme)

## Build Instructions

### Prerequisites
Always install these dependencies before working with the site:

```bash
# Install Hugo (Extended version required)
HUGO_VERSION=0.147.7
wget -O /tmp/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb
sudo dpkg -i /tmp/hugo.deb

# Verify installation
hugo version  # Should show v0.147.7+extended
go version    # Go 1.22+ required for theme modules
```

### Build Process
**ALWAYS** run commands from the `roadmap/` subdirectory (not the repository root):

```bash
# Navigate to Hugo site directory
cd roadmap/

# CRITICAL: Always run this first to download theme dependencies
hugo mod tidy

# Development server (local testing)
hugo server --bind 0.0.0.0 --port 1313
# Access at http://localhost:1313

# Production build
HUGO_ENVIRONMENT=production HUGO_ENV=production hugo --gc --minify
```

### Known Build Issues & Workarounds

1. **Network Dependency Error**: Hugo may fail with FlexSearch CDN errors:
   ```
   ERROR Could not retrieve FlexSearch js file from https://cdn.jsdelivr.net/npm/flexsearch
   ```
   **Workaround**: The build still completes successfully and generates all files in `public/` directory. This error can be safely ignored in offline environments.

2. **Theme Dependencies**: Always run `hugo mod tidy` before any build operation to ensure theme modules are properly downloaded.

3. **Build Timing**: 
   - `hugo mod tidy`: ~1 second (after initial download)
   - `hugo server`: ~2-3 seconds to start
   - `hugo build`: ~100ms for production build

### Testing Changes
```bash
cd roadmap/

# Test local development
hugo server --bind 0.0.0.0 --port 1313

# Verify build works
hugo --gc --minify

# Check generated files
ls -la public/  # Should contain index.html and all site assets
```

## Project Layout & Architecture

### Directory Structure
```
/
├── .github/                    # GitHub workflows and configuration
│   ├── dependabot.yml         # Dependency updates for devcontainer
│   └── workflows/pages.yml    # GitHub Pages deployment
├── .devcontainer/             # VS Code development container
│   └── devcontainer.json     # Go 1.24 + Hugo environment
├── roadmap/                   # Hugo site root (WORK HERE)
│   ├── hugo.yaml             # Main Hugo configuration
│   ├── go.mod/go.sum         # Go module files for Hextra theme
│   ├── content/              # All site content (Markdown)
│   │   ├── _index.md         # Homepage content
│   │   ├── faq/              # FAQ section
│   │   ├── roadmap/          # Learning roadmap content
│   │   └── images/           # Static images and assets
│   ├── archetypes/           # Content templates
│   │   └── default.md        # Default page template
│   ├── i18n/                 # Internationalization
│   │   └── en.yaml           # English translations
│   └── public/               # Generated site (ignored by git)
├── README.md                  # Repository documentation
└── LICENSE                   # MIT License
```

### Key Configuration Files

1. **`roadmap/hugo.yaml`**: Main site configuration
   - Base URL: https://faq.hackncode.dev/
   - Theme: Hextra (github.com/imfing/hextra)
   - Navigation menu structure
   - Site metadata and copyright

2. **`roadmap/go.mod`**: Theme dependency management
   - Go version: 1.24.5
   - Hextra theme version: v0.11.1

3. **`.github/workflows/pages.yml`**: Automated deployment
   - Triggers on pushes to main branch
   - Uses Hugo v0.147.7 and Go 1.22
   - Builds from `roadmap/` directory
   - Deploys to GitHub Pages

### Content Organization

- **Homepage** (`content/_index.md`): Welcome page with navigation cards
- **Roadmap** (`content/roadmap/_index.md`): Comprehensive cybersecurity learning path
- **FAQ** (`content/faq/_index.md`): Common questions from Discord community
- **Static Assets** (`content/images/`): Icons, images, and other assets

### Validation Pipeline

The repository uses GitHub Actions for continuous deployment:
1. **Build Job**: Downloads Hugo, sets up Go, runs `hugo mod tidy`, builds site
2. **Deploy Job**: Uploads to GitHub Pages
3. **Dependencies**: Dependabot monitors devcontainer updates

### Manual Validation Steps

After making changes, always verify:
```bash
cd roadmap/
hugo server --bind 0.0.0.0 --port 1313

# Check these in browser at localhost:1313:
# - All pages load correctly
# - Navigation works as expected  
# - Content is properly formatted
# - Images and links are functional
# - No broken internal links
```

### Development Environment Options

1. **Recommended**: Use VS Code with Dev Containers extension
   - Pre-configured with Go 1.24 and Hugo
   - Consistent environment across machines
   - No local dependency installation needed

2. **Local Setup**: Install Hugo Extended + Go locally
   - Follow prerequisites section above
   - Requires manual dependency management

### Dependencies & Relationships

- **Hugo Extended** (v0.147.7): Required for SCSS processing in theme
- **Go** (1.22+): Required for Hugo module system and theme downloads
- **Hextra Theme**: Modern documentation theme with search functionality
- **FlexSearch**: Client-side search (loaded from CDN, optional)

### Common File Locations

- Site content: `roadmap/content/`
- Configuration: `roadmap/hugo.yaml`
- Theme settings: `roadmap/go.mod`
- Build output: `roadmap/public/` (generated, not committed)
- Page templates: Provided by Hextra theme
- Custom archetype: `roadmap/archetypes/default.md`

### Root Directory Files

- `README.md`: Comprehensive documentation with contribution guidelines
- `LICENSE`: MIT License for open source usage
- `.gitignore`: Excludes `public/` build directory

## Important Notes for Agents

1. **Working Directory**: Always work in `roadmap/` subdirectory, not repository root
2. **Build Dependencies**: Network access required for initial `hugo mod tidy`, but builds work offline afterward
3. **Error Tolerance**: FlexSearch CDN errors are non-fatal and can be ignored
4. **Content Format**: All content uses Markdown with Hugo front matter
5. **Theme Updates**: Use `hugo mod get -u` to update Hextra theme if needed
6. **Local Development**: Always test with `hugo server` before committing changes

Trust these instructions and only search for additional information if these details are incomplete or found to be incorrect.