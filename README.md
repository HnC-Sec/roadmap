# Hard Way Hacking and Coding

This repository holds the static site for Hard Way Hacking and Coding, and contains all of the information for the FAQ and cybersecurity roadmap.

## Repository Structure

This repository is organized as follows:

```
/
├── roadmap/                 # Hugo site root directory
│   ├── hugo.yaml           # Hugo configuration file
│   ├── go.mod              # Go module file for theme dependencies
│   ├── go.sum              # Go module checksums
│   ├── content/            # Site content (Markdown files)
│   │   ├── _index.md       # Homepage content
│   │   ├── faq/           # FAQ section
│   │   ├── roadmap/       # Roadmap section
│   │   └── images/        # Static images
│   ├── archetypes/        # Content templates for new pages
│   │   └── default.md     # Default page template
│   └── i18n/              # Internationalization files
│       └── en.yaml        # English translations
├── .github/               # GitHub workflows and configuration
├── .devcontainer/         # Development container configuration
└── README.md              # This file
```

## Working with Hugo

This site is built using [Hugo](https://gohugo.io/), a fast and flexible static site generator written in Go.

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended version recommended)
- [Go](https://golang.org/doc/install) (for theme modules)

### Using the Development Container (Recommended)

This repository includes a preconfigured development container that provides everything you need to work with the site without installing dependencies locally.

**Requirements:**
- [Docker](https://docs.docker.com/get-docker/) or [Podman](https://podman.io/getting-started/installation)
- [VS Code](https://code.visualstudio.com/) with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

**Getting Started:**
1. Clone this repository
2. Open the repository in VS Code
3. When prompted, click "Reopen in Container" or use the command palette (`Ctrl+Shift+P`) and select "Dev Containers: Reopen in Container"
4. The container will automatically build with:
   - Go 1.24 (Debian Bookworm base)
   - Hugo (latest version)
   - Git and common development tools
   - All necessary dependencies preconfigured

**Benefits:**
- ✅ Consistent development environment across all machines
- ✅ No need to install Hugo, Go, or other dependencies locally
- ✅ Isolated environment that doesn't affect your local system
- ✅ Pre-configured with all necessary tools and extensions

### Building and Testing

To work with the site locally:

1. **Navigate to the Hugo directory:**
   ```bash
   cd roadmap/
   ```

2. **Install dependencies:**
   ```bash
   hugo mod tidy
   ```

3. **Start the development server:**
   ```bash
   hugo server --bind 0.0.0.0 --port 1313
   ```
   The site will be available at `http://localhost:1313`

### Adding Content

- Create new pages using Hugo archetypes: `hugo new content/section/page.md`
- Edit existing content in the `content/` directory
- Static assets go in the `content/images/` directory

## Theme and Documentation

This site uses the **Hextra** theme, a modern and feature-rich Hugo theme designed for documentation sites.

### Documentation Links

- **Hugo Official Documentation:** https://gohugo.io/documentation/
- **Hextra Theme Documentation:** https://imfing.github.io/hextra/
- **Hextra GitHub Repository:** https://github.com/imfing/hextra
- **Hugo Content Management:** https://gohugo.io/content-management/
- **Hugo Configuration:** https://gohugo.io/getting-started/configuration/

## Contributing

We welcome contributions to improve the Hard Way Hacking and Coding site! Whether you want to fix a typo, add new content, or suggest improvements, your contributions are valued.

### Contribution Process

1. **Fork the Repository**
   - Click the "Fork" button on the [GitHub repository page](https://github.com/hnc-sec/roadmap)
   - Clone your forked repository to your local machine:
     ```bash
     git clone https://github.com/YOUR-USERNAME/roadmap.git
     cd roadmap
     ```

2. **Make Your Changes**
   - Create a new branch for your changes:
     ```bash
     git checkout -b your-feature-branch
     ```
   - Make your desired changes to the content, documentation, or site structure
   - Follow the existing content structure and formatting conventions
   - Ensure your changes align with the project's goals and style

3. **Test Your Changes Locally**
   - Use the development container (recommended) or install Hugo locally
   - Navigate to the `roadmap/` directory and start the development server:
     ```bash
     cd roadmap/
     hugo server --bind 0.0.0.0 --port 1313
     ```
   - Preview your changes at `http://localhost:1313`
   - Verify that:
     - All pages load correctly
     - Navigation works as expected
     - Content is properly formatted
     - Images and links are functional

4. **Open a Pull Request**
   - Commit your changes with clear, descriptive messages:
     ```bash
     git add .
     git commit -m "Add detailed description of your changes"
     git push origin your-feature-branch
     ```
   - Go to the original repository and click "New Pull Request"
   - Provide a clear title and detailed description of your changes
   - Include:
     - What was changed and why
     - Any new content or features added
     - Screenshots (if applicable)
     - Testing steps you performed

### Guidelines for Contributions

- **Content Quality**: Ensure all content is accurate, well-researched, and relevant to cybersecurity learning. If AI is used to generate content, it should be carefully reviewed to ensure that the information provided is accurate and does not include hallucinations or bias.
- **Formatting**: Follow Markdown best practices and maintain consistency with existing content
- **Images**: Optimize images for web use and place them in the appropriate `content/images/` directory
- **Links**: Verify that all internal and external links are working
- **Accessibility**: Consider accessibility best practices when adding content

### Questions or Issues?

If you have questions about contributing or encounter any issues:
- Open an issue on GitHub
- Join our [Discord community](https://discord.gg/MwVE6KffFK)
- Review existing issues and pull requests for guidance

Thank you for helping make Hard Way Hacking and Coding better for everyone! 🚀