# Product Recommendations Widget

A responsive product carousel widget built with Swiper.js that integrates with an external API to display recommended products.

## Features

### ✅ Responsive Design
- **Mobile**: 1 product per slide
- **Tablet** (640px+): 2 products per slide
- **Desktop** (1024px+): 3 products per slide
- Optimized layouts and typography for all screen sizes

### ✅ API Integration
- Fetches product recommendations from external API
- **API Endpoint**: `https://australia-southeast1-stepone-backend.cloudfunctions.net/getProductRecommendations`
- Comprehensive error handling with retry functionality
- Loading state with animated spinner
- Fallback for missing product images

### ✅ Analytics Tracking
Mock analytics function that tracks the following events:

| Event Type | Description |
|------------|-------------|
| `widget-load` | Widget initialization |
| `products-loaded` | Products successfully fetched from API |
| `product-click` | User clicks on a product card |
| `add-to-cart` | User clicks "Add to Cart" button |
| `slide-view` | User views a specific slide |
| `navigation-next` | Next button clicked |
| `navigation-prev` | Previous button clicked |
| `pagination-click` | Pagination dot clicked |
| `carousel-end-reached` | User reaches end of carousel |
| `api-error` | API request fails |
| `error` | Error state displayed |

All events are logged to the browser console with detailed metadata including:
- Widget ID
- Event type
- Product data (where applicable)
- Timestamp
- User agent
- Screen size

### ✅ User Experience
- Smooth carousel transitions
- Navigation arrows
- Pagination dots (clickable)
- Scrollbar indicator
- Hover effects on product cards
- "Add to Cart" functionality
- Product detail view on card click

## Setup

### Installation

No build process required! Simply open the HTML file in a browser:

```bash
open index.html
```

Or use a local server:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx http-server
```

Then navigate to `http://localhost:8000`

## File Structure

```
growth-engineering/
├── index.html          # Main widget implementation
└── README.md          # This file
```

## Technologies Used

- **HTML5** - Semantic markup
- **CSS3** - Responsive design with Flexbox and media queries
- **JavaScript (ES6+)** - Fetch API, async/await
- **Swiper.js v12** - Carousel functionality (loaded via CDN)

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Analytics Integration

The widget includes a mock `track()` function that logs events to the console. To integrate with a real analytics service:

```javascript
function track(widgetId, eventType, productData) {
    const eventData = {
        widgetId,
        eventType,
        productData,
        timestamp: new Date().toISOString(),
        userAgent: navigator.userAgent,
        screenSize: `${window.innerWidth}x${window.innerHeight}`
    };

    // Replace this with your analytics service
    // Example: Google Analytics
    // gtag('event', eventType, eventData);

    // Example: Segment
    // analytics.track(eventType, eventData);

    // Example: Custom API
    // fetch('/api/analytics', {
    //     method: 'POST',
    //     body: JSON.stringify(eventData)
    // });
}
```

## API Response Format

The widget expects the following JSON structure from the API:

```json
[
  {
    "id": 6770842632264,
    "title": "Product Title",
    "handle": "product-handle",
    "product_type": "Product Type",
    "images": [
      "https://example.com/image1.jpg",
      "https://example.com/image2.jpg"
    ]
  }
]
```

## Error Handling

The widget includes robust error handling:

1. **API Errors**: Network failures, HTTP errors, or invalid responses trigger the error state
2. **Empty Response**: If API returns no products, error state is shown
3. **Image Load Failures**: Fallback placeholder image displayed
4. **Retry Mechanism**: Users can click "Retry" button to attempt reload

## Customization

### Styling

Colors, fonts, and spacing can be customized in the `<style>` section:

```css
.slide button {
    background: #000;  /* Change button color */
    color: white;
}

.swiper-slide:hover {
    transform: translateY(-4px);  /* Adjust hover effect */
}
```

### Swiper Configuration

Modify carousel behavior in the JavaScript:

```javascript
const swiper = new Swiper('.swiper', {
    loop: true,           // Enable infinite loop
    spaceBetween: 30,     // Space between slides
    slidesPerView: 1,     // Slides visible at once
    // ... more options
});
```

## Performance Considerations

- Images lazy load by default with Swiper
- Minimal dependencies (only Swiper.js)
- CDN-hosted libraries for optimal caching
- Efficient DOM manipulation
- Debounced event tracking possible (not implemented)

## Future Enhancements

- [ ] Add product filtering/sorting
- [ ] Implement skeleton loading state
- [ ] Add image gallery lightbox
- [ ] Include product ratings/reviews
- [ ] Add wishlist functionality
- [ ] Implement A/B testing variants
- [ ] Add keyboard navigation support
- [ ] Implement swipe gestures on mobile
- [ ] Add accessibility improvements (ARIA labels)

## License

MIT

## Contact

For questions or issues, please contact the development team.
