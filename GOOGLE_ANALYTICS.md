# Adding Google Analytics later

1. Create a GA4 property at https://analytics.google.com (Admin → Create Property) for mysipnotes.com. This gives you a Measurement ID like `G-XXXXXXXXXX`.
2. In `index.html`, right after the opening `<head>` tag (or right before `</head>`), add:

   ```html
   <script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'G-XXXXXXXXXX');
   </script>
   ```

   Replace both `G-XXXXXXXXXX` with your real Measurement ID.
3. Add the same snippet to `privacy-policy.html` and `data-deletion.html` if you want traffic tracked there too — GA is per-page, not site-wide by default.
4. Since this is a static site (no router), pageviews on the single `index.html` fire automatically on load. No extra pageview code needed unless you add more pages or turn sections into separate routes.
5. Mention the new tracking in `privacy-policy.html` — you're already collecting no personal data client-side today, so this is a real change worth disclosing (e.g. a line noting you use Google Analytics and link to Google's privacy policy).
6. Deploy, then confirm it's firing in GA4 under Reports → Realtime while you browse the live site.
