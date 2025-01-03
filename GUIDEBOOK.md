# Guidelines for Developing Robust React.js Components

1.  Forms and Input Handling

    - Always disable the form submit button and show a loader while an HTTP request is in progress to prevent duplicate submissions.
    - Validate user input on blur and/or on submit, providing clear and actionable error messages.
    - Use controlled components (`value` and `onChange`) for inputs to manage state effectively.
    - Set default values for forms to prevent uncontrolled behavior.

2.  HTTP Requests

    - Show a loading spinner or skeleton screen while fetching data.
    - Handle errors gracefully and display meaningful messages to the user (e.g., “Failed to load, please try again”).
    - Use `try-catch` for async operations and wrap API calls in reusable utility functions.
    - Cancel or debounce API calls on user input to prevent excessive requests (e.g., in search functionality).

3.  Button States

    - Disable buttons while a task is in progress (e.g., a form is submitting or data is loading).
    - Use `aria-busy` attributes for accessibility during loading states.
    - Change button text to indicate action progress (e.g., "Saving..." or "Loading...").

4.  Rendering and Data Display

    - Always check for **null, undefined, or empty states** before rendering data (e.g., `data && data.length > 0`).
    - Show fallback UIs for empty or error states (e.g., “No results found” or “Something went wrong”).
    - Use `key` props correctly in lists to avoid rendering issues (e.g., use unique IDs, not indices).

5.  CSS and Styling

    - Add **hover, focus, and active states** for interactive elements (e.g., buttons, links).
    - Use `cursor: not-allowed` for disabled buttons to improve user feedback.
    - Ensure text is readable with proper contrast ratios (use a contrast checker tool).

6.  Error Handling

    - Always wrap components that can fail with **error boundaries** or a custom error UI.
    - Handle promise rejections in API calls and show user-friendly messages.
    - Log errors to the console or send them to a monitoring tool (e.g., Sentry).

7.  Accessibility (a11y)

    - Use semantic HTML (`<button>`, `<label>`, `<main>`, etc.) to ensure proper navigation for screen readers.
    - Add `aria-label` attributes to buttons, links, and icons without visible text.
    - Ensure keyboard navigation works seamlessly (e.g., tab order, Enter/Space to activate buttons).

8.  Component Behavior

    - Use `React.memo` for components that don't need to re-render on every state change.
    - Avoid inline functions in `render` methods to prevent unnecessary renders.
    - Clean up side effects using `useEffect` cleanup functions (e.g., clearing timers, unsubscribing).

9.  Events and Interactions

    - Prevent default form submissions with `event.preventDefault()` in custom handlers.
    - Add debounce or throttle for frequent events like `scroll`, `resize`, or `input` changes.
    - Provide feedback for user actions (e.g., “Item added to cart” toast notification).

10. Code Practices

    - Always destructure props and state for readability.
    - Use constants for repetitive strings or values to avoid typos.
    - Avoid hardcoded styles in JSX; use CSS classes or inline styles via objects.

11. State Management

    - Keep local state minimal; avoid duplicating global state in local state.
    - Reset forms or component states after successful actions (e.g., clear input after submitting).
    - Use `useReducer` for complex state logic.

12. Tooltips and Hints

    - Always sanitize user inputs, especially if rendering HTML (e.g., using `react-html-parser`).
    - Show tooltips or hints for non-obvious actions.
    - Example for "copy to clipboard" functionality:
      - Display "Copy" by default.
      - Change to "Copied!" when the user clicks the copy button.
      - Revert back to "Copy" after a few seconds.
      - Use a state variable to manage the tooltip content dynamically.

13. Console Logs

    - Always remove all `console.log`, `console.error`, and `console.warn` statements before finalizing and deploying the code. Use a logging library for controlled logs in development and production if needed.

14. Cleanup Effects

    - Ensure all subscriptions, event listeners, and intervals set in `useEffect` are **cleaned up** in the return function to prevent memory leaks.
    - Example:

    ```javascript
    useEffect(() => {
      const timer = setInterval(() => console.log('Running'), 1000);
      return () => clearInterval(timer); // Cleanup
    }, []);
    ```

