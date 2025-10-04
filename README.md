# hugo-sample

A sample static site for open source projects using Hugo and the hugo-classless theme.

## Features

- **Hugo Static Site Generator**: Fast and flexible static site generation
- **hugo-classless Theme**: Clean, minimal design using classless CSS frameworks
- **Three Content Sections**:
  - **Pages**: HTML content pages
  - **Posts**: Markdown blog posts
  - **News**: Markdown news updates
- **Automated Deployment**: CI/CD with GitHub Actions
- **GitHub Pages Hosting**: Free, reliable hosting

## Site Structure

```
content/
├── pages/      # HTML pages
├── posts/      # Blog posts (Markdown)
└── news/       # News items (Markdown)
```

## Local Development

### Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) version 0.135.0 or later

### Running Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/rlnorthcutt/hugo-sample.git
   cd hugo-sample
   ```

2. Start the development server:
   ```bash
   hugo server -D
   ```

3. Open your browser to `http://localhost:1313`

### Building the Site

To build the site for production:

```bash
hugo --gc --minify
```

The built site will be in the `public/` directory.

## Deployment

The site automatically deploys to GitHub Pages when changes are pushed to the `main` branch.

### GitHub Pages Setup

1. Go to your repository settings
2. Navigate to "Pages" in the sidebar
3. Under "Build and deployment", select "GitHub Actions" as the source
4. The workflow will automatically deploy the site

The site will be available at: `https://rlnorthcutt.github.io/hugo-sample/`

## Content Management

### Adding a New Page

```bash
hugo new content/pages/your-page-name.md
```

### Adding a New Post

```bash
hugo new content/posts/your-post-title.md
```

### Adding a News Item

```bash
hugo new content/news/your-news-item.md
```

## Theme

This site uses the [hugo-classless](https://github.com/mozanunal/hugo-classless) theme, which provides a clean, minimal design using classless CSS frameworks.

## License

This sample site is provided as-is for educational and demonstration purposes.

