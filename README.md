# AI/Run CodeMie Documentation

This repository contains the official documentation for AI/Run CodeMie, an AI-powered development platform that enhances software development workflows through intelligent automation, code assistance, and seamless integration with development tools.

## Documentation Structure

The documentation is organized into two main sections:

### 📘 [User Guide](./docs/user-guide/)

Comprehensive guide for developers and users working with AI/Run CodeMie:

- **[Getting Started](./docs/user-guide/getting-started/)** - Introduction to the platform and initial setup
- **[Concepts](./docs/user-guide/concepts/)** - Understand projects, data sources, and integrations
- **[Working With Assistants](./docs/user-guide/assistants/)** - Create, configure, and manage AI assistants
- **[Workflows](./docs/user-guide/workflows/)** - Build and execute automated workflows
- **[Conversational Advice](./docs/user-guide/conversational-advice/)** - Tips for effective AI interactions
- **[AI Documentation](./docs/user-guide/ai-documentation/)** - AI-generated documentation features

### 🚀 [Deployment Guide](./docs/deployment-guide/aws/)

Technical documentation for platform administrators and DevOps teams deploying on AWS:

- **[Overview](./docs/deployment-guide/aws/01-overview.md)** - AWS deployment overview and planning
- **[Prerequisites](./docs/deployment-guide/aws/02-prerequisites.md)** - System requirements and preparation
- **[Architecture](./docs/deployment-guide/aws/03-architecture.md)** - Platform architecture details
- **[Infrastructure Deployment](./docs/deployment-guide/aws/04-infrastructure-deployment/)** - Deploy AWS infrastructure with Terraform
- **[Components Deployment](./docs/deployment-guide/aws/05-components-deployment/)** - Deploy platform components on EKS
- **[Post-Installation](./docs/deployment-guide/aws/06-post-installation.md)** - Configuration and verification
- **[AI Models Integration](./docs/deployment-guide/aws/07-ai-models-integration.md)** - Connect AI models and providers
- **[Updates](./docs/deployment-guide/aws/08-update.md)** - Update and maintenance procedures
- **[Extensions](./docs/deployment-guide/aws/09-extensions.md)** - Platform extensions and customizations
- **[FAQ](./docs/deployment-guide/aws/10-faq.md)** - Deployment troubleshooting

## Quick Start

### Prerequisites

- Node.js 18.0 or higher
- npm or yarn package manager

### Local Development

1. **Install dependencies:**

   ```bash
   npm install
   ```

2. **Start the development server:**

   ```bash
   npm start
   ```

   This will open the documentation site in your browser at `http://localhost:3000`.

3. **Build for production:**

   ```bash
   npm run build
   ```

   This generates static content into the `build` directory.

4. **Serve production build locally:**
   ```bash
   npm run serve
   ```

## Contributing

We welcome contributions to improve the documentation! Here's how you can help:

### Reporting Issues

