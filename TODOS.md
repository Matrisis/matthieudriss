# TODOS

## Design — Done (offer-rewrite)

### og-image.png regenerated
- **Status:** ✓ Complete
- New og-image.png (1200x630) with text: "Audit IA & Agentic Dev" / "Consultation personnalisée · 300€ HT"
- Monochrome design (#000/#fff), SF Compact geometric sans-serif, teal pill accent per DESIGN.md
- Generated 2026-05-06 via Python Pillow

### Prior "Build it now" items — Done
- ✓ Form loading/error states (D4): spinner animation + 10s timeout with email fallback
- ✓ Hero meta mobile CSS (D9): full-width pill on <768px
- ✓ Success banner redesign (D11): "Merci ! Je vous contacte sous 24h."

---

## Diagnostic IA rebrand — Post-ship

### Track Diagnostic IA → MVP Build deduction
- **Status:** [ ] Open
- **What:** When a lead pays 500€ for the Diagnostic IA and later books an MVP Build, apply the promised 500€ deduction.
- **Why:** "500€ déduits" appears in 3 places on the live page (card list item, card tagline, footer). No tracking system currently backs this promise.
- **Context:** At current volume, manual tracking is fine (remember who paid). Add a CRM tag, email label, or form field when the funnel converts consistently. Could be as simple as a dedicated email label in your inbox or a Notion table.
- **Depends on:** Nothing — implement whenever first Diagnostic → MVP Build conversion happens.

### Regenerate og-image.png
- **Status:** [ ] Open — do after copy ships
- **What:** og-image.png currently shows "Consultation personnalisée · 300€ HT". After the Diagnostic IA rebrand, regenerate with new label/price.
- **Why:** Social preview cards (LinkedIn, Twitter/X, Slack) use the baked-in image text. Until regenerated, shares will show old label + old price in the visual card.
- **Context:** Use the same Python Pillow script from 2026-05-06. New text: "Audit IA & Agentic Dev" / "Diagnostic IA · 500€ HT". Low urgency — social caches expire slowly, but regenerate before any active social promotion.
- **Depends on:** Copy changes shipped to main.

---

## Post-deploy checks (not blocking)

- [ ] Google Rich Results Test on deployed URL (all 4 JSON-LD schemas)
- [ ] Twitter Card Validator
- [ ] LinkedIn Post Inspector
