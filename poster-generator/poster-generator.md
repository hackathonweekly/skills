# Poster Generator Skill

Generate beautiful event posters in three distinct styles: Blue-Purple Gradient, Black-White Minimalist, and Brutalist Modern.

## When to Use This Skill

Use this skill when the user wants to:
- Create event posters or announcements
- Generate promotional graphics for hackathons, meetups, or community events
- Design social media graphics (WeChat headers, etc.)
- Create visual content from event information

## Workflow

1. **Extract Event Information**: Parse the user's event content to extract:
   - Event title
   - Date and time
   - Location
   - Speakers/guests (name, title, description)
   - Event description
   - Schedule/agenda
   - Registration URL (will be converted to QR code)

2. **Generate QR Code**: If a registration URL is provided, use qrcode.js library to generate QR code directly in the browser:
   - Include qrcode.js from CDN: `https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js`
   - Generate QR code using JavaScript when the page loads
   - No external API dependency, works offline

3. **Generate 2 HTML Previews**: Create two HTML files with different styles:
   - `style1-minimalist.html` - Black-white minimalist brutalist design
   - `style2-brutalist.html` - Bold brutalist modern design

3. **User Review**: Output the HTML file paths and ask the user to open them in a browser to review.

4. **Iterate if Needed**: If the user wants adjustments, modify the HTML and regenerate.

5. **Convert to PNG**: Once approved, convert each HTML to PNG in two sizes:
   - Poster size: 1080x1440px (3:4 ratio)
   - WeChat header size: 900x383px (landscape)

## Style Guidelines

### Style 1: Black-White Minimalist
- Background: White (#FFFFFF)
- Typography: Bold, uppercase headings; clean body text
- Layout: Grid-based, brutalist aesthetic
- Borders: Thick black borders (8px)
- Accent: None - pure black and white
- Visual elements: Strong geometric shapes, hard edges

### Style 2: Brutalist Modern
- Background: Dark (#1A1A1A) or bold colors
- Typography: Mixed weights, experimental layouts
- Layout: Asymmetric, overlapping elements
- Accent: Neon colors or high contrast
- Visual elements: Raw, unpolished aesthetic with grid overlays

## Assets

The skill includes HackathonWeekly logos in the `assets/` folder:
- `logo.png` / `logo.svg` - Standard logo
- `logo-white.png` - White version for dark backgrounds
- `logo-black.png` - Black version for light backgrounds
- `logo-stack.png` / `logo-stack.svg` - Stacked version

## Technical Implementation

### HTML Generation
- Use inline CSS for portability
- For QR codes: Use qrcode.js library from CDN to generate QR codes in the browser
- Set fixed dimensions (1080x1440px for poster, 900x383px for header)
- Use web-safe fonts with fallbacks

### QR Code Generation
When a registration URL is provided, use qrcode.js library to generate QR code in the browser:
```html
<!-- Include qrcode.js from CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

<!-- QR code container -->
<div id="qrcode"></div>

<!-- Generate QR code -->
<script>
new QRCode(document.getElementById("qrcode"), {
  text: "https://example.com/register",
  width: 140,
  height: 140
});
</script>
```
This approach works offline and doesn't depend on external APIs.

### PNG Conversion
Use the `html2png` skill or Playwright to convert HTML to PNG:
```bash
# Using html2png skill
npx @anthropic-ai/html2png input.html output.png --width 1080 --height 1440
```

## Example Usage

**User**: "Create a poster for our OpenClaw meetup on March 15th at 7pm in Shenzhen. Registration link: https://example.com/register"

**Assistant**:
1. Extracts event details and registration URL
2. Generates QR code from the URL
3. Generates 2 HTML files with different styles, each containing the QR code
4. Outputs: "I've created 2 poster designs with QR code for registration. Please open these files in your browser to review:
   - style1-minimalist.html
   - style2-brutalist.html

   Let me know which style you prefer or if you'd like any adjustments!"
5. After user approval, converts to PNG in both sizes

## Output Files

For each approved style, generate:
- `{event-name}-{style}-poster.png` (1080x1440px)
- `{event-name}-{style}-header.png` (900x383px)
- `{event-name}-{style}.html` (source file)

## Notes

- Always generate both styles initially unless user specifies otherwise
- If user provides a registration URL, automatically convert it to a QR code
- Keep Chinese text readable with appropriate font sizes (min 24px)
- QR codes should be at least 140x140px for easy scanning
- Test color contrast for accessibility
- Use the HackathonWeekly logo prominently in all designs