Found a problem or have a suggestion? Please [open an issue](https://github.com/codemie-ai/docs/issues) with:

- Clear description of the issue or suggestion
- Relevant page or section
- Suggested improvements (if applicable)

### Making Changes

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improve-docs`)
3. Make your changes
4. Test locally (`npm start`)
5. Commit your changes (`git commit -m 'Improve documentation'`)
6. Push to your branch (`git push origin feature/improve-docs`)
7. Open a Pull Request

### Documentation Guidelines

- Use clear, concise language
- Include code examples where applicable
- Follow the existing structure and formatting
- Add images to appropriate directories (`docs/user-guide/images/` or `docs/deployment-guide/aws/images/`)
- Test all code examples before submitting
- Ensure all internal links work correctly
- Use relative paths for internal links

## Technology Stack

This documentation site is built with:

- [Docusaurus 3.9.2](https://docusaurus.io/) - Documentation framework
- [React 19](https://reactjs.org/) - UI library
- [TypeScript](https://www.typescriptlang.org/) - Type safety
- [Markdown](https://www.markdownguide.org/) - Content format
- [docusaurus-plugin-image-zoom](https://github.com/flexanalytics/plugin-image-zoom) - Image zoom functionality

## Project Structure

```text
docs/
├── .github/                  # GitHub workflows and configurations
│   ├── scripts/             # Validation scripts
│   └── workflows/           # CI/CD workflows
│       ├── documentation-pipeline.yml  # PR validation (commits, linting, build)
│       └── deploy.yml       # GitHub Pages deployment
├── docs/                     # Documentation content
│   ├── index.md             # Homepage/landing page
│   ├── user-guide/          # User guide content
│   │   ├── getting-started/ # Initial platform introduction
│   │   ├── concepts/        # Core concepts and fundamentals
│   │   ├── assistants/      # Assistant management guides
│   │   ├── workflows/       # Workflow automation guides
│   │   ├── conversational-advice/ # Tips and best practices
│   │   ├── ai-documentation/ # AI documentation features
│   │   └── images/          # User guide images (237 images)
│   └── deployment-guide/    # Deployment guide content
│       └── aws/             # AWS-specific deployment
│           ├── 01-overview.md
│           ├── 02-prerequisites.md
│           ├── 03-architecture.md
│           ├── 04-infrastructure-deployment/
│           ├── 05-components-deployment/
│           ├── 06-post-installation.md
│           ├── 07-ai-models-integration.md
│           ├── 08-update.md
│           ├── 09-extensions.md
│           ├── 10-faq.md
│           └── images/      # Deployment guide images
├── src/                      # Custom components and pages
│   ├── css/                 # Custom styling
│   │   └── custom.css
│   └── pages/               # Custom pages (if any)
├── static/                   # Static assets
│   └── img/                 # Site-wide images (logos, favicon)
├── docusaurus.config.ts     # Docusaurus configuration
├── sidebars.ts              # Sidebar structure configuration
├── package.json             # Dependencies and scripts
└── tsconfig.json            # TypeScript configuration
```

## CI/CD Workflows

This repository uses GitHub Actions for automated validation and deployment:

### Documentation Pipeline (`documentation-pipeline.yml`)

Runs on pull requests to ensure code quality:

- **Commit & PR Validation**: Validates commit messages and PR titles against pattern `EPMCDME-XXXX: Description`
- **Code Quality Checks**:
  - TypeScript type checking
  - ESLint validation
  - Prettier formatting check
  - Markdown linting
- **Build Verification**: Ensures documentation builds successfully

### GitHub Pages Deployment (`deploy.yml`)

Automatically deploys to GitHub Pages when changes are pushed to main:

- Builds the Docusaurus site
- Deploys to GitHub Pages
- Can be triggered manually via workflow_dispatch

## Available Scripts

- `npm start` - Start development server with hot reload
- `npm run build` - Build for production
- `npm run typecheck` - Run TypeScript type checking
- `npm run lint:eslint` - Run ESLint validation
- `npm run lint:prettier` - Check Prettier formatting
- `npm run lint:markdown` - Lint markdown files

## Working with Links

When creating links in documentation:

- **Internal Links**: Use relative paths without `.md` extension

  ```markdown
  [Link to Overview](./overview)
  [Link to Getting Started](../getting-started/)
  ```

- **Index Pages**: For directory index pages, use trailing slash

  ```markdown
  [Infrastructure Deployment](./infrastructure-deployment/)
  ```

- **Numbered Files**: Docusaurus automatically strips number prefixes (e.g., `01-overview.md` becomes `overview`)

  ```markdown
  <!-- File is 01-overview.md, but reference as: -->

  [Overview](./overview)
  ```

## Content Statistics

- **Total Pages**: 65+ markdown documents
- **User Guide**: 40+ articles covering platform usage
- **Deployment Guide**: 15+ articles for AWS deployment
- **Images**: 240+ screenshots and diagrams

## Development Notes

### Building the Documentation

The build process:

1. Validates all internal links
2. Compiles TypeScript configurations
3. Generates static HTML/CSS/JS
4. Creates optimized production bundle

Link validation is strict - broken links will fail the build. This ensures documentation integrity.

### Docusaurus Configuration

Key configuration files:

- `docusaurus.config.ts` - Site configuration, navbar, footer
- `sidebars.ts` - Sidebar navigation structure
- `src/css/custom.css` - Custom styling and theme

## Support

- **Documentation Issues**: [GitHub Issues](https://github.com/codemie-ai/docs/issues)
- **Platform Support**: Contact your system administrator or platform team

---

Built with ❤️ using [Docusaurus](https://docusaurus.io/)
