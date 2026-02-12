# AGENTS.md - Developer & AI Agent Guidelines

Guidelines for agentic coding and human developers working on the weather-web-app project.

## 🎯 Project Overview

- **Type**: Vanilla HTML/CSS/JavaScript weather application
- **Design**: Apple Liquid Glass aesthetic with glassmorphic UI components
- **Deployment**: GitHub Pages (static site, no build process)
- **Stack**: HTML5, CSS3, ES6+ JavaScript (zero dependencies)
- **Target**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+)

## 🔨 Build & Development Commands

### Local Development Server

```bash
# Using Node.js http-server
npx http-server

# Using Python 3
python3 -m http.server 8000

# Using PHP (if available)
php -S localhost:8000

# Using Live Server (VS Code extension)
# Open index.html and use Live Server
```

### No Build Process
This project uses **zero build tools** - vanilla HTML/CSS/JS only.
- No npm install needed
- No compilation step
- No bundler configuration
- Direct browser execution

### GitHub Pages Deployment

```bash
# Push to GitHub (auto-deploys to GitHub Pages)
git add .
git commit -m "your message"
git push origin main

# Site available at: https://thiennn.github.io/weather-web-app
```

### Code Quality Tools

Currently no linting/testing framework configured. When adding:

```bash
# To add ESLint (optional future enhancement)
npm init -y
npm install --save-dev eslint
npx eslint js/*.js

# To add tests (optional future enhancement)
npm install --save-dev jest
npm test
```

## 📝 Code Style Guidelines

### JavaScript (ES6+)

#### Imports & Module Pattern
```javascript
// ✅ GOOD: Module pattern with exports
const weather = (() => {
  const API_KEY = '73b569ae622a1de19b12eb599eb7547b';
  const API_BASE = 'https://api.openweathermap.org/data/2.5';

  const fetchWeather = async (lat, lon) => {
    // implementation
  };

  return { fetchWeather };
})();

// ✅ ACCEPTABLE: Class-based modules
class WeatherAPI {
  constructor(apiKey) {
    this.apiKey = apiKey;
  }
  
  async fetch(lat, lon) {
    // implementation
  }
}

// ❌ AVOID: Global variables
window.API_KEY = 'key'; // Don't expose to global scope
```

#### Naming Conventions
```javascript
// ✅ GOOD: Clear, descriptive names
const fetchCurrentWeather = async (latitude, longitude) => {};
const formatTemperature = (celsius) => `${Math.round(celsius)}°C`;
const calculateFeelsLike = (temp, humidity, wind) => {};

// ✅ Constants: UPPER_SNAKE_CASE
const API_KEY = '73b569ae622a1de19b12eb599eb7547b';
const MAX_RETRY_ATTEMPTS = 3;
const CACHE_DURATION_MS = 30 * 60 * 1000;

// ✅ Functions: camelCase
const updateWeatherDisplay = (data) => {};
const toggleDarkMode = () => {};

// ✅ Classes: PascalCase
class WeatherAPIClient {}
class UIRenderer {}

// ✅ Boolean variables: prefix with is/has/should
const isLoading = true;
const hasError = false;
const shouldRefresh = true;
```

#### Formatting & Indentation
```javascript
// ✅ GOOD: 2-space indentation, clear structure
const app = {
  state: {
    weather: null,
    theme: 'light'
  },
  
  async init() {
    this.setupEventListeners();
    await this.loadWeather();
  }
};

// ✅ Arrow functions for callbacks/promises
const numbers = [1, 2, 3].map(n => n * 2);
const promise = fetch(url).then(r => r.json());

// ✅ Template literals for strings
const message = `Temperature: ${temp}°C in ${location}`;

// ❌ AVOID: var keyword (use const/let)
// ❌ AVOID: Single space indentation or tabs
// ❌ AVOID: Excessive nesting (max 3 levels)
```

#### Type Safety & Documentation
```javascript
// ✅ JSDoc for complex functions
/**
 * Fetches weather data from OpenWeatherMap API
 * @param {number} latitude - Geographic latitude
 * @param {number} longitude - Geographic longitude
 * @returns {Promise<Object>} Weather data object
 * @throws {Error} If API request fails
 */
async function fetchWeather(latitude, longitude) {
  // implementation
}

// ✅ Type hints in comments where helpful
const parseResponse = (response) => {
  // response: {temp: number, condition: string, humidity: number}
  return {
    temp: Math.round(response.temp),
    condition: response.condition
  };
};

// ✅ Input validation
const setTheme = (theme) => {
  if (!['light', 'dark'].includes(theme)) {
    throw new Error(`Invalid theme: ${theme}`);
  }
  // implementation
};
```

