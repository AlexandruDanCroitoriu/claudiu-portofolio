# GitHub Copilot Instructions

## Project Overview
This is a portfolio website for guitarist/composer Claudiu Marian Spataru, built with Vue 3, Vite, and Tailwind CSS. It's a single-page application (SPA) with a light, warm aesthetic inspired by the provided reference layout.

## Technology Stack
- **Frontend Framework**: Vue 3 with Composition API
- **Build Tool**: Vite
- **CSS Framework**: Tailwind CSS v4.1.11
- **Routing**: Vue Router v4.5.1
- **Package Manager**: npm
 

## Project Structure
```
src/
├── App.vue              # Main app component with all sections
├── main.js              # App entry point
├── style.css            # Global styles
├── components/          # Reusable Vue components
│   ├── HeroLight.vue
│   ├── AboutLight.vue
│   └── FooterSection.vue
├── data/
│   └── claudiuData.js     # Centralized data store
└── assets/
  └── images/          # Images used by sections
```

## Design Guidelines
- **Theme**: Light, warm, modern, and minimalistic
- **Color Palette**: Cream backgrounds, warm amber accents, slate text
- **Typography**: Clean, modern fonts that convey clarity and musicality
- **Layout**: Single-page with smooth scrolling sections
- **Spacing**: Generous whitespace, minimal clutter
- **Imagery**: High-quality guitar performance and studio photos

## Coding Standards
1. **Vue 3 Composition API**: Use `<script setup>` syntax for all components
2. **Component Structure**: Follow the pattern of script, template, style blocks
3. **Props & Emits**: Use proper TypeScript-style prop definitions when possible
4. **Tailwind Classes**: Prefer utility classes over custom CSS
5. **Responsive Design**: Mobile-first approach with responsive utilities
6. **Data Management**: Centralize data in `src/data/claudiuData.js`

## Component Guidelines
- Each section component should be self-contained and reusable
- Use props for dynamic content when appropriate
- Emit events for parent-child communication
- Keep components focused on a single responsibility
- Follow consistent naming conventions (PascalCase for components)

## Data Structure
All content data is stored in `src/data/claudiuData.js` with the following structure:
- `personal`: Basic information, contact details, images
- `credentials`: Professional certifications and qualifications
- `services`: Detailed service offerings with descriptions and pricing
- `whyChooseMe`: Unique selling propositions
- `testimonials`: Client feedback and reviews
- `socialMedia`: Links to social platforms
- `contact`: Contact form configuration and details

## Styling Conventions
- Use Tailwind utility classes for styling
- Custom CSS should be minimal and placed in component `<style>` blocks
- Prefer light theme classes: `bg-amber-50`, `bg-white`, `text-zinc-900`, `text-slate-700`
- Consistent spacing using Tailwind's spacing scale
- Use `container` class with proper centering for main content areas

## Development Practices
- Keep components small and focused
- Use semantic HTML elements
- Ensure accessibility with proper ARIA labels
- Optimize images and use appropriate formats
- Test responsiveness across different screen sizes
- Use Vue 3 reactivity features appropriately (ref, reactive, computed)

## Performance Considerations
- Lazy load components when appropriate
- Optimize images with proper sizing and formats
- Use Vite's built-in optimizations
- Minimize bundle size by avoiding unnecessary dependencies
- Implement proper caching strategies

## Content Guidelines
- Maintain professional tone throughout
- Focus on guitar performance, composition, and coaching
- Use action-oriented language for CTAs (listen, book, learn)
- Keep text concise but informative
- Highlight Claudiu's musical strengths and versatility
- Include social proof and testimonials when available

## Integration Points
- Social media links and sharing capabilities
- Contact form (client-side only)
- Mobile-responsive navigation
- Smooth scrolling between sections

## Testing Approach
- Test component functionality in isolation
- Verify responsive design on multiple devices
- Check cross-browser compatibility
- Validate form submissions and widget integrations
- Ensure smooth animations and transitions

## Deployment
- Build with `npm run build`
- Static site deployment ready
- Optimized for CDN delivery
- Environment-specific configurations in Vite config

## Future Enhancements
When suggesting improvements or new features, consider:
- Progressive Web App (PWA) capabilities
- Advanced animations and micro-interactions
- Music-specific integrations (playlists, video embeds)
- Blog or notes for releases, shows, and guitar tips
- Client portal functionality
- Payment integration for lessons or bookings
- SEO optimizations and meta tags
- Analytics integration

## Code Examples
When generating code, follow these patterns:

### Component Template
```vue
<script setup>
import { ref, computed, onMounted } from 'vue'
import { claudiuData } from '@/data/claudiuData.js'

// Component logic here
</script>

<template>
  <section class="bg-amber-50 text-zinc-900 py-16">
    <!-- Component content -->
  </section>
</template>

<style scoped>
/* Minimal custom styles if needed */
</style>
```

### Responsive Design
```vue
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  <!-- Use responsive grid patterns -->
</div>
```

### Dark Theme Colors
```vue
<div class="bg-white text-zinc-900 border-[#F1DEC6] hover:bg-amber-50">
  <!-- Consistent light theme usage -->
</div>
```
