# Guidelines for Developing Robust React.js Components

1.  Forms and Input Handling

    - Always disable the form submit button and show a loader while an HTTP request is in progress to prevent duplicate submissions.
    - Validate user input on blur and/or on submit, providing clear and actionable error messages.
    - Use controlled components (value and onChange) for inputs to manage state effectively.
    - Set default values for forms to prevent uncontrolled behavior.

2.  HTTP Requests

    - Show a loading spinner or skeleton screen while fetching data.
    - Handle errors gracefully and display meaningful messages to the user (e.g., “Failed to load, please try again”).
    - Use try-catch for async operations and wrap API calls in reusable utility functions.
    - Cancel or debounce API calls on user input to prevent excessive requests (e.g., in search functionality).

3.  Button States

    - Disable buttons while a task is in progress (e.g., a form is submitting or data is loading).
    - Use aria-busy attributes for accessibility during loading states.
    - Change button text to indicate action progress (e.g., "Saving..." or "Loading...").

4.  Rendering and Data Display

    - Always check for null, undefined, or empty states before rendering data (e.g., data && data.length > 0).
    - Show fallback UIs for empty or error states (e.g., “No results found” or “Something went wrong”).
    - Use key props correctly in lists to avoid rendering issues (e.g., use unique IDs, not indices).

5.  CSS and Styling

    - Add hover, focus, and active states for interactive elements (e.g., buttons, links).
    - Use cursor: not-allowed for disabled buttons to improve user feedback.
    - Ensure text is readable with proper contrast ratios (use a contrast checker tool).

6.  Error Handling

    - Always wrap components that can fail with error boundaries or a custom error UI.
    - Handle promise rejections in API calls and show user-friendly messages.
    - Log errors to the console or send them to a monitoring tool (e.g., Sentry).

7.  Accessibility (a11y)

    - Use semantic HTML (`<button>`, `<label>`, `<main>`, etc.) to ensure proper navigation for screen readers.
    - Add aria-label attributes to buttons, links, and icons without visible text.
    - Ensure keyboard navigation works seamlessly (e.g., tab order, Enter/Space to activate buttons).

8.  Component Behavior

    - Use React.memo for components that don't need to re-render on every state change.
    - Avoid inline functions in render methods to prevent unnecessary renders.
    - Clean up side effects using useEffect cleanup functions (e.g., clearing timers, unsubscribing).

9.  Events and Interactions

    - Prevent default form submissions with event.preventDefault() in custom handlers.
    - Add debounce or throttle for frequent events like scroll, resize, or input changes.
    - Provide feedback for user actions (e.g., “Item added to cart” toast notification).

10. Code Practices

    - Always destructure props and state for readability.
    - Use constants for repetitive strings or values to avoid typos.
    - Avoid hardcoded styles in JSX; use CSS classes or inline styles via objects.

11. State Management

    - Keep local state minimal; avoid duplicating global state in local state.
    - Reset forms or component states after successful actions (e.g., clear input after submitting).
    - Use useReducer for complex state logic.

12. Miscellaneous Tips

    - Always sanitize user inputs, especially if rendering HTML (e.g., using react-html-parser).
    - Show tooltips or hints for non-obvious actions.
    - Test components for responsiveness using developer tools or frameworks like Tailwind.

13. Console Logs

    - Always remove all console.log, console.error, and console.warn statements before finalizing and deploying the code. Use a logging library for controlled logs in development and production if needed.

14. Cleanup Effects

    - Ensure all subscriptions, event listeners, and intervals set in useEffect are cleaned up in the return function to prevent memory leaks.
    - Example:

    ```javascript
    useEffect(() => {
      const timer = setInterval(() => console.log('Running'), 1000);
      return () => clearInterval(timer); // Cleanup
    }, []);
    ```
