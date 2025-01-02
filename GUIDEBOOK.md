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
