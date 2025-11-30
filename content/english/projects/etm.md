---
title: "ETMday: Entrepreneurship Event Website"
description: "In this post I am going to share my experience on building the frontend for ETMday, a large-scale entrepreneurship event website featuring an interactive map, real-time countdown, advanced search, and dynamic content management using Vue 3, Laravel Mix, and modern frontend technologies."
images:
  - "images/project/etm/home.png"
date: 2025-10-06
tags: ["Vue 3", "Laravel Mix", "WordPress", "Themosis", "SCSS", "JavaScript", "Interactive Map", "SVG"]
categories: ["Projects"]
draft: false
slug: "etmday-entrepreneurship-event-website"
---

ETMday (Emprende tu Mente) is a large-scale entrepreneurship event website built on top of WordPress with the Themosis framework, featuring an interactive SVG map, real-time countdown timers, advanced search functionality, and comprehensive content management using Vue 3, Laravel Mix, and modern frontend technologies.

### Outline

- The project
- Key features
- The stack
- Frontend architecture
- Interactive components
- Conclusion
- Live website

### The project

ETMday is Chile's premier entrepreneurship event, bringing together thousands of entrepreneurs, startups, corporates, and strategic partners. The website serves as the central hub for event information, featuring speakers, activities, stands, program schedules, and an interactive event map.

The frontend development required implementing complex interactive features including an SVG-based interactive map with tooltips, real-time countdown timers, advanced filtering and search systems, and dynamic content displays that handle thousands of attendees and hundreds of activities.

### Key features

The website includes several sophisticated features:

- **Interactive SVG Map**: Custom-built interactive map with clickable zones, tooltips, and dynamic content display
- **Real-time Countdown**: Event countdown timer with automatic updates and mobile optimization
- **Advanced Search**: Multi-category search across activities, speakers, stands, and content
- **Dynamic Filtering**: Complex filtering system with tabs, favorites, and downloadable resources
- **Animated Statistics**: Odometer animations for displaying event metrics
- **Content Management**: Comprehensive card components for activities, speakers, stands, and blog posts
- **Form Handling**: Multi-step forms with validation using Vee-Validate
- **Lightbox Galleries**: Image galleries with LightGallery integration
- **Responsive Design**: Fully responsive design optimized for all devices

### The stack

The frontend stack consists of:

- **Vue 3.2.4**: Modern reactive framework for building interactive components
- **Laravel Mix 6.0**: Asset compilation and bundling
- **SCSS**: Advanced styling with organized architecture
- **Vee-Validate 4.15.0**: Form validation with Yup schemas
- **Axios 1.6.8**: HTTP client for API requests
- **Splide.js 4.1.4**: Modern carousel and slider components
- **LightGallery 2.8.3**: Lightbox gallery functionality
- **Odometer 0.4.8**: Animated number counting
- **Headroom.js**: Header behavior on scroll
- **jQuery 3.7.1**: DOM manipulation and legacy support
- **SweetAlert2**: Modern alert dialogs
- **GLightbox 3.3.1**: Alternative lightbox solution

### Frontend architecture

#### Vue components

The application features a comprehensive set of Vue 3 components:

**Card Components:**
- `cards/activities.vue`: Activity cards with favorites functionality
- `cards/speakers.vue`: Speaker cards with modal details
- `cards/stands.vue`: Stand/exhibitor cards
- `cards/blog.vue`: Blog post cards
- `cards/shortcut.vue`: Quick access shortcut cards

**Functional Components:**
- `SectionCards.vue`: Main section component with tabs, filtering, and card display
- `Search.vue`: Advanced search component with multi-category results
- `Form.vue`: Dynamic form component with validation
- `FormCalendar.vue`: Calendar form component
- `CustomFilter.vue`: Reusable filter component
- `CustomSelect.vue`: Custom select dropdown
- `Pagination.vue`: Pagination component

#### JavaScript components

The application includes 17 specialized JavaScript components:

**Interactive Features:**
- `interactiveMap.js`: SVG map interaction with tooltips, zones, and dynamic content
- `countdown.js`: Real-time countdown timer with automatic updates
- `odometer.js`: Animated number counting with scroll triggers
- `map.js`: Map zone interactions and modal displays

**UI Components:**
- `header.js`: Header functionality and navigation
- `headroom.js`: Header hide/show on scroll
- `accordion.js`: Accordion interactions
- `tabs.js`: Tab functionality
- `cards.js`: Card interactions and modals
- `siteModals.js`: Modal management system
- `UI.js`: General UI utilities

**Media Components:**
- `video.js`: Video player setup
- `lightgallery.js`: Lightbox gallery initialization
- `splide.js`: Carousel initialization
- `slick.js`: Legacy carousel support

**Utilities:**
- `scrollTrigger.js`: Scroll-based animations
- `imgToSvg.js`: SVG image conversion utility

#### SCSS architecture

The styling follows a well-organized SCSS architecture:

