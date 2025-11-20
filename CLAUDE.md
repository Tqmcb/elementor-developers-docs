# CLAUDE.md - Elementor Developers Documentation

> **Repository Context Guide for AI Assistants**
> This document provides comprehensive information about the Elementor Developers Docs repository structure, development workflows, and conventions to help AI assistants effectively navigate and contribute to this codebase.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Architecture & Technology Stack](#architecture--technology-stack)
3. [Directory Structure](#directory-structure)
4. [Development Workflow](#development-workflow)
5. [Documentation Conventions](#documentation-conventions)
6. [Sidebar Navigation System](#sidebar-navigation-system)
7. [Content Creation Guidelines](#content-creation-guidelines)
8. [Code Examples Standards](#code-examples-standards)
9. [Assets & Media](#assets--media)
10. [Build & Deployment](#build--deployment)
11. [Common Tasks & Recipes](#common-tasks--recipes)
12. [Important Considerations](#important-considerations)

---

## Project Overview

### Purpose
This repository contains the complete technical documentation for Elementor developers, covering how to extend Elementor through custom widgets, controls, dynamic tags, hooks, and addons.

### Key Facts
- **Site URL**: https://developers.elementor.com/docs/
- **GitHub Repository**: elementor/elementor-developers-docs
- **Primary Audience**: WordPress developers building Elementor extensions
- **Content Scope**: 292+ markdown files organized into 23 documentation sections
- **Total Content**: ~25,800+ lines of documentation

### Technology Stack
- **Framework**: VuePress v1.9.7 (Vue-powered static site generator)
- **Node Version**: v16.20.2 (specified in `.nvmrc`)
- **Package Manager**: npm/yarn
- **Build System**: VuePress with custom plugins

---

## Architecture & Technology Stack

### VuePress v1.9.7
Static site generator optimized for technical documentation with:
- Hot module replacement for development
- Vue-powered single-page application
- Automatic sidebar generation from configuration
- Built-in search functionality
- PWA support

### Dependencies

```json
{
  "devDependencies": {
    "vuepress": "^1.9.7",                      // Core framework
    "@vuepress/plugin-pwa": "^1.9.7",          // Progressive Web App support
    "vuepress-plugin-clean-urls": "^1.1.2",   // Clean URL routing (no .html)
    "vuepress-plugin-seo": "^0.2.0"           // SEO optimization
  }
}
```

### Build Configuration
- **Base URL**: `/docs/` (configurable via `BASE` environment variable)
- **Source Directory**: `src/`
- **Output Directory**: `src/.vuepress/dist/`
- **OpenSSL Legacy Provider**: Required for Node 16.20.2 builds

---

## Directory Structure

```
elementor-developers-docs/
│
├── .github/
│   └── workflows/
│       └── auto-dispatch.yaml          # CI/CD pipeline (triggers on master push)
│
├── src/                                # Documentation source files (292 .md files)
│   ├── .vuepress/                      # VuePress configuration
│   │   ├── config.js                   # Main VuePress configuration
│   │   ├── enhanceApp.js               # App-level Vue enhancements
│   │   ├── public/                     # Static assets (favicons, manifest, images)
│   │   │   ├── favicon.ico
│   │   │   ├── favicon.png
│   │   │   ├── manifest.json           # PWA manifest
│   │   │   └── assets/
│   │   │       └── img/                # Documentation images
│   │   ├── sidebars/                   # Navigation sidebar configs (23 files)
│   │   │   ├── widgets.js
│   │   │   ├── editor-controls.js
│   │   │   ├── getting-started.js
│   │   │   └── ... (one per section)
│   │   ├── styles/
│   │   │   ├── index.styl              # Custom Stylus styles
│   │   │   └── palette.styl            # Brand color palette
│   │   └── layout/
│   │       └── Layout.vue              # Custom layout component
│   │
│   ├── index.md                        # Homepage
│   │
│   ├── addons/                         # Building Addons (plugin structure, architecture)
│   ├── cli/                            # CLI documentation
│   ├── context-menu/                   # Context menu extension
│   ├── controls/                       # Creating custom controls
│   ├── data-structure/                 # Elementor data structure internals
│   ├── deprecations/                   # Deprecated features & migration guides
│   ├── dynamic-tags/                   # Dynamic tags system
│   ├── editor/                         # Editor internals
│   ├── editor-controls/                # Control types (text, select, color, etc.)
│   ├── finder/                         # Finder component
│   ├── form-actions/                   # Form action handlers
│   ├── form-fields/                    # Form field types
│   ├── getting-started/                # Onboarding documentation
│   ├── hello-elementor-theme/          # Hello Elementor theme documentation
│   ├── hooks/                          # PHP & JavaScript hooks
│   ├── hosting/                        # Hosting & deployment guides
│   ├── js/                             # JavaScript utilities & APIs
│   ├── managers/                       # Manager classes
│   ├── scripts-styles/                 # Scripts & styles loading
│   ├── theme-conditions/               # Theme conditions system
│   ├── themes/                         # Theme locations
│   └── widgets/                        # Widget creation (most comprehensive)
│
├── package.json                        # Project metadata, scripts, dependencies
├── package-lock.json                   # Dependency lock file
├── .nvmrc                              # Node version requirement (v16.20.2)
├── .gitignore                          # Git ignore rules
├── .npmignore                          # NPM publish exclusions
└── README.md                           # Repository overview
```

---

## Development Workflow

### Setup & Installation

```bash
# Clone repository
git clone https://github.com/elementor/elementor-developers-docs.git
cd elementor-developers-docs

# Ensure correct Node version (use nvm if available)
nvm use  # Uses v16.20.2 from .nvmrc

# Install dependencies
npm install
# OR
yarn install
```

### Development Commands

```bash
# Start local development server with hot reload
npm run dev
# Access at http://localhost:8080/docs/

# Build static site for production
npm run build
# Output: src/.vuepress/dist/

# Build with legacy OpenSSL provider (for CI/CD)
export NODE_OPTIONS=--openssl-legacy-provider
npm run build
```

### Development Server
- **URL**: http://localhost:8080/docs/
- **Hot Reload**: Automatic page refresh on file changes
- **Port**: 8080 (default, configurable)

---

## Documentation Conventions

### File Naming
- **Format**: `kebab-case.md` (all lowercase, hyphen-separated)
- **Entry Point**: Each section starts with `index.md`
- **Examples**:
  - ✅ `simple-example.md`
  - ✅ `widget-structure.md`
  - ❌ `SimpleExample.md`
  - ❌ `Widget_Structure.md`

### Document Structure

Every documentation page follows this pattern:

```markdown
# Page Title

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic|Intermediate|Advanced" />

Brief introduction paragraph explaining the topic...

## Section Heading

Content here...

### Subsection

More detailed content...

## Code Examples

```php
// PHP code example with proper syntax highlighting
```

## Related Topics

- [Link to related doc](./related-page.md)
```

### Badge System

Badges provide metadata about content difficulty and target version:

```markdown
<!-- Version Badge -->
<Badge type="tip" vertical="top" text="Elementor Core" />
<Badge type="tip" vertical="top" text="Elementor Pro" />

<!-- Difficulty Badge -->
<Badge type="warning" vertical="top" text="Basic" />
<Badge type="warning" vertical="top" text="Intermediate" />
<Badge type="warning" vertical="top" text="Advanced" />
```

**Usage Rules**:
- Always include both version and difficulty badges
- Place badges immediately after the H1 title
- Separate badges with a space

### Markdown Features

VuePress supports standard markdown plus:

```markdown
# Headers (H1-H6)
## Use H2 for main sections
### Use H3 for subsections

**Bold text**
*Italic text*

[Relative links](./other-page.md)
[Absolute links](/widgets/simple-example.md)

<!-- Images with VuePress base path helper -->
<img :src="$withBase('/assets/img/example.png')" alt="Description">

<!-- Tables -->
| Column 1 | Column 2 |
|----------|----------|
| Data 1   | Data 2   |

<!-- Code blocks with syntax highlighting -->
```php
// PHP code
```

```javascript
// JavaScript code
```

<!-- Inline code -->
Use `code` for inline references

<!-- Lists -->
- Unordered list item
- Another item

1. Ordered list item
2. Another item

<!-- Blockquotes -->
> Important note or quote
```

---

## Sidebar Navigation System

### How Sidebars Work

Each documentation section has its own sidebar configuration file in `src/.vuepress/sidebars/[section-name].js`.

### Sidebar File Structure

**Example: `src/.vuepress/sidebars/widgets.js`**

```javascript
module.exports = [
  {
    title: 'Section Title',           // Sidebar group title
    collapsable: false,                // Whether section can collapse
    sidebarDepth: -1,                  // Depth of heading extraction (-1 = all)
    children: [
      ['', 'Introduction'],            // First item links to index.md
      'file-name-without-extension',   // Refers to file-name-without-extension.md
      {
        title: 'Subsection',
        collapsable: false,
        sidebarDepth: -1,
        children: [
          'subsection-file-1',
          'subsection-file-2'
        ]
      }
    ]
  },
  {
    title: 'Another Section',
    collapsable: false,
    sidebarDepth: -1,
    children: [
      'another-file'
    ]
  }
];
```

### Key Sidebar Concepts

1. **Empty String Reference**: `['', 'Introduction']` always refers to `index.md`
2. **File Extensions**: Omit `.md` extension in sidebar config
3. **Paths**: Relative to the section directory
4. **Nesting**: Use nested objects for grouped navigation
5. **Order**: Items appear in sidebar in array order

### Registering Sidebars

Sidebars must be imported and registered in `src/.vuepress/config.js`:

```javascript
// 1. Import sidebar
const widgetsSidebar = require('./sidebars/widgets');

// 2. Register in themeConfig.sidebar
module.exports = {
  themeConfig: {
    sidebar: {
      '/widgets/': widgetsSidebar,
      // ... other sidebars
    }
  }
};
```

---

## Content Creation Guidelines

### Creating a New Documentation Page

**Step 1: Create the Markdown File**

```bash
# Navigate to appropriate section
cd src/widgets/

# Create new file (use kebab-case)
touch new-feature-guide.md
```

**Step 2: Add Document Header**

```markdown
# New Feature Guide

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Brief introduction explaining what this guide covers...
```

**Step 3: Add to Sidebar Navigation**

Edit `src/.vuepress/sidebars/widgets.js`:

```javascript
module.exports = [
  {
    title: 'Section Name',
    children: [
      // ... existing items
      'new-feature-guide',  // Add your new file here
    ]
  }
];
```

**Step 4: Test Locally**

```bash
npm run dev
# Navigate to the page and verify rendering
```

### Creating a New Documentation Section

**Step 1: Create Directory**

```bash
mkdir src/new-section
```

**Step 2: Create Index File**

```bash
cat > src/new-section/index.md << 'EOF'
# New Section

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Introduction to this section...
EOF
```

**Step 3: Create Sidebar Config**

```bash
cat > src/.vuepress/sidebars/new-section.js << 'EOF'
module.exports = [
  {
    title: 'New Section',
    collapsable: false,
    sidebarDepth: -1,
    children: [
      ['', 'Introduction']
    ]
  }
];
EOF
```

**Step 4: Register in VuePress Config**

Edit `src/.vuepress/config.js`:

```javascript
// Add import at top
const newSectionSidebar = require('./sidebars/new-section');

// Add to themeConfig.sidebar
module.exports = {
  themeConfig: {
    sidebar: {
      // ... existing sidebars
      '/new-section/': newSectionSidebar,
    }
  }
};
```

**Step 5: Add to Navigation Menu**

Edit `src/.vuepress/config.js` navigation:

```javascript
themeConfig: {
  nav: [
    {
      text: 'Components',
      items: [
        // ... existing items
        {
          text: 'New Section',
          link: '/new-section/',
        },
      ],
    },
  ],
}
```

---

## Code Examples Standards

### PHP Code Examples

```php
<?php
/**
 * Function description with proper PHPDoc.
 *
 * @since 1.0.0
 * @param Type $param Parameter description.
 * @return Type Return value description.
 */
function example_function( $param ) {
    // Always check for direct access
    if ( ! defined( 'ABSPATH' ) ) {
        exit; // Exit if accessed directly.
    }

    // Use proper WordPress coding standards
    return $param;
}
```

**PHP Standards**:
- Always include ABSPATH check
- Follow WordPress coding standards
- Use proper PHPDoc blocks
- Include `@since` version tags
- Escape output: `esc_html__()`, `esc_attr()`, etc.
- Use text domains for i18n

### JavaScript Code Examples

```javascript
/**
 * Function description.
 *
 * @since 1.0.0
 * @param {Type} param - Parameter description.
 * @return {Type} Return value description.
 */
function exampleFunction( param ) {
    // Use jQuery if needed (available in Elementor)
    jQuery( document ).ready( function( $ ) {
        // Code here
    } );
}
```

**JavaScript Standards**:
- Use JSDoc comments
- Follow Elementor's JavaScript patterns
- Use jQuery via `jQuery` or `$` in closures

### File Structure Examples

Use code blocks with comments to show directory structures:

```markdown
```
plugin-name/
|
├── assets/
|  ├── css/
|  └── js/
|
├── widgets/
|  └── widget-name.php
|
└── plugin-name.php
```
```

---

## Assets & Media

### Image Handling

**Location**: All images go in `src/.vuepress/public/assets/img/`

**Usage in Markdown**:

```markdown
<!-- Use VuePress $withBase helper for proper path resolution -->
<img :src="$withBase('/assets/img/example-screenshot.png')" alt="Descriptive alt text">
```

**Image Guidelines**:
- Use descriptive filenames: `elementor-widget-panel.png`
- Optimize images before committing (use compression)
- Always include descriptive `alt` text for accessibility
- Prefer PNG for screenshots, SVG for diagrams/logos
- Keep images under 500KB when possible

### Adding New Images

```bash
# Copy image to correct directory
cp ~/Downloads/new-screenshot.png src/.vuepress/public/assets/img/

# Reference in markdown
<img :src="$withBase('/assets/img/new-screenshot.png')" alt="Widget panel showing controls">
```

---

## Build & Deployment

### CI/CD Pipeline

**Workflow File**: `.github/workflows/auto-dispatch.yaml`

**Trigger**: Automatic on push to `master` branch

**Pipeline Steps**:

1. **Checkout**: Clone repository
2. **Build**:
   - Set Node OpenSSL legacy provider
   - Install dependencies with yarn
   - Build static site
3. **Dispatch**:
   - Send repository dispatch event to deployment repo
   - Include commit SHA, actor, and ref information

### Manual Deployment

```bash
# Build production assets
npm run build

# Output location
ls -la src/.vuepress/dist/

# The dist/ directory contains the complete static site
```

### Environment Variables

```bash
# Use custom base path (default: /docs/)
BASE=1 npm run build

# Use OpenSSL legacy provider (required for Node 16.20.2)
export NODE_OPTIONS=--openssl-legacy-provider
npm run build
```

---

## Common Tasks & Recipes

### Task 1: Update an Existing Documentation Page

```bash
# 1. Find and edit the file
vim src/widgets/simple-example.md

# 2. Test locally
npm run dev

# 3. Commit changes
git add src/widgets/simple-example.md
git commit -m "Update simple widget example with new API"
git push origin master
```

### Task 2: Add a New Widget Documentation Page

```bash
# 1. Create markdown file
touch src/widgets/my-new-widget.md

# 2. Add content with proper structure
cat > src/widgets/my-new-widget.md << 'EOF'
# My New Widget

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Description of the new widget...

## Overview

Content here...
EOF

# 3. Add to sidebar
# Edit src/.vuepress/sidebars/widgets.js and add 'my-new-widget'

# 4. Test
npm run dev

# 5. Commit
git add src/widgets/my-new-widget.md src/.vuepress/sidebars/widgets.js
git commit -m "Add documentation for My New Widget"
git push origin master
```

### Task 3: Fix Broken Links

```bash
# 1. Identify broken links (VuePress will warn in console)
npm run dev

# 2. Search for the broken link
grep -r "broken-link" src/

# 3. Update references
# Use relative paths: ./other-page.md
# Or absolute from root: /section/page.md

# 4. Verify fix
npm run dev
```

### Task 4: Update Sidebar Navigation Order

```bash
# 1. Edit appropriate sidebar file
vim src/.vuepress/sidebars/widgets.js

# 2. Reorder items in children array
# Items appear in the order listed

# 3. Test navigation
npm run dev

# 4. Commit changes
git add src/.vuepress/sidebars/widgets.js
git commit -m "Reorganize widgets sidebar navigation"
git push origin master
```

### Task 5: Add New Code Example

```markdown
## Example Usage

Here's how to implement this feature:

```php
<?php
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Register custom widget.
 *
 * @since 1.0.0
 * @param \Elementor\Widgets_Manager $widgets_manager Elementor widgets manager.
 * @return void
 */
function register_my_widget( $widgets_manager ) {
    require_once( __DIR__ . '/widgets/my-widget.php' );
    $widgets_manager->register( new \My_Widget() );
}
add_action( 'elementor/widgets/register', 'register_my_widget' );
```

This code should be placed in your plugin's main file.
```

---

## Important Considerations

### 1. Version Compatibility

**Always Specify Versions**:
```markdown
<!-- In code example headers -->
* Elementor tested up to: 3.25.0
* Elementor Pro tested up to: 3.25.0
```

### 2. Security Best Practices

**Always Include Security Checks**:

```php
// ABSPATH check in all PHP files
if ( ! defined( 'ABSPATH' ) ) {
    exit; // Exit if accessed directly.
}

// Escape output
echo esc_html( $variable );
echo esc_attr( $attribute );
echo esc_url( $url );

// Sanitize input
$clean = sanitize_text_field( $_POST['input'] );

// Verify nonces
wp_verify_nonce( $_POST['_wpnonce'], 'action_name' );
```

### 3. WordPress Coding Standards

Follow WordPress coding standards in all examples:
- **Naming**: `snake_case` for functions, `Capitalized_Snake_Case` for classes
- **Spacing**: Spaces around operators, after commas
- **Braces**: Opening brace on same line, closing on new line
- **Indentation**: Tabs for indentation, spaces for alignment
- **Documentation**: PHPDoc blocks for all functions and classes

### 4. Text Domain & Internationalization

```php
// Always use text domain for translatable strings
esc_html__( 'Text', 'plugin-text-domain' )
esc_attr__( 'Text', 'plugin-text-domain' )

// Use placeholder in plugin headers
* Text Domain: plugin-text-domain
```

### 5. Accessibility

- **Alt Text**: Always provide descriptive alt text for images
- **Semantic HTML**: Use proper heading hierarchy (H1 → H2 → H3)
- **Link Text**: Use descriptive link text, avoid "click here"

### 6. Content Quality

- **Clarity**: Write clear, concise explanations
- **Examples**: Provide practical, working code examples
- **Context**: Explain why, not just how
- **Consistency**: Maintain consistent terminology throughout

### 7. Testing Before Commit

```bash
# Always test locally before committing
npm run dev

# Check for:
# - Proper rendering
# - Working links
# - Code syntax highlighting
# - Image display
# - Sidebar navigation

# Verify build succeeds
npm run build
```

### 8. Git Commit Messages

Use clear, descriptive commit messages:

```bash
# Good examples
git commit -m "Add documentation for custom control types"
git commit -m "Fix broken links in widgets section"
git commit -m "Update widget example with new API"

# Bad examples
git commit -m "Update"
git commit -m "Fix stuff"
git commit -m "Changes"
```

### 9. Breaking Changes

When documenting breaking changes or deprecations:

```markdown
# Feature Name

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

::: warning BREAKING CHANGE
As of Elementor 3.x, this method has been deprecated. Use `new_method()` instead.
:::

## Migration Guide

To migrate from the old API:

[Migration steps here]
```

### 10. Link to Official Resources

Always link to official resources when referencing WordPress or Elementor features:

```markdown
Learn more about [WordPress hooks](https://developer.wordpress.org/plugins/hooks/).

See the [Elementor GitHub repository](https://github.com/elementor/elementor).
```

---

## Quick Reference

### Common File Paths

```
Configuration: src/.vuepress/config.js
Sidebars: src/.vuepress/sidebars/[section].js
Images: src/.vuepress/public/assets/img/
Styles: src/.vuepress/styles/
Documentation: src/[section]/[page].md
```

### Common Commands

```bash
npm run dev          # Development server
npm run build        # Production build
npm install          # Install dependencies
```

### Documentation Sections (Alphabetical)

- addons
- cli
- context-menu
- controls
- data-structure
- deprecations
- dynamic-tags
- editor
- editor-controls
- finder
- form-actions
- form-fields
- getting-started
- hello-elementor-theme
- hooks
- hosting
- js
- managers
- scripts-styles
- theme-conditions
- themes
- widgets

### Badge Types

```markdown
<Badge type="tip" vertical="top" text="Elementor Core" />
<Badge type="tip" vertical="top" text="Elementor Pro" />
<Badge type="warning" vertical="top" text="Basic" />
<Badge type="warning" vertical="top" text="Intermediate" />
<Badge type="warning" vertical="top" text="Advanced" />
```

---

## Additional Resources

### External Links

- **Live Documentation**: https://developers.elementor.com/docs/
- **Elementor GitHub**: https://github.com/elementor/elementor
- **VuePress Documentation**: https://v1.vuepress.vuejs.org/
- **WordPress Developer Resources**: https://developer.wordpress.org/
- **Elementor Developer Blog**: https://developers.elementor.com/blog/

### Getting Help

- Check existing documentation thoroughly
- Review similar documentation pages for patterns
- Test changes locally before committing
- Follow established conventions and patterns
- When in doubt, ask for clarification

---

**Last Updated**: 2025-11-20
**VuePress Version**: 1.9.7
**Node Version**: 16.20.2
**Repository**: elementor/elementor-developers-docs
