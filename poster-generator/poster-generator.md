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
   - QR code or registration info

2. **Generate 3 HTML Previews**: Create three HTML files with different styles:
   - `style1-blue-purple.html` - Blue-purple gradient with modern design
   - `style2-minimalist.html` - Black-white minimalist brutalist design
   - `style3-brutalist.html` - Bold brutalist modern design

3. **User Review**: Output the HTML file paths and ask the user to open them in a browser to review.

4. **Iterate if Needed**: If the user wants adjustments, modify the HTML and regenerate.

5. **Convert to PNG**: Once approved, convert each HTML to PNG in two sizes:
   - Poster size: 1080x1440px (3:4 ratio)
   - WeChat header size: 900x383px (landscape)

## Style Guidelines

### Style 1: Blue-Purple Gradient
- Background: Linear gradient from blue (#4F46E5) to purple (#9333EA)
- Typography: Clean, modern sans-serif (Inter, SF Pro)
- Layout: Centered content with ample white space
- Accent: Yellow highlights (#FCD34D) for important info
- Visual elements: Subtle geometric shapes, soft shadows

### Style 2: Black-White Minimalist
- Background: White (#FFFFFF)
- Typography: Bold, uppercase headings; clean body text
- Layout: Grid-based, brutalist aesthetic
- Borders: Thick black borders (8px)
- Accent: None - pure black and white
- Visual elements: Strong geometric shapes, hard edges

### Style 3: Brutalist Modern
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
- Embed base64 images or use local file paths
- Set fixed dimensions (1080x1440px for poster, 900x383px for header)
- Use web-safe fonts with fallbacks

### PNG Conversion
Use the `html2png` skill or Playwright to convert HTML to PNG:
```bash
# Using html2png skill
npx @anthropic-ai/html2png input.html output.png --width 1080 --height 1440
```

## Example Usage

**User**: "Create a poster for our OpenClaw meetup on March 15th at 7pm in Shenzhen"

**Assistant**:
1. Extracts event details
2. Generates 3 HTML files with different styles
3. Outputs: "I've created 3 poster designs. Please open these files in your browser to review:
   - style1-blue-purple.html
   - style2-minimalist.html
   - style3-brutalist.html

   Let me know which style you prefer or if you'd like any adjustments!"
4. After user approval, converts to PNG in both sizes

## Output Files

For each approved style, generate:
- `{event-name}-{style}-poster.png` (1080x1440px)
- `{event-name}-{style}-header.png` (900x383px)
- `{event-name}-{style}.html` (source file)

## Notes

- Always generate all 3 styles initially unless user specifies otherwise
- Keep Chinese text readable with appropriate font sizes (min 24px)
- Ensure QR codes are large enough to scan (min 200x200px)
- Test color contrast for accessibility
- Use the HackathonWeekly logo prominently in all designs
