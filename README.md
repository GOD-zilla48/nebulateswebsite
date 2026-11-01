# NEBULA RACING website

Static site, no build step.

```
index.html                    the whole site (content lists are at the top of the script)
models/nebula-formula.glb     the 3D car
functions/api/enquiry.js      sponsorship form -> email (Cloudflare Pages Function)
_headers                      caching and security headers
```

## Run locally
The page must be served over http, not opened as a file:
`python3 -m http.server 8000` then open http://localhost:8000

## Deploy: GitHub + Cloudflare Pages
1. Create a GitHub repo and push these files to the root of the `main` branch.
2. Cloudflare dashboard > Workers & Pages > Create > Pages > Connect to Git, pick the repo.
3. Build command: leave empty. Build output directory: `/` (root). Save and deploy.
4. Custom domain: Pages project > Custom domains > Set up a custom domain.
   If you already have a Cloudflare Pages project and domain for the old coming-soon site, push these files to that repo instead and the domain stays as it is.

## Make the sponsorship form work
1. Create a free Resend account, verify your domain, create an API key.
2. In the Pages project > Settings > Variables and Secrets, add:
   `RESEND_API_KEY` (secret), `TO_EMAIL` (team inbox), `FROM_EMAIL` (e.g. `Nebula Racing <enquiries@yourdomain>`).
3. Redeploy. Until this is set the form shows an error instead of claiming success.
Alternative: set `email` in `CONFIG` in index.html to use a mailto fallback.

## Sponsorship proposal
Put your PDF at `proposal/nebula-racing-sponsorship.pdf` and set `proposalUrl` in `CONFIG` to that path.

## Edit content
Top of the script in index.html: `DIV` (engineering divisions, with an `img` field for images), `STAGES` (dates and status),
`JOURNAL` (add entries), `TEAM` (names). Add images under an `images/` folder and reference them as `images/name.jpg`.

## Credits and licence (check before taking sponsorship)
The car is a procedural three.js model adapted from github.com/bddicken/formula1 (declared ISC, no LICENSE file or named owner).
Confirm with the author before commercial use. Libraries: three.js (MIT), GSAP (GreenSock standard licence).
