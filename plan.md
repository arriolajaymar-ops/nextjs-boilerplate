```markdown
# Detailed Implementation Plan for Location Tracking Website

## Overview
We will build a Next.js website that allows users to enter their Instagram and Facebook profile links and then "tracks" (simulates) location data based on those links. The application will feature a modern, minimalist UI using Tailwind CSS and will include robust error handling and best practices for both client- and server-side code.

## Step-by-Step Implementation

### 1. Create the Main Homepage (src/app/page.tsx)
- **Purpose:**  
  Present a clean, modern form for users to input their Instagram and Facebook profile URLs and display the simulated location data returned by the API.
- **Implementation Details:**  
  - Create a new file `src/app/page.tsx`.  
  - Import React hooks (`useState`) to manage form inputs, loading status, results, and errors.  
  - Build a form with two text input fields:
    - One for the Instagram profile URL.
    - One for the Facebook profile URL.
  - Add a submit button labeled "Track Location" styled with Tailwind CSS (use utilities for padding, margin, font, and colors).
  - On form submission, validate the inputs with a simple regex to verify proper URL format.
  - Call the `/api/track` endpoint using the `fetch` API and handle:
    - Loading state feedback.
    - Successful retrieval of location data (e.g., displaying "Instagram Location: New York, USA" and "Facebook Location: San Francisco, USA" along with coordinates).
    - Displaying error messages if the API returns an error or if the inputs are invalid.
  - Ensure the UI layout is responsive with proper spacing, and accessible (proper labels and semantic HTML).

### 2. Create the API Route for Location Tracking (src/app/api/track/route.ts)
- **Purpose:**  
  Handle POST requests by receiving Instagram and Facebook URLs, validate them, and return simulated location data.
- **Implementation Details:**  
  - Create a folder `src/app/api/track/` and within it, a file named `route.ts`.
  - Export an async request handler that:
    - Checks if the HTTP method is POST; otherwise, returns a 405 Method Not Allowed error.
    - Parses the incoming JSON payload and validates that both `instagramUrl` and `facebookUrl` are provided.
    - Simulates location extraction:
      - For Instagram, return location "New York, USA" with coordinates `{ lat: 40.7128, lng: -74.0060 }`.
      - For Facebook, return location "San Francisco, USA" with coordinates `{ lat: 37.7749, lng: -122.4194 }`.
    - Wrap the processing logic within a try-catch block to capture any runtime errors and return a proper error message in JSON (with a 400 or 500 HTTP status as appropriate).

### 3. UI/UX and Styling Considerations
- **Modern, Clean Design:**  
  - Use Tailwind CSS classes to create a user interface that emphasizes readability, ample whitespace, and modular components.  
  - Style the input fields with clear focus states, borders, and error highlights.
  - Maintain a consistent typography and layout (e.g., use classes such as `text-lg`, `p-4`, `mb-4`, and `bg-gray-50`).
- **Accessibility:**  
  - Ensure each input has associated `<label>` elements.  
  - Include descriptive error messages and fallback content without using external icons or images.
  
### 4. Error Handling and Best Practices
- **Client-side:**  
  - Validate URLs using regex before form submission.  
  - Display concise, user-friendly error messages if validation fails or if the network request returns an error.
- **Server-side:**  
  - Enforce POST-only requests by returning a 405 status for incorrect methods.  
  - Validate JSON payload rigorously and return informative error messages, using HTTP statuses like 400 for bad requests.
  - Use try-catch blocks to gracefully manage unexpected errors and respond with clear error details.
  
### 5. Testing and API Verification
- **API Testing via curl:**  
  Use the following curl command to ensure your API endpoint works as expected:
  ```bash
  curl -X POST http://localhost:8000/api/track \
       -H "Content-Type: application/json" \
       -d '{"instagramUrl": "https://instagram.com/example", "facebookUrl": "https://facebook.com/example"}'
  ```
- **Manual UI Testing:**  
  - Run the Next.js application, navigate to the homepage, and test the form inputs with valid and invalid URLs.
  - Verify that the page correctly displays simulated location data and shows errors when necessary.

## File Dependencies
- **src/app/page.tsx:**  
  New file for the main user interface containing the input form and results display.
- **src/app/api/track/route.ts:**  
  New file defining the API route to process tracking requests.
- **src/app/globals.css:**  
  Global styles (modify only if additional custom styles are needed for layout consistency).
- **package.json:**  
  Ensure dependencies such as Next.js, React, and Tailwind CSS are installed and configured.

## Summary
- A modern UI is built on `src/app/page.tsx` featuring a form for Instagram and Facebook URLs.
- The API route at `src/app/api/track/route.ts` handles POST requests, validates the payload, and returns dummy location data.
- The system implements robust error handling on both client and server sides.
- Tailwind CSS provides the visual design with proper spacing, typography, and responsive design.
- API functionality is tested using curl commands and manual validation in the browser.
- Code follows best practices for input validation and error management, ensuring a secure, user-friendly experience.
