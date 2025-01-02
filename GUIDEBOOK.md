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