#### Error Handling
```javascript
// ✅ GOOD: Descriptive error messages
try {
  const response = await fetch(url);
  if (!response.ok) {
    throw new Error(`API Error: ${response.status} ${response.statusText}`);
  }
  return await response.json();
} catch (error) {
  console.error('Failed to fetch weather:', error);
  // Fallback to cached data or default
  return getDefaultWeather();
}

// ✅ GOOD: Validate before processing
const updateUI = (data) => {
  if (!data || typeof data !== 'object') {
    console.warn('Invalid data format:', data);
    return false;
  }
  // Safe to use data
};

// ✅ GOOD: User-friendly error messages
const showError = (error) => {
  const message = error.message === 'Failed to fetch'
    ? 'Unable to connect. Check your internet connection.'
    : error.message;
  ui.showNotification(message, 'error');
};

// ❌ AVOID: Silent failures
// ❌ AVOID: Generic catch blocks without handling
// ❌ AVOID: console.log in production (use console.error/warn)
```

#### Async/Await Pattern
```javascript
// ✅ GOOD: Clear async/await usage
const loadWeatherData = async () => {
  try {
    const coords = await getGeolocation();
    const weather = await fetchWeather(coords.lat, coords.lon);
    const aqi = await fetchAQI(coords.lat, coords.lon);
    return { weather, aqi };
  } catch (error) {
    console.error('Failed to load weather:', error);
    return null;
  }
};

// ✅ GOOD: Parallel requests when independent
const [weather, forecast, aqi] = await Promise.all([
  fetchWeather(lat, lon),
  fetchForecast(lat, lon),
  fetchAQI(lat, lon)
]);

// ❌ AVOID: Unnecessary Promise wrapping
// ❌ AVOID: await in loops (use Promise.all instead)
```

### CSS Styling

#### File Organization
```css
/* ✅ GOOD: Organized structure in styles.css */

/* 1. CSS Variables */
:root {
  --color-primary: #0EA5E9;
  --blur-amount: 25px;
  --border-radius: 28px;
}

/* 2. Base Styles */
* { margin: 0; padding: 0; }
html { font-size: 16px; }
body { font-family: -apple-system, sans-serif; }

/* 3. Typography */
h1, h2, h3 { font-weight: 600; }

/* 4. Components */
.button { /* styles */ }
.card { /* styles */ }

/* 5. Layout */
.container { /* styles */ }
.grid { /* styles */ }

/* 6. Utilities */
.hidden { display: none; }
.loading { opacity: 0.5; }
```

#### Glassmorphic Design Standards
```css
/* ✅ Liquid Glass component */
.glass-card {
  backdrop-filter: blur(25px);
  -webkit-backdrop-filter: blur(25px); /* Safari */
  background: rgba(255, 255, 255, 0.92);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 28px;
  box-shadow: 0 8px 32px rgba(31, 39, 55, 0.1);
}

/* ✅ Dark mode variant */
body.dark-mode .glass-card {
  background: rgba(30, 30, 30, 0.92);
  border-color: rgba(255, 255, 255, 0.1);
}

/* ✅ Light reflection overlay */
.glass-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 50%;
  background: linear-gradient(180deg, rgba(255,255,255,0.2) 0%, transparent 100%);
  border-radius: 28px;
  pointer-events: none;
}
```

#### Naming Conventions
```css
/* ✅ GOOD: BEM-inspired, descriptive class names */
.weather-card { /* block */ }
.weather-card__temperature { /* element */ }
.weather-card--loading { /* modifier */ }

/* ✅ GOOD: Functional/utility naming */
.flex-center { display: flex; justify-content: center; }
.text-center { text-align: center; }
.mt-4 { margin-top: 1rem; }

/* ✅ GOOD: Semantic naming */
.primary-button { /* primary action */ }
.secondary-button { /* secondary action */ }
.error-message { /* error state */ }

/* ❌ AVOID: Style-based names */
.red-text { /* Don't use colors in class names */ }
.big-font { /* Don't hardcode styles */ }
.left-side { /* Don't position in class names */ }
```

### HTML Structure

