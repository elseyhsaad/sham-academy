# Sham Academy Worldclass Landing Page

A fully independent Vue 3 + Vite + Tailwind 4 landing page. No API/backend dependency.

## Run

```bash
npm install
npm run dev -- --port 5174
```

Then open http://localhost:5174.

## Configure buttons

Copy `.env.example` to `.env.local` and fill:

- `VITE_PLATFORM_LOGIN_URL=https://your-platform.example/login`
- `VITE_PUBLIC_WHATSAPP=...` (international digits only)
- `VITE_PUBLIC_EMAIL=...`

Restart Vite after changing `.env.local`.

## Images

The group-lesson image is a local WebP in `public/images/group.webp`, so that card cannot break due to external availability. Other editorial images use Unsplash with bundled local WebP fallback on error. The fallback images are AI-generated concept visuals, not actual academy photography. Replace images with licensed original photos before public campaigns if needed. The site does not claim unverified testimonials, teacher credentials, enrollment figures or success rates.

## Deploy

`npm run build`, then deploy `dist` to the standalone static hosting.
