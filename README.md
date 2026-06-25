# UniCompare
**A university rankings explorer and comparison tool**
 
UniCompare lets prospective students search, filter, and compare universities from the QS World University Rankings 2024. Built with vanilla JavaScript and Firebase Realtime Database, the app loads and queries live ranking data across 1,400+ institutions.
 
![UniCompare Homepage](img1.png)
 
---
 
## Features
 
- **Search** — Find any university by partial name from the global header; results load on a dedicated search page
- **Explore with Filters** — Browse all universities with 10+ filterable dimensions including country, size, research intensity, focus type, and min/max score ranges for academic reputation, citations per faculty, employer reputation, sustainability, and more
- **Side-by-side Comparison** — Add up to 3 universities by name and compare their full ranking profiles simultaneously
- **Progressive Disclosure** — University cards show key info upfront with a "Show more details" toggle for the full breakdown
- **Live Data** — Rankings data is fetched at runtime from Firebase Realtime Database; no static JSON files
---
 
## Tech Stack
 
- **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+)
- **Backend/Data:** Firebase Realtime Database (two sharded databases merged client-side)
- **Data Source:** [QS World University Rankings 2024](https://www.topuniversities.com/world-university-rankings)
---
 
## Pages
 
| Page | Description |
|------|-------------|
| `index.html` | Landing page |
| `universities.html` | Full rankings list with filters sidebar |
| `compare.html` | Side-by-side university comparison tool |
| `search-results.html` | Search results page (accessed via header search) |
| `about-us.html` | About the project |
| `contact-us.html` | Contact form |
 
---
 
## How It Works
 
Data is stored across two Firebase Realtime Database instances and fetched concurrently using `Promise.all`. The app handles three rank formats from the QS dataset: numeric (`42`), range (`660-700`), and capped (`1400+`), with a custom sort function that normalizes all three for correct ordering.
 
```javascript
// Fetches from both databases in parallel and merges
const [response1, response2] = await Promise.all([fetch(db1URL), fetch(db2URL)]);
const universities = [...Object.values(data1), ...Object.values(data2)];
universities.sort(customSort);
```
 
---
 
## Setup
 
No build tools required. Open `index.html` directly in a browser or serve with any static file server:
 
```bash
python3 -m http.server 8000
# Open http://localhost:8000
```
 
> The app fetches live data from public Firebase endpoints. No API keys or local setup needed.
 
---
 
## Project Structure
 
```
unicompare/
├── index.html
├── universities.html
├── compare.html
├── search-results.html
├── about-us.html
├── contact-us.html
├── script.js          # All data fetching, filtering, search, and comparison logic
├── style.css          
├── img1.png           # Image on the main page of site
└── README.md
```
 
