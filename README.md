# CSS Assignment 6: Responsive Hamburger Menu

For this assignment, I created a responsive header and landing page for "Laundry Wallah", a professional laundry service website. The main focus of this assignment is implementing a responsive hamburger menu using only CSS, specifically using the `:focus` and `:focus-within` pseudo-classes rather than a JavaScript script or the checkbox hack.

## Toggling with `:focus` and `:focus-within`

Instead of using a hidden checkbox to toggle the menu state, this implementation relies on native HTML element focus states to control the menu visibility.

### How it works:
1. **The Wrapper Container**: I wrapped both the hamburger button and the navigation links inside a `.navigation` container.
2. **Opening the Menu**: On mobile screens, when a user clicks or taps the menu button (`.menu-btn`), the button receives focus. In CSS, we catch this with `.menu-btn:focus` and set the navigation menu (`.nav`) to `display: block;`.
3. **Keeping the Menu Open**: When a user selects or tabs to one of the links inside the navigation menu, focus shifts from the button to the link. Under a simple `:focus` rule on the button, this would immediately hide the menu. To keep it open while the user interacts with the links, I used the `:focus-within` pseudo-class on the parent `.navigation` container. As long as focus is active *anywhere* inside the `.navigation` container, the menu stays open.
4. **Closing the Menu**: Clicking or tapping anywhere outside of the menu area removes focus from the container, which automatically hides the navigation menu.

## Accessibility and Semantics

The previous setup used a `<label>` element pointing to a hidden checkbox. However, a `<label>` is not a semantic button and does not receive keyboard focus natively. 

Updating this to a native `<button>` element provides several benefits:
* It is natively keyboard-accessible and focusable using the `Tab` key.
* It is screen-reader friendly and uses an `aria-label="Toggle Menu"` to communicate its purpose.
* It provides a cleaner and more standard HTML structure.

## CSS Implementation Details

The core CSS selectors used to manage the menu toggle state and animate the hamburger icon into an "X" are:

```css
/* Show the menu when button is focused or navigation is active */
.menu-btn:focus ~ .nav,
.navigation:focus-within .nav {
    display: block;
}

/* Rotate the hamburger bars into an X when open */
.menu-btn:focus span:nth-child(1),
.navigation:focus-within .menu-btn span:nth-child(1) {
    transform: rotate(45deg) translate(6px, 6px);
}

.menu-btn:focus span:nth-child(2),
.navigation:focus-within .menu-btn span:nth-child(2) {
    opacity: 0;
}

.menu-btn:focus span:nth-child(3),
.navigation:focus-within .menu-btn span:nth-child(3) {
    transform: rotate(-45deg) translate(6px, -6px);
}
```

This approach allows us to create a responsive, animated header menu using only native HTML and CSS features.