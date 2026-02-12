# Weather Web App 🌤️

A beautiful, modern weather application built with vanilla HTML, CSS, and JavaScript. Features Apple's Liquid Glass design aesthetic, comprehensive weather data, and seamless dark mode support.

## 🎨 Design

The app follows Apple's Liquid Glass design language with:
- **Glassmorphic UI**: Translucent, frosted glass effect with backdrop blur
- **Smooth Gradients**: Dynamic light/dark mode backgrounds
- **Rounded Corners**: 24-28px border radius for Apple-style appearance
- **Specular Highlights**: Subtle light reflection effects on glass elements
- **Responsive Layout**: Mobile-first design that scales to all devices

## ✨ Features

### Core Weather Display
- **Current Conditions**: Temperature, condition, feels-like temperature
- **Detailed Metrics**: Humidity, wind speed, visibility, pressure, dew point
- **Location Support**: Geolocation detection with Hanoi (Vietnam) fallback
- **Live Updates**: Auto-refresh with manual refresh button

### Extended Features
- **Hourly Forecast**: Next 24 hours with 3-hour intervals
- **5-Day Forecast**: Daily high/low temperatures and conditions
- **UV Index**: Color-coded (Green/Yellow/Orange/Red) sun exposure level
- **Air Quality Index (AQI)**: Pollution level with health recommendations
- **Sunrise/Sunset**: Display solar event times

### Interactive Features
- **City Search**: Find weather for any location worldwide
- **Recent Locations**: Quick access to previously searched cities
- **Dark Mode Toggle**: Smooth theme switching with persistent preference
- **Responsive Design**: Optimized for mobile, tablet, and desktop screens

## 🚀 Quick Start

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, Edge)
- No build process or dependencies required
- OpenWeatherMap API key (included in project)

### Installation

```bash
# Clone the repository
git clone https://github.com/thiennn/weather-web-app.git
cd weather-web-app

# No build step needed - serve locally
npx http-server

# Or use Python
python3 -m http.server 8000

# Open http://localhost:8000 in your browser
```

### GitHub Pages Deployment

The app is automatically deployed to GitHub Pages. Live version: 
[https://thiennn.github.io/weather-web-app](https://thiennn.github.io/weather-web-app)

## 📁 Project Structure

```
weather-web-app/
├── index.html                  # Main HTML template
├── css/
│   ├── styles.css             # Core styles & Liquid Glass components
│   ├── responsive.css         # Media queries & responsive design
│   └── animations.css         # Keyframes & smooth transitions
├── js/
│   ├── app.js                 # Main application controller
│   ├── weather.js             # OpenWeatherMap API integration
│   ├── ui.js                  # DOM manipulation & rendering
│   ├── theme.js               # Dark mode logic & persistence
│   └── icons.js               # SVG weather icon definitions
├── manifest.json              # PWA manifest file
├── .gitignore                 # Git ignore rules
├── README.md                  # This file
└── AGENTS.md                  # Guidelines for AI agents/developers
```

## 🛠️ Technology Stack

- **HTML5**: Semantic markup for accessibility
- **CSS3**: Custom properties, Grid, Flexbox, backdrop-filter
- **JavaScript (ES6+)**: Vanilla JS, no frameworks or dependencies
- **APIs**: 
  - OpenWeatherMap API (weather data)
  - Geolocation API (browser location detection)
  - localStorage (persistence)

## 🎨 Color Palette

### Light Mode
- **Background Gradient**: Sky blue to light purple
- **Glass Fill**: White with 92% opacity
- **Text Primary**: Dark gray (#1F2937)
- **Text Secondary**: Medium gray (#6B7280)
- **Accent**: Cyan blue (#0EA5E9)

### Dark Mode
- **Background Gradient**: Navy to dark purple
- **Glass Fill**: Dark gray with 92% opacity
- **Text Primary**: Off-white (#F9FAFB)
- **Text Secondary**: Light gray (#D1D5DB)
- **Accent**: Light cyan (#38BDF8)

## 🔧 Configuration

### OpenWeatherMap API
The app uses OpenWeatherMap's free tier. API key is configured in `js/weather.js`:
```javascript
const API_KEY = '73b569ae622a1de19b12eb599eb7547b';
```

### Default Location
Default fallback location: **Hanoi, Vietnam** (21.0285°N, 105.8542°E)

Change in `js/weather.js`:
```javascript
const DEFAULT_LOCATION = {
  name: 'Hanoi, Vietnam',
  lat: 21.0285,
  lon: 105.8542
};
```

## 📱 Responsive Breakpoints

| Device | Width | Layout |
|--------|-------|--------|
| Mobile | 320px | Single column, stacked cards |
| Tablet | 768px | 2-column grid, scrollable forecast |
| Desktop | 1024px | 3-column grid, full layout |

## ♿ Accessibility

- **WCAG AA Compliance**: 4.5:1 text contrast ratio
- **Semantic HTML**: Proper heading hierarchy and landmark regions
- **Keyboard Navigation**: Full keyboard support (Tab, Enter)
- **Focus Indicators**: Visible focus states on all interactive elements
- **Reduced Motion**: Respects `prefers-reduced-motion` media query
- **Screen Reader Support**: ARIA labels on dynamic content

## 📊 Performance

- **Load Time**: < 2 seconds on 4G connection
- **No External Dependencies**: 0 KB framework overhead
- **Asset Optimization**: SVG icons (scalable, small file size)
- **Caching**: Weather data cached in localStorage for 30 minutes

## 🐛 Known Limitations

- Requires HTTPS for geolocation on production (GitHub Pages provides this)
- Geolocation may be denied by user browser settings
- OpenWeatherMap free tier limited to 1000 API calls/day
- No offline functionality (requires internet connection)

## 📝 Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari, Chrome Mobile)

## 🤝 Development

See **AGENTS.md** for detailed development guidelines including:
- Code style conventions
- Git workflow
- Testing approach
- File organization
- Error handling patterns

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- **Design Inspiration**: Apple's Liquid Glass design system
- **Weather Data**: OpenWeatherMap API
- **Icons**: Custom SVG weather icons in Apple SF Symbols style

## 📞 Support

For issues, questions, or suggestions:
1. Check the existing GitHub issues
2. Create a new issue with detailed description
3. Include browser and OS information

---

**Last Updated**: February 2026  
**Status**: Production Ready