#### Semantic Markup
```html
<!-- ✅ GOOD: Proper semantic HTML -->
<main class="app">
  <header class="app-header">
    <h1>Weather App</h1>
    <button aria-label="Toggle dark mode">🌙</button>
  </header>
  
  <section class="weather-display">
    <article class="weather-card">
      <!-- Weather content -->
    </article>
  </section>
  
  <footer class="app-footer">
    <p>Last updated: <time datetime="2024-02-12">Now</time></p>
  </footer>
</main>

<!-- ✅ GOOD: Accessibility attributes -->
<button 
  id="refresh-btn"
  aria-label="Refresh weather data"
  aria-busy="false"
>
  Refresh
</button>

<!-- ✅ GOOD: Data attributes for JS targeting -->
<div data-weather-card data-condition="rainy">
  <!-- Content -->
</div>

<!-- ❌ AVOID: Div soup without semantics -->
<!-- ❌ AVOID: Onclick handlers (use event listeners) -->
<!-- ❌ AVOID: Non-semantic elements for headings -->
```

## 📂 File & Directory Organization

```
weather-web-app/
├── index.html              # Single entry point
├── css/
│   ├── styles.css         # Main + components
│   ├── responsive.css     # Media queries
│   └── animations.css     # Keyframes
├── js/
│   ├── app.js             # Init & orchestration
│   ├── weather.js         # API layer
│   ├── ui.js              # DOM rendering
│   ├── theme.js           # Theme logic
│   └── icons.js           # Icon definitions
├── manifest.json          # PWA manifest
└── AGENTS.md
```

#### Guidelines
- Keep modules small and focused (single responsibility)
- One export per module (or IIFE pattern)
- Use descriptive file names matching functionality
- No utility folder - inline small helpers

## 🔒 Security Practices

```javascript
// ✅ API Key - embedded but not exposed in commits
const API_KEY = '73b569ae622a1de19b12eb599eb7547b';

// ✅ HTTPS required for production
// GitHub Pages provides HTTPS automatically

// ✅ Sanitize user input
const sanitizeLocation = (input) => {
  return input.trim().slice(0, 100); // Limit length
};

// ✅ No sensitive data in localStorage
// Only store: theme preference, recent searches
```

## ✅ Git Workflow

```bash
# 1. Create feature branch
git checkout -b feature/add-hourly-forecast

# 2. Commit frequently with clear messages
git add css/styles.css
git commit -m "feat: add hourly forecast styling"

# 3. Push and merge
git push origin feature/add-hourly-forecast
# Create Pull Request on GitHub

# 4. Auto-deploys to GitHub Pages on merge
```

#### Commit Message Convention
```
feat: add hourly forecast display
fix: correct dark mode color contrast
style: refactor CSS variable names
docs: update README.md
chore: update .gitignore
```

## 🧪 Testing (Optional Future Enhancement)

When tests are added:

```bash
# Run single test
npm test -- weather.test.js

# Run with coverage
npm test -- --coverage

# Watch mode
npm test -- --watch
```

Test structure (future):
```javascript
// tests/weather.test.js
describe('WeatherAPI', () => {
  test('should fetch current weather', async () => {
    // test implementation
  });
});
```

## ⚡ Performance Standards

- Page load: < 2 seconds
- API response: < 1 second (with caching)
- Animation frame rate: 60fps
- Cache weather data: 30 minutes
- Use CSS animations (not JavaScript)

## 📋 Before Committing Code

- [ ] Code follows style guidelines above
- [ ] No console errors/warnings
- [ ] Mobile responsive (test at 320px, 768px, 1024px)
- [ ] Dark mode works correctly
- [ ] Accessibility: Tab through page works
- [ ] Git message is clear and follows convention
- [ ] No API keys exposed in code

## 🚫 Common Anti-Patterns

```javascript
// ❌ Global variables
window.weather = {};

// ❌ Mixing concerns
const weather = {
  data: {},
  render: () => {}, // DOM logic shouldn't be here
};

// ❌ Hardcoded values
const url = 'https://api.openweathermap.org/data/2.5/weather?lat=21...';

// ❌ Callback hell
fetch(url).then(r => r.json()).then(d => {
  updateUI(d);
});

// ❌ Not handling errors
const data = JSON.parse(userInput); // What if invalid?

// ❌ Creating memory leaks
element.addEventListener('click', onClick); // Never removed
```

## ✨ Code Review Checklist

1. **Functionality**: Does it work as intended?
2. **Style**: Follows guidelines above?
3. **Performance**: No unnecessary renders/requests?
4. **Accessibility**: WCAG AA compliant?
5. **Security**: No sensitive data exposed?
6. **Testing**: Works on mobile/desktop/dark mode?
7. **Documentation**: Code is self-documenting?

---

**Last Updated**: February 2026  
**For Questions**: Refer to README.md or create GitHub issue
