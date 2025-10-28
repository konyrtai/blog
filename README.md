# Alibek Konyrtai's Blog

A personal blog built with Hugo and PaperMod theme, featuring programming posts, tutorials, and insights.

## Features

- **Posts**: Programming articles and tutorials
- **Categories**: Organized content by topics
- **Tags**: Find posts by specific technologies and concepts
- **About**: Personal information and contact details

## Local Development

### Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) (v0.100.0 or later)
- Git

### Setup

1. Clone the repository:
```bash
git clone https://github.com/alibekkonyrtai/blog.git
cd blog
```

2. Install Hugo theme:
```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

3. Start the development server:
```bash
hugo server -D
```

The site will be available at `http://localhost:1313`

### Creating New Posts

Create a new post in the `content/posts/` directory:

```bash
hugo new posts/my-new-post.md
```

### Building for Production

```bash
hugo --minify
```

The built site will be in the `public/` directory.

## Deployment

This blog is configured to deploy automatically to GitHub Pages using GitHub Actions. Simply push to the main branch and the site will be built and deployed automatically.

## License

This project is open source and available under the [MIT License](LICENSE).

## Contact

- **Email**: alibek@konyrtai.dev
- **LinkedIn**: [linkedin.com/in/alibekkonyrtai](https://linkedin.com/in/alibekkonyrtai)
- **GitHub**: [github.com/alibekkonyrtai](https://github.com/alibekkonyrtai)
