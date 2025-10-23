# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Fort Wayne Affordable Housing Eligibility Calculator - A single-page web application that helps Fort Wayne, IN residents determine if they qualify for affordable housing programs by translating Area Median Income (AMI) percentages isnto clear dollar amounts and program eligibility.

## Technology Stack

- **Pure HTML/CSS/JavaScript** - No build tools, frameworks, or dependencies
- **Tailwind CSS** - Loaded via CDN only
- **Deployment** - Designed for static hosting (Netlify or GitHub Pages)

This is intentionally a simple, single-file application with no build process.

## Project Structure

Currently planned as:
```
index.html    - Main calculator page (all HTML, CSS, JavaScript in one file)
```

The entire application should be contained in a single HTML file with embedded styles and scripts.

## Core Data Model

The calculator uses HUD Income Limits for Allen County (Fort Wayne, IN). AMI limits are structured by household size (1-8 people) and AMI percentage (30%, 50%, 60%, 80%):

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

**IMPORTANT:** This data must be updated annually when HUD publishes new income limits (typically in April). Source: https://www.huduser.gov/portal/datasets/il.html

## Calculation Logic

1. User provides: annual household income + household size (1-8 people)
2. Compare income against AMI thresholds for their household size
3. Determine AMI level and qualification:
   - ≤30% AMI = "Extremely Low Income" (qualifies for all programs)
   - ≤50% AMI = "Very Low Income" (qualifies for Section 8, most LIHTC)
   - ≤60% AMI = "Low Income" (qualifies for LIHTC 60%/80% units)
   - ≤80% AMI = "Moderate Income" (qualifies for LIHTC 80% units)
   - >80% AMI = "Above income limits" (does not qualify)
4. Calculate affordable rent range: 30-40% of monthly income
5. Display eligible programs with specific Fort Wayne contact information

## Fort Wayne Resources (Include in Results)

- **Fort Wayne Housing Authority (FWHA)**: (260) 267-9300, fwha.org
- **Brightpoint**: (260) 423-3546 ext. 332, mybrightpoint.org
- **IHCDA Fort Wayne Office**: (260) 422-2522

## Design Requirements

- **Mobile-first**: Primary users will be on smartphones
- **No jargon**: Avoid technical housing terms, use plain language
- **Large, readable text**: Accessibility for all ages
- **Color-coded results**: Green for qualified, yellow/red for above limits
- **Print-friendly**: Users may print results for appointments
- **Fast and simple**: No loading states, instant calculations

## Testing

Test with these cases to verify calculation logic:

| Annual Income | Household Size | Expected AMI Level |
|--------------|----------------|-------------------|
| $25,000 | 2 | 50% AMI (Very Low Income) |
| $35,000 | 3 | 60% AMI (Low Income) |
| $45,000 | 4 | 60% AMI (Low Income) |
| $20,000 | 1 | 50% AMI (Very Low Income) |
| $85,000 | 4 | Above limits |

## Local Development

Since this is a single HTML file with no dependencies:

1. Open `index.html` directly in a browser
2. Make changes and refresh to test
3. No build process, compilation, or server needed

## Deployment

Simply upload `index.html` to any static hosting service (Netlify, GitHub Pages, etc.). No build step required.

## Project Constraints

**What this project IS:**
- Simple, accessible calculator
- Single-page, no-backend solution
- Information tool only

**What this project is NOT:**
- Property database or listing service
- User account system
- Multi-county solution (Fort Wayne/Allen County only for MVP)
- Dynamic data that updates from APIs

## Annual Maintenance

This calculator requires annual updates when HUD publishes new AMI limits (typically April). Update the `amiData` object with new values for Allen County.