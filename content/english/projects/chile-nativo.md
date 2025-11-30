---
title: "Chile Nativo: Patagonia Travel Website"
description: "In this post I am going to share my experience on building the frontend for Chile Nativo, a travel tour website for Patagonia experiences, implementing a Figma design using Vue 3, Laravel Mix, and modern frontend technologies."
images:
  - "images/project/chile-nativo/home.png"
date: 2024-01-15T12:00:00+06:00
tags: ["Vue 3", "Laravel Mix", "WordPress", "Themosis", "SCSS", "JavaScript", "Figma"]
categories: ["Projects"]
draft: false
slug: "chile-nativo-patagonia-travel-website"
---

Chile Nativo is a travel tour website for Patagonia experiences, built on top of WordPress with the Themosis framework, featuring a modern frontend implementation based on a Figma design using Vue 3, Laravel Mix, and a comprehensive SCSS architecture.

### Outline

- The project
- Design implementation
- The stack
- Frontend architecture
- Key features
- Conclusion
- Live website

### The project

Chile Nativo is a travel company specializing in Patagonia tours, offering experiences in destinations like Torres del Paine, Tierra del Fuego, and Isla Navarino. The website serves as the primary platform for showcasing tours, managing bookings, and providing information about their travel experiences.

The frontend development was based on a comprehensive Figma design, requiring pixel-perfect implementation of complex UI components, interactive forms, filtering systems, and responsive layouts that work seamlessly across all devices.

### Design implementation

The entire frontend was built from a detailed Figma design, ensuring:

- **Pixel-perfect accuracy**: Matching the design specifications precisely
- **Responsive design**: Implementing breakpoints and mobile-first approach
- **Component consistency**: Maintaining design system patterns throughout
- **Interactive elements**: Translating static designs into dynamic, interactive components
- **Animation and transitions**: Implementing smooth user experience enhancements

### The stack

The frontend stack consists of:

- **Vue 3.2.4**: Modern reactive framework for building interactive components
- **Laravel Mix 6.0**: Asset compilation and bundling
- **SCSS**: Advanced styling with a well-organized architecture
- **Pinia 2.3.1**: State management for Vue applications
- **Vee-Validate 4.15.0**: Form validation with Yup schemas
- **Axios 1.6.8**: HTTP client for API requests
- **Splide.js 4.1.4**: Modern carousel and slider components
- **Headroom.js**: Header behavior on scroll
- **Plyr 3.7.8**: Video player implementation
- **SweetAlert2**: Modern alert dialogs
- **jQuery 3.7.1**: Legacy support and DOM manipulation utilities

### Frontend architecture

#### Vue components

The application features a comprehensive set of Vue 3 components organized by functionality:

**Filtering and Search Components:**
- `ToursFilter.vue`: Advanced tour filtering with multiple criteria
- `TourDatesFilter.vue`: Date-based filtering for tour availability
- `ToursFilterDropdown.vue` & `ToursFilterDropdownMobile.vue`: Responsive filter dropdowns
- `TestimonialsFilter.vue`: Filtering system for customer testimonials
- `NewsFilter.vue`: Blog and news filtering
- `SearchResults.vue`: Search results display with pagination

**Form Components:**
- `PersonalizedTripForm.vue`: Multi-step form for custom trip requests with validation
- `ContactFormSimple.vue`: Contact form with reCAPTCHA integration
- `FormHelp.vue`: Help center form
- `FormGiftCard.vue`: Gift card purchase form
- `FormCareers.vue`: Job application form
- `NewsletterForm.vue`: Newsletter subscription

**Card Components:**
- `Tour.vue` & `TourLoading.vue`: Tour card display with loading states
- `TourDate.vue` & `TourDateLoading.vue`: Tour date selection cards
- `Testimonial.vue` & `TestimonialLoading.vue`: Customer testimonial cards
- `Blog.vue` & `BlogLoading.vue`: Blog post cards
- `Team.vue` & `TeamLoading.vue`: Team member cards
- `ResourceCard.vue` & `ResourceLoading.vue`: Resource display cards

**Utility Components:**
- `Pagination.vue`: Reusable pagination component
- `Select.vue`: Custom select dropdown with search
- `Loader.vue` & `LoaderFullScreen.vue`: Loading indicators
- `EmptyState.vue`: Empty state displays
- `ContentResources.vue`: Resource content management
- `TeamTabsFilter.vue`: Tabbed team member filtering

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
│   ├── _colors.scss
│   ├── _fonts.scss
│   └── _reset.scss
└── components/        # Component-specific styles
    └── [125 component files]
```

**Key SCSS features:**
- **BEM methodology**: Consistent naming convention throughout
- **Media query mixins**: Using `sass-mq` for responsive design
- **Modular architecture**: Each component has its own SCSS file
- **Abstract layer**: Reusable variables, mixins, and functions
- **Vue transitions**: Custom transition styles for Vue components

#### JavaScript architecture

The JavaScript is organized into two main entry points:

**Main application (`app.js`):**
- Initializes core application functionality
- Sets up jQuery plugins and utilities
- Handles legacy browser support

**Vue application (`vue/main.js`):**
- Configures Vue 3 app with Pinia for state management
- Registers global Vue components
- Sets up Vee-Validate configuration
- Integrates third-party Vue plugins (VueTelInput, etc.)

**Component utilities (`app/components/`):**
- `header.js`: Header behavior and navigation
- `footer.js`: Footer functionality
- `splide.js`: Carousel initialization
- `slick.js`: Legacy carousel support
- `accordions.js`: Accordion interactions
- `tabs.js`: Tab functionality
- `scrollTrigger.js`: Scroll-based animations
- `video.js`: Video player setup
- `sticky-sidebar.js`: Sticky sidebar behavior

### Key features

#### Multi-step forms

The `PersonalizedTripForm.vue` component implements a sophisticated multi-step form with:
- Step-by-step navigation with progress indicators
- Form validation using Vee-Validate and Yup schemas
- Dynamic form fields based on user selections
- Phone number input with international support (VueTelInput)
- reCAPTCHA integration for spam protection
- Loading states and error handling

#### Advanced filtering system

The tour filtering system (`ToursFilter.vue`) provides:
- Multiple filter criteria (destination, activity type, trip type, month)
- Real-time filtering with URL parameter synchronization
- Responsive design with mobile accordion interface
- Custom select components with search functionality
- Empty states and loading indicators
- Integration with WordPress backend via Axios

#### Responsive design

The entire website is fully responsive with:
- Mobile-first approach
- Breakpoint management using `sass-mq`
- Touch-friendly interactions
- Optimized images and assets
- Performance optimizations for mobile devices

#### Performance optimizations

- **Code splitting**: Laravel Mix extracts vendor libraries
- **Asset versioning**: Automatic cache busting
- **Image optimization**: Lazy loading and responsive images
- **Minification**: Production builds are minified and optimized
- **Tree shaking**: Unused code elimination in production

#### Accessibility

- Semantic HTML structure
- ARIA labels where appropriate
- Keyboard navigation support
- Focus management in forms
- Screen reader considerations

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

### Conclusion and final thoughts

Building the Chile Nativo frontend from a Figma design was an excellent opportunity to:

- **Master Vue 3**: Working with the Composition API, reactive systems, and modern Vue patterns
- **Implement complex forms**: Multi-step forms with validation, international phone inputs, and reCAPTCHA
- **Build scalable architecture**: Organizing 40+ Vue components and 125+ SCSS files in a maintainable structure
- **Optimize performance**: Implementing code splitting, lazy loading, and production optimizations
- **Ensure design fidelity**: Translating Figma designs into pixel-perfect implementations
- **Handle responsive design**: Creating seamless experiences across all device sizes

The project demonstrates proficiency in:
- Modern JavaScript frameworks (Vue 3)
- Build tools and asset compilation (Laravel Mix, Webpack)
- CSS architecture and methodologies (SCSS, BEM)
- Form validation and user experience
- Component-based development
- Design system implementation

The integration with WordPress/Themosis backend required careful consideration of server-side rendering, API endpoints, and content management workflows, making this a full-stack frontend implementation.

### Live website:

https://chilenativo.travel/

### Figma prototype:

https://www.figma.com/proto/ywHPhSP1UfYUAE8eWVQv4L/Dise%C3%B1o-Desktop---Chile-Nativo?node-id=289-3912&m=dev&scaling=min-zoom&content-scaling=fixed&page-id=289%3A3911&starting-point-node-id=289%3A3912
