# QR Code PDF Generator

A simple, frictionless web application that generates QR codes and allows users to download them as PDFs with precise 10mm × 10mm dimensions. Built with HTML, JavaScript, and Bootstrap for a clean, responsive user experience.

## Features

- **Real-time QR Code Generation**: QR codes generate automatically as you type (300ms debounce)
- **Precise PDF Output**: Generates QR codes at exactly 10mm × 10mm for print applications
- **Zero Friction UX**: No buttons to click for generation, auto-clears example text
- **High Quality Output**: 300 DPI resolution for crisp print quality
- **Responsive Design**: Bootstrap-powered interface that works on all devices
- **Data Validation**: Supports various data types with appropriate capacity limits

## Quick Start

1. **Clone or Download**: Save the HTML file to your local machine
2. **Open in Browser**: Double-click the HTML file or serve it via a web server
3. **Start Using**: 
   - Click in the text field (example text auto-clears)
   - Type your content
   - QR code appears instantly
   - Click download to get your 10mm × 10mm PDF

## Technology Stack

- **Frontend Framework**: Bootstrap 5.3.2
- **QR Code Generation**: QRious 4.0.2
- **PDF Generation**: jsPDF 2.5.1
- **Icons**: Bootstrap Icons 1.11.2
- **Languages**: HTML5, CSS3, JavaScript ES6+

## Data Capacity Limits

The QR code can store different amounts of data depending on the character type:

| Data Type | Maximum Characters | Use Cases |
|-----------|-------------------|-----------|
| **Numeric** | 7,089 characters | ID numbers, codes, phone numbers |
| **Alphanumeric** | 4,296 characters | URLs, basic text (A-Z, 0-9, $%*+-./: space) |
| **Binary/Byte** | 2,953 characters | Any UTF-8 text, special characters |
| **Kanji/Kana** | 1,817 characters | Japanese characters |

### Practical Recommendations

- **URLs**: Keep under 200-300 characters for optimal scanning
- **Text Content**: Up to 500-800 characters work reliably
- **Complex Data**: Consider using URL shorteners for longer content

## File Structure

```
qr-code-pdf-generator/
├── index.html              # Main application file
├── README.md               # This documentation
```

## Browser Compatibility

- **Chrome**: 60+ ✅
- **Firefox**: 55+ ✅
- **Safari**: 12+ ✅
- **Edge**: 79+ ✅
- **Mobile Browsers**: iOS Safari 12+, Chrome Mobile 60+ ✅

## Usage Examples

### Basic URL
```
https://example.com
```

### Contact Information (vCard)
```
BEGIN:VCARD
VERSION:3.0
FN:John Doe
ORG:Company Name
TEL:+1234567890
EMAIL:john@example.com
END:VCARD
```

### WiFi Network
```
WIFI:T:WPA;S:NetworkName;P:password123;H:false;;
```

### SMS Message
```
sms:+1234567890:Hello from QR code!
```

## Technical Specifications

### QR Code Output
- **Physical Size**: Exactly 10mm × 10mm (1cm × 1cm)
- **Resolution**: 300 DPI for print quality
- **Error Correction**: Medium level (M)
- **Format**: PNG embedded in PDF

### PDF Specifications
- **Page Size**: A4 (210 × 297mm)
- **QR Position**: 20mm from top-left corner
- **Additional Info**: Content preview, size confirmation, timestamp
- **File Naming**: `qr-code-10mm.pdf`

## Customization

### Changing QR Code Size
To modify the output size, update the calculation in the `downloadAsPDF()` function:

```javascript
// Current: 10mm calculation
const targetMM = 10;
const currentMM = 11.6;
const currentPoints = 11.68;
const finalPoints = currentPoints * (targetMM / currentMM);

// For different size, change targetMM value
const targetMM = 20; // For 20mm × 20mm
```

### Styling Modifications
The app uses standard Bootstrap classes. Key elements:

```css
/* Main container */
.container.py-5

/* QR preview area */
#qrcode

/* Download button */
.btn.btn-success.btn-lg
```

### Adding Custom Features
The modular structure makes it easy to add features:

- **Batch Processing**: Loop through multiple inputs
- **Custom Styling**: Modify QRious options for colors/logos
- **Different Formats**: Add PNG/SVG download options
- **Size Presets**: Create multiple size options

## Development

### Prerequisites
- Modern web browser with JavaScript enabled
- No build process required - pure HTML/CSS/JS

### Testing
Test with various data types:
- Short URLs (< 50 chars)
- Long URLs (200+ chars)
- Text with special characters
- Unicode content
- vCard contact information

## Troubleshooting

### QR Code Not Appearing
- Check browser console for JavaScript errors
- Ensure all CDN resources are loading
- Verify internet connection for external libraries

### Incorrect PDF Size
- The app auto-calibrates based on measured output
- Current calibration: 11.68 points = 11.6mm measured
- Adjust `finalPoints` calculation if needed

### Scanning Issues
- Ensure adequate quiet zone around printed QR code
- Use high-quality printer (300+ DPI recommended)
- Test with multiple QR code reader apps
- Consider reducing data complexity for small prints

## Performance Considerations

- **Debounced Input**: 300ms delay prevents excessive generation
- **Memory Management**: Canvas elements are reused efficiently
- **CDN Loading**: External libraries cached by browser
- **File Size**: Generated PDFs typically < 50KB

## Browser Security

The application:
- ✅ Runs entirely client-side (no data transmission)
- ✅ Uses only standard web APIs
- ✅ No local storage or cookies
- ✅ No external data collection

## License

This project is open source. Feel free to use, modify, and distribute.

## Contributing

Contributions welcome! Areas for improvement:
- Additional output formats (PNG, SVG)
- Batch QR code generation
- Custom styling options
- Advanced error correction settings
- Mobile app conversion

## Changelog

### v1.0.0 (Current)
- ✅ Real-time QR generation with debouncing
- ✅ Precise 10mm × 10mm PDF output
- ✅ Auto-clearing example text
- ✅ Bootstrap UI with proper icons
- ✅ High-resolution 300 DPI output
- ✅ Comprehensive error handling

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Verify browser compatibility
3. Test with different input data
4. Check browser developer console for errors

## Acknowledgments

- **QRious**: Reliable QR code generation library
- **jsPDF**: Client-side PDF generation
- **Bootstrap**: Responsive UI framework
- **Bootstrap Icons**: Professional icon set