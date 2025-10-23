# Fort Wayne Affordable Housing Eligibility Calculator

## Project Overview

A simple, single-page web calculator that helps Fort Wayne, IN residents determine if they qualify for affordable housing programs. Solves the confusion around "Area Median Income (AMI)" percentages by translating them into clear dollar amounts and program eligibility.

## The Problem We're Solving

When people see affordable housing listed as "60% AMI" or "50% AMI", they have no idea:
- What that means in dollars
- If they qualify
- What programs are available to them
- How much rent they can afford

This calculator takes their income and household size and gives them clear, actionable answers.

## MVP Scope

**What we're building:**
- Single HTML page with embedded JavaScript
- Simple form with 2 inputs: annual income and household size
- Instant calculation showing:
  - AMI qualification level (30%, 50%, 60%, 80%)
  - Affordable rent range
  - Programs they qualify for
  - Next steps with contact info

**What we're NOT building (for now):**
- Property database
- User accounts
- Backend/database
- Search functionality

## Technical Stack

- **Frontend:** Pure HTML, CSS (Tailwind CDN), JavaScript
- **Deployment:** Netlify or GitHub Pages
- **Dependencies:** None (except Tailwind CDN)
- **Maintenance:** Update AMI data once per year

## Key Data: Allen County AMI Limits (2025)

Source: HUD Income Limits (needs to be verified/updated from https://www.huduser.gov/portal/datasets/il.html)

```javascript
const amiData = {
    1: { 30: 19950, 50: 33250, 60: 39900, 80: 53200 },
    2: { 30: 22800, 50: 38000, 60: 45600, 80: 60800 },
    3: { 30: 25650, 50: 42750, 60: 51300, 80: 68400 },
    4: { 30: 28500, 50: 47500, 60: 57000, 80: 76000 },
    5: { 30: 30800, 50: 51300, 60: 61560, 80: 82080 },
    6: { 30: 33100, 50: 55100, 60: 66120, 80: 88160 },
    7: { 30: 35350, 50: 58900, 60: 70680, 80: 94240 },
    8: { 30: 37650, 50: 62750, 60: 75300, 80: 100400 }
};
```

## Calculation Logic

1. **User inputs:** Annual household income + household size
2. **Compare income** against AMI limits for their household size
3. **Determine AMI level:**
   - ≤30% AMI = "Extremely Low Income"
   - ≤50% AMI = "Very Low Income"
   - ≤60% AMI = "Low Income"
   - ≤80% AMI = "Moderate Income"
   - >80% AMI = "Above income limits"
4. **Calculate affordable rent:** 30-40% of monthly income
5. **Show eligible programs** based on AMI level

## Program Eligibility by AMI Level

**30% AMI qualifies for:**
- Public Housing (rent based on 30% of income)
- Section 8 Housing Choice Vouchers
- Project-Based Section 8
- All LIHTC properties (30%, 50%, 60%, 80% units)

**50% AMI qualifies for:**
- Section 8 Housing Choice Vouchers
- Some Public Housing units
- LIHTC properties (50%, 60%, 80% units)

**60% AMI qualifies for:**
- LIHTC properties (60%, 80% units)
- Some Section 8 properties

**80% AMI qualifies for:**
- LIHTC properties (80% units)
- Workforce housing

## Fort Wayne Housing Resources

Include in "Next Steps" section:

- **Fort Wayne Housing Authority (FWHA)**
  - Phone: (260) 267-9300
  - Website: fwha.org
  - Programs: Public Housing, Section 8, LIHTC properties

- **Brightpoint** (surrounding counties)
  - Phone: (260) 423-3546 ext. 332
  - Website: mybrightpoint.org
  - Programs: Housing Choice Vouchers, Housing Solutions

- **IHCDA Fort Wayne Office**
  - Phone: (260) 422-2522
  - Programs: LIHTC property database

## File Structure

```
fort-wayne-housing-calculator/
├── index.html          (Main calculator page)
├── README.md           (This file)
└── .gitignore          (Optional)
```

## Design Requirements

- **Mobile-first:** Most users will be on phones
- **Clear, simple form:** No jargon
- **Large, readable text:** Accessible to all ages
- **Color-coded results:**
  - Green = Qualified
  - Yellow = Above limits
- **Print-friendly:** Users may want to bring results to appointments

## Deployment Steps

1. **Build:** Create single `index.html` file
2. **Test locally:** Open in browser, verify calculations
3. **Deploy to Netlify:**
   - Drag and drop `index.html`
   - Get free subdomain: `fort-wayne-housing.netlify.app`
4. **Optional:** Buy custom domain ($12/year)
   - Suggestion: `fortwaynehousing.org`

## Testing Checklist

Test with these sample inputs to verify calculations:

| Income  | Household | Expected Result |
|---------|-----------|-----------------|
| $25,000 | 2 people  | 50% AMI (Very Low Income) |
| $35,000 | 3 people  | 60% AMI (Low Income) |
| $45,000 | 4 people  | 60% AMI (Low Income) |
| $20,000 | 1 person  | 50% AMI (Very Low Income) |
| $85,000 | 4 people  | Above limits |

## Future Enhancements (Post-MVP)

- [ ] Add Wells County and Huntington County AMI data
- [ ] Spanish translation
- [ ] Email results to user
- [ ] Print-optimized results page
- [ ] Link to actual property listings (if we build phase 2)
- [ ] Save/share results via URL
- [ ] Add disability/veteran preferences info

## Success Metrics

Track with simple Google Analytics:
- Calculator submissions per week
- Which AMI levels are most common
- Bounce rate vs. engagement

**Goal:** 100+ uses in first month = proof of demand

## Notes for Development

- AMI data must be updated annually (HUD publishes in April)
- All calculations in the browser (no backend needed)
- Keep it simple - resist feature creep
- Focus on clarity over sophistication
- Make sure results are actionable (include phone numbers, next steps)

## Marketing Plan

Once deployed, share on:
- r/FortWayne subreddit
- Fort Wayne Facebook groups
- Email to FWHA, Brightpoint, United Way
- Local libraries bulletin boards
- Social service agencies (211, Community Harvest Food Bank, etc.)

**Marketing angle:** "Confused by '60% AMI'? Our free calculator tells you EXACTLY what affordable housing you qualify for in Fort Wayne in 30 seconds."

## Questions to Resolve

- [ ] Confirm exact 2025 AMI data for Allen County from HUD
- [ ] Should we include Wells/Huntington counties in v1?
- [ ] What domain name to use?
- [ ] Any other Fort Wayne-specific programs to mention?
- [ ] Should we add a feedback form?

## Development Timeline

- **Day 1-2:** Create HTML structure and form
- **Day 3:** Implement calculation logic
- **Day 4:** Style with Tailwind, make mobile-responsive
- **Day 5:** Test thoroughly, refine UX
- **Day 6:** Deploy to Netlify
- **Day 7:** Share and gather initial feedback

---

**Total time to MVP:** ~1 week (8-10 hours)  
**Maintenance:** ~1 hour per year (update AMI data)  
**Cost:** $0-12/year (free hosting + optional domain)

## License

This project is intended to be a free public resource for Fort Wayne residents seeking affordable housing.

## Contact

[Your contact information or link to provide feedback]