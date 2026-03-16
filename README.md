# QR Code PDF Generator

A simple, frictionless web application that generates QR codes and allows users to download them as PDFs at a configurable square size. Built with HTML, JavaScript, and Bootstrap for a clean, responsive user experience.

## Features

- **Real-time QR Code Generation**: QR codes generate automatically as you type (300ms debounce)
- **Configurable PDF Output**: Set any square output size from 5mm to 50mm (default 10mm × 10mm)
- **Correct PDF Sizing**: Dimensions are passed directly to jsPDF in millimetres — no point conversion required
- **Zero Friction UX**: Field starts empty; clicking into it selects all content so you can type straight over it
- **Character Count Indicator**: Live count with colour feedback (green ≤300 / amber ≤500 / red >500)
- **High Quality Output**: 300 DPI resolution for crisp print quality
- **Responsive Design**: Bootstrap-powered interface that works on all devices
- **Dynamic File Naming**: Downloaded PDF is named to reflect the chosen size (e.g. `qr-code-25mm.pdf`)

## Quick Start

1. **Clone or Download**: Save the HTML file to your local machine
2. **Open in Browser**: Double-click the HTML file or serve it via a web server
3. **Start Using**:
   - Click in the text field and type your content
   - QR code appears instantly in the preview
   - Optionally adjust the output size (5–50mm, default 10mm)
   - Click the download button to get your PDF

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

- **URLs**: Keep under 200–300 characters for optimal scanning (indicated green by the character counter)
- **Text Content**: Up to 500 characters work reliably (amber warning above 300)
- **Complex Data**: Consider using URL shorteners for longer content (red warning above 500)

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
- **Default Size**: 10mm × 10mm
- **Size Range**: 5mm × 5mm to 50mm × 50mm (square, user-configurable)
- **Size Handling**: `targetMM` is passed directly to `pdf.addImage()` — jsPDF's coordinate system is millimetres throughout, no point conversion needed
- **Resolution**: 300 DPI for print quality (`pixels = mm × (300 / 25.4)`)
- **Error Correction**: Medium level (M)
- **Format**: PNG embedded in PDF

### PDF Specifications
- **Page Size**: A4 (210 × 297mm)
- **QR Position**: 20mm from top-left corner
- **Additional Info**: Content preview, size confirmation, timestamp
- **File Naming**: `qr-code-{size}mm.pdf` (e.g. `qr-code-10mm.pdf`)

## Customisation

### Changing the Default Size
The size input defaults to 10mm. To change this, update the `value` attribute on the size input and the reset value in `clearAllData()`:

```html
<!-- In the HTML -->
<input type="number" id="sizeInput" value="10" min="5" max="50" step="1">
```

```javascript
// In clearAllData()
document.getElementById('sizeInput').value = 10;
```

### Adjusting the Size Range
The valid range is controlled in three places — keep them consistent:

```html
<!-- HTML attribute (browser validation) -->
<input type="number" id="sizeInput" min="5" max="50">
```

```javascript
// getTargetMM() — clamps the value used for PDF generation
if (isNaN(raw) || raw < 5) return 5;
if (raw > 50)              return 50;

// downloadAsPDF() — validates before generating
if (isNaN(rawSize) || rawSize < 5 || rawSize > 50) { ... }
```

### Adding Custom Features
The modular structure makes it easy to extend:

- **Batch Processing**: Loop through multiple inputs
- **Custom Styling**: Modify QRious options for colours/logos
- **Different Formats**: Add PNG/SVG download options
- **Non-square Output**: Separate width/height inputs (requires updating `addImage` call)

## Development

### Prerequisites
- Modern web browser with JavaScript enabled
- No build process required — pure HTML/CSS/JS

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
- `pdf.addImage()` takes millimetres directly — `targetMM` is passed straight through with no conversion
- If a viewer reports a different size, check its own scaling/zoom settings

### Scanning Issues
- Ensure adequate quiet zone around the printed QR code
- Use a high-quality printer (300+ DPI recommended)
- Test with multiple QR code reader apps
- Consider reducing data complexity for smaller print sizes (5–10mm)

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

### v1.2.0 (Current)
- ✅ Fixed PDF output size bug: `targetMM` now passed directly to `pdf.addImage()` instead of an incorrectly pre-converted points value
- ✅ Removed redundant `pdfSizePt` calculation (jsPDF coordinate system is mm throughout — no point conversion required)
- ✅ Fixed `textY` positioning below QR image (was also using the incorrect points value)
- ✅ Updated README to remove misleading point-conversion formula references

### v1.1.0
- ✅ Configurable output size (5–50mm) with live button label update
- ✅ Empty field on load; focus selects all content for instant overtyping
- ✅ Live character count with colour-coded thresholds (green / amber / red)
- ✅ Dynamic PDF filename reflects chosen size
- ✅ Favicon `<link>` tags correctly placed inside `<head>`
- ✅ Clear Data resets size to 10mm as well as clearing text

### v1.0.0
- ✅ Real-time QR generation with debouncing
- ✅ PDF output with Bootstrap UI and Bootstrap Icons
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
