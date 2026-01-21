# 🚀 Deployment Guide - Elite Hotel

## Deploy to Vercel (Frontend)

### Option 1: Using Vercel CLI
```bash
# Install Vercel CLI globally
npm install -g vercel

# Deploy
cd Elite-hotel-main
vercel
```

### Option 2: Using GitHub Integration (Recommended)

1. **Push to GitHub:**
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/Elite-hotel.git
   git branch -M main
   git push -u origin main
   ```

2. **Connect to Vercel:**
   - Go to [vercel.com](https://vercel.com)
   - Sign up/Login with GitHub
   - Click "New Project"
   - Import the repository
   - **Framework Preset**: Vite
   - **Root Directory**: `frontend`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - Click "Deploy"

## GitHub Pages Setup

Since this is a monorepo with a Vite frontend, you can use GitHub Actions to auto-deploy to GitHub Pages:

1. Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: cd frontend && npm install
      
      - name: Build
        run: cd frontend && npm run build
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./frontend/dist
```

2. Enable GitHub Pages in repository settings:
   - Go to Settings → Pages
   - Set source to "gh-pages" branch
   - Your site will be live at: `https://YOUR_USERNAME.github.io/Elite-hotel`

## Environment Variables

### For Vercel:
1. Go to Project Settings → Environment Variables
2. Add required variables (if using backend APIs):
   - `VITE_API_BASE_URL`
   - `VITE_SOCKET_URL`
   - etc.

## Preview Links

After deployment:
- **Vercel**: `https://elite-hotel.vercel.app`
- **GitHub Pages**: `https://YOUR_USERNAME.github.io/Elite-hotel`

## Production Build

```bash
cd frontend
npm run build
npm run preview
```

Visit `http://localhost:4173` to preview production build locally.