15. Default Fallbacks

    - Always provide **fallback content** for dynamic data (e.g., `default` `values`, `loading placeholders`).
    - Example:

    ```javascript
    <h1>{title || 'Default Title'}</h1>
    ```

16. API Response Handling

    - Validate and sanitize API responses to ensure they meet expected data structures before rendering.
    - Use optional chaining (`?.`) to avoid runtime errors for undefined/null values.
    - Example:

    ```javascript
    <p>{user?.name || 'Guest'}</p>
    ```

17. Event Handlers

    - Always debounce expensive event handlers (e.g., `scroll`, `resize`, or `input` changes).
    - Example using `lodash.debounce`:

    ```javascript
    const handleSearch = debounce(query => fetchResults(query), 300);
    ```

18. Button and Link Behavior

    - Disable buttons or links while performing actions (e.g., saving or submitting).
    - Prevent multiple submissions by disabling the button immediately after the first click.
    - Example:

    ```javascript
    const [isSubmitting, setIsSubmitting] = useState(false);
    const handleSubmit = async () => {
      setIsSubmitting(true);
      await submitData();
      setIsSubmitting(false);
    };
    ```

19. Error Messages

    - Show **specific and actionable error messages** instead of generic ones (e.g., “Email is required” instead of “Invalid input”).
    - Use toast notifications or inline error indicators for better UX.

20. Keyboard Navigation

    - Ensure that interactive elements are focusable and usable with the keyboard (e.g., via the `tab` key).
    - Add `onKeyDown` handlers for important actions to support Enter or Space key activation.

21. Image Handling

    - Always provide an `alt` attribute for images to ensure accessibility.
    - Use a fallback image for broken or missing image URLs.
    - Example:

    ```javascript
    <img
      src={imageUrl || fallbackUrl}
      alt='Profile'
      onError={e => (e.target.src = fallbackUrl)}
    />
    ```

22. Code Comments

    - Add comments for complex logic, especially for code that might not be intuitive at first glance.
    - Avoid excessive comments; the code should be self-explanatory where possible.

23. Component Unmounting

    - Handle cleanup logic properly in `useEffect` or component lifecycle methods to prevent unintended behaviors.

24. Avoid Hardcoding

    - Replace hardcoded strings, numbers, or configurations with constants or environment variables.

25. Dependencies

    - Keep an eye on the **dependencies array** in `useEffect` to prevent unnecessary or missing updates.
    - Example:

    ```javascript
    useEffect(() => {
      fetchData();
    }, [dependency]); // Add all required dependencies here
    ```

26. Testing Before Deployment

    - Test the component in all target browsers and screen sizes (mobile, tablet, desktop).
    - Verify behavior with no or slow internet connections to check for fallback states.
    - Simulate user interactions to ensure proper state updates and validations.

27. Loading States

    - Always show a **loading spinner** or skeleton while waiting for data to load. Never leave the UI blank or unresponsive.

28. Avoid Inline Styles

    - Use CSS modules or styled-components for maintainable and reusable styles instead of inline styles.

29. Avoid Using Index as Key

    - Use unique identifiers as `key` in lists to avoid rendering issues and bugs.

30. Error Monitoring

    - Integrate an error tracking tool (e.g., Sentry) to capture errors in production for debugging and monitoring.

31. Mobile Responsiveness

    - Always test for mobile responsiveness. Use flexible layouts (`flexbox`, `grid`) and media queries to adapt to different screen sizes.

32. Environment Variables

    - Include an `.env.example` file in all React.js and Nest.js repositories to list all required environment variables for the project.
    - Ensure the `.env.example` file is always up-to-date with accurate and descriptive placeholders (e.g., `API_URL=<Your API Endpoint>`).
    - Never commit actual `.env` files or sensitive information into version control. Add `.env` to `.gitignore`.
    - Validate that all required environment variables are present at runtime using libraries like `dotenv-safe`.
    - Example `.env.example` file:

    ```plaintext
    REACT_APP_API_URL=<Your API Endpoint>
    REACT_APP_AUTH_KEY=<Your Auth Key>
    ```

