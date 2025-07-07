# HTML Project with RagKB Integration

This project demonstrates how to integrate a Vite-built React application into a traditional HTML website.

## Project Structure

```
html-project/
├── index.html          # Hello World page
├── chatbot.html        # Page with RagKB integration
└── README.md          # This file
```

## Files Used from Vite Build

The integration uses the following files from your Vite build output (`../dist/`):

- `ragkb.iife.js` - The main application bundle (IIFE format)
- `style.css` - The application styles

## How to Run

1. **Using a local server** (recommended):

   ```bash
   # Using Python 3
   python -m http.server 8000

   # Using Node.js (if you have http-server installed)
   npx http-server -p 8000

   # Using PHP
   php -S localhost:8000
   ```

2. **Open in browser**:
   - Navigate to `http://localhost:8000/html-project/`
   - Click on "Open Chatbot" to see the integration

## Integration Details

### Key Components

1. **React Dependencies**: The HTML pages include React and ReactDOM from CDN, which are required for the IIFE build format.

2. **CSS Integration**: The built CSS file is linked directly in the HTML head.

3. **JavaScript Integration**: The built JS file is loaded as a script tag, making the `window.RagKB` object available.

4. **Initialization**: The application is initialized by calling `window.RagKB.init('container-id')`.

### Code Example

```html
<!-- Include React dependencies -->
<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

<!-- Include your built files -->
<link rel="stylesheet" href="path/to/style.css" />
<script src="path/to/ragkb.iife.js"></script>

<!-- Container for the app -->
<div id="ragkb-container"></div>

<!-- Initialize the app -->
<script>
  document.addEventListener('DOMContentLoaded', function () {
    if (typeof window.RagKB !== 'undefined') {
      window.RagKB.init('ragkb-container');
    }
  });
</script>
```

## Customization

### Changing the Container ID

You can change the container ID by modifying the `init()` call:

```javascript
window.RagKB.init('my-custom-container-id');
```

### Styling the Container

The container can be styled using CSS:

```css
#ragkb-container {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 20px;
  background: white;
}
```

### Error Handling

The integration includes error handling for cases where the JavaScript file fails to load:

```javascript
if (typeof window.RagKB !== 'undefined') {
  window.RagKB.init('ragkb-container');
} else {
  // Handle error
  console.error('RagKB not loaded');
}
```

## Troubleshooting

### Common Issues

1. **CORS Errors**: Make sure you're serving the files from a web server, not opening them directly as files.

2. **React Not Found**: Ensure the React CDN links are accessible and loading correctly.

3. **File Path Issues**: Verify that the paths to your built files are correct relative to the HTML files.

4. **Container Not Found**: Make sure the container element exists before calling `init()`.

### Debug Mode

To debug integration issues, open the browser console and check for:

- JavaScript errors
- Network requests for the built files
- Whether `window.RagKB` is defined

## Next Steps

1. **Deploy**: Copy the HTML files and your dist folder to your web server
2. **Customize**: Modify the styling and layout to match your website design
3. **Extend**: Add more pages or integrate with your existing website structure

## Notes

- The IIFE build format is used because it's self-contained and doesn't require a module bundler
- React and ReactDOM are loaded from CDN to avoid conflicts with existing React versions
- The integration is designed to be lightweight and easy to implement
