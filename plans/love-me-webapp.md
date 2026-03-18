# Love Me Webapp - Plan

## Context
User wants a simple, fun webapp with:
- A question: "Do you love me?"
- Two buttons: "Yes" and "No"
- The "No" button runs away when the mouse hovers over it (can never be clicked)
- Clicking "Yes" shows: "I love u too babi"

## Approach
Create a simple static HTML file with embedded CSS and JavaScript. This is the simplest approach for a single-file webapp.

**Files to create:**
- `index.html` - Single HTML file containing the entire app

**Implementation details:**
1. **HTML**: Container with heading/question and two button elements
2. **CSS**: Centered layout, styled buttons, hidden message container
3. **JavaScript**:
   - Event listener on "No" button for `mouseover` event
   - On hover, calculate random position within viewport and move button
   - Event listener on "Yes" button to show the sweet message
   - Optional: prevent default button behavior

## Verification
- Open `index.html` in a browser
- Test hovering over "No" button - it should move away
- Test clicking "Yes" button - should display the message
- Test that "No" button cannot be clicked