33. Environment-Specific Configurations

    - Ensure configurations for different environments (e.g., development, staging, production) are well-documented and included in the `.env.example` file.
    - Always test the application in the environment it is configured for before deployment.

34. Documentation

    - Maintain a `README.md` file that includes:
      - Project setup instructions.
      - How to configure environment variables.
      - Testing and deployment guidelines.
    - Update the documentation whenever new features or dependencies are added.

35. Timestamp Handling

    - Always convert timestamps (including time only) to UTC when saving to ensure consistency across different time zones.
    - Convert timestamps to the local timezone when reading for display purposes, ensuring the user sees time relevant to their location.
    - Use libraries like `date-fns`, `moment`, or `Intl.DateTimeFormat` for robust timezone conversions and formatting.
    - Example for saving to UTC:

    ```javascript
    const saveTimestamp = localTime => {
      const utcTime = new Date(localTime).toISOString();
      return utcTime;
    };
    ```

    - Example for converting to local:

    ```javascript
    const readTimestamp = utcTime => {
      const localTime = new Date(utcTime).toLocaleString();
      return localTime;
    };
    ```

36. Copy to Clipboard

    - Always include a tooltip for any "copy to clipboard" functionality.
    - The tooltip should:
      - Display "Copy" by default.
      - Change to "Copied!" when the user clicks the copy button.
      - Revert back to "Copy" after a few seconds.
    - Use a state variable to manage the tooltip content dynamically.

37. Naming Conventions

    - Consistent naming improves code readability and maintainability. Follow these naming conventions for variables, functions, and components.

    **Variables and Constants**

    - Use camelCase for variables and function names.
      - Example:
      ```javascript
      const userName = 'JohnDoe';
      const isLoggedIn = true;
      ```
    - Use UPPER_SNAKE_CASE for constants.
      - Example:
      ```javascript
      const API_URL = 'https://api.example.com';
      ```

    **Functions**

    - Use camelCase for function names. Start the name with a verb to indicate its action or purpose.
      - Example:
      ```javascript
      const fetchData = async () => {
        /* Logic here */
      };
      const handleClick = () => {
        /* Logic here */
      };
      ```

    **Components**

    - Use PascalCase for React component names. Each word should start with an uppercase letter.
      - Example:
      ```javascript
      const UserProfile = () => {
        return <div>Profile Component</div>;
      };
      export default UserProfile;
      ```

    **Files and Folders**

    - Use PascalCase for component file names to match the component's name.
      - Example:
      ```plaintext
      File name: UserProfile.jsx
      Folder structure:
      src/
      ├── components/
      │   └── UserProfile/
      │       ├── UserProfile.jsx
      │       └── UserProfile.css
      ```
    - Use kebab-case for non-component files or folders (e.g., utility files, assets).
      - Example:
      ```plaintext
      File name: user-profile-utils.js
      ```

    **Event Handlers and Props**

    - Prefix event handlers with "handle" and props with "on" to indicate their purpose.
      - Example:
      ```javascript
      const handleButtonClick = () => {
        /* Logic here */
      };
      <Button onClick={handleButtonClick} />;
      ```

    **Interfaces and Types (if using TypeScript)**

    - Use PascalCase for interfaces and types. Prefix interfaces with "I" or use descriptive names.

      - Example:

      ```typescript
      interface IUser {
        id: number;
        name: string;
      }

      type UserRole = 'admin' | 'user' | 'guest';
      ```

    **Avoid Ambiguity**

    - Avoid using single letters (e.g., x, y) except for loop indices or mathematical contexts.
    - Use descriptive names to indicate purpose and context.
      - Good Example:
      ```javascript
      const fetchUserData = async () => {
        /* Logic */
      };
      ```
      - Bad Example:
      ```javascript
      const fetch = async () => {
        /* Logic */
      };
      ```

---

_Disclaimer: This document is prepared for the frontend React.js team of Invotyx. These conventions might not be relevant for all._