```
scss/
├── abstracts/          # Variables, mixins, functions
│   ├── _functions.scss
│   ├── _mixins.scss
│   ├── _variables.scss
│   ├── _mq.scss       # Media query mixins
│   └── _keyframes.scss
├── base/              # Base styles and typography
│   ├── _typography.scss
│   ├── _container.scss
│   └── _reset.scss
└── components/        # Component-specific styles
    └── [52 component files]
```

**Key SCSS features:**
- **BEM methodology**: Consistent naming convention
- **Media query mixins**: Using `sass-mq` for responsive design
- **Modular architecture**: Each component has its own SCSS file
- **Component organization**: 52 component-specific SCSS files

### Interactive components

#### Interactive SVG Map

The `interactiveMap.js` component implements a sophisticated SVG-based interactive map:

**Features:**
- **SVG Tooltips**: Dynamically generated tooltips with text wrapping
- **Zone Interactions**: Clickable zones with modal displays
- **Point Markers**: Interactive points with icons and labels
- **Dynamic Content**: Content loaded based on zone/point selection
- **Responsive Design**: Optimized for mobile and desktop

**Technical Implementation:**
- SVG namespace manipulation for tooltip creation
- Text wrapping algorithm for tooltip content
- Path generation for tooltip shapes with rounded corners
- Event delegation for zone and point interactions
- Smooth animations and transitions

#### Real-time Countdown

The `countdown.js` component provides a real-time countdown timer:

**Features:**
- **Automatic Updates**: Updates every second
- **Multi-unit Display**: Days, hours, minutes, and seconds
- **Pluralization**: Proper Spanish pluralization (Día/Días, Hora/Horas)
- **Mobile Optimization**: Simplified display on mobile devices
- **End State Handling**: Automatic transition when countdown ends

#### Advanced Search System

The `Search.vue` component implements a comprehensive search system:

**Features:**
- **Multi-category Search**: Searches across activities, speakers, stands, and other content
- **Category Tabs**: Quick navigation between result categories
- **Result Counts**: Dynamic result counts per category
- **Scroll Navigation**: Smooth scrolling to category sections
- **Carousel Display**: Splide carousels for result display
- **Loading States**: Loading indicators during search
- **Empty States**: User-friendly empty state messages

#### Dynamic Filtering System

The `SectionCards.vue` component provides advanced filtering:

**Features:**
- **Tab Navigation**: Multiple filter tabs
- **Favorites System**: Save and filter favorite items
- **Search Integration**: Inline search within filters
- **Reset Functionality**: Clear all filters with one click
- **Downloadable Resources**: Download buttons for resources
- **URL Synchronization**: Filter state in URL parameters
- **Responsive Design**: Mobile accordion interface

#### Animated Statistics

The `odometer.js` component provides animated number counting:

**Features:**
- **Scroll-triggered**: Animations trigger on scroll
- **Prefix/Suffix Support**: Handles formatted numbers (e.g., "56,000+")
- **Mobile Optimization**: Static display on mobile
- **Smooth Animations**: Odometer theme integration

### Development workflow

The project uses Laravel Mix for asset compilation:

```javascript
// Development
npm run dev          // Compile assets
npm run watch        // Watch for changes
npm run hot          // Hot module replacement

// Production
npm run production   // Optimized production build
```

**BrowserSync integration** provides:
- Live reloading during development
- Synchronized browser testing
- Proxy configuration for WordPress development

### Performance optimizations

- **Code splitting**: Laravel Mix extracts vendor libraries
- **Asset versioning**: Automatic cache busting
- **Image optimization**: Lazy loading and responsive images
- **Minification**: Production builds are minified and optimized
- **Tree shaking**: Unused code elimination in production
- **SVG optimization**: Efficient SVG manipulation and rendering

### Accessibility

- Semantic HTML structure
- ARIA labels for interactive elements
- Keyboard navigation support
- Focus management in forms and modals
- Screen reader considerations
- Proper alt text for images

### Conclusion and final thoughts

Building the ETMday frontend was an excellent opportunity to:

- **Master SVG interactions**: Creating complex interactive SVG maps with dynamic tooltips and zones
- **Implement real-time features**: Building countdown timers and live updates
- **Build advanced search**: Multi-category search with filtering and categorization
- **Handle complex state**: Managing filters, favorites, and dynamic content
- **Optimize performance**: Implementing efficient animations and lazy loading
- **Ensure scalability**: Building components that handle large datasets (thousands of attendees, hundreds of activities)

The project demonstrates proficiency in:
- Modern JavaScript frameworks (Vue 3)
- SVG manipulation and interaction
- Real-time UI updates
- Advanced filtering and search systems
- Build tools and asset compilation (Laravel Mix, Webpack)
- CSS architecture and methodologies (SCSS, BEM)
- Component-based development
- Event-driven architecture

The integration with WordPress/Themosis backend required careful consideration of server-side rendering, API endpoints, and content management workflows, making this a full-stack frontend implementation for a large-scale event.

### Live website:

https://etmday.org/

### Figma Prototype:

https://www.figma.com/proto/mt9fJ8P03M5gf0nQwcU99q/EtM-Day-2025---Dise%C3%B1o?node-id=1-2743&m=dev&scaling=scale-down&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=1%3A2743
