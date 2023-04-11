```mermaid
  sequenceDiagram
    participant browser
    participant server
    
    Note right of browser: The user fills in a form and clicks 'submit'
    Note right of browser: The browser then sends a POST request containing the note as a body and POST as a header.

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/notes
    activate server

    Note left of server: Server adds the new note to the JSON file containing all notes.

    server-->>browser: HTTP 302 Status Code: FOUND. Redirect back to notes page.
    deactivate server

    Note right of browser: Browser sends another get request for the /notes.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server

    Note left of server: Server sends back the HTML for /notes.

    server-->>browser: notes.html
    deactivate server

    Note right of browser: Browser parses the HTML and sends multiple GET requests for the CSS and JS files referenced in the HTML file.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: main.js
    deactivate server
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/styles.css
    activate server
    server-->>browser: styles.css
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server

    Note left of server: Server returns updated JSON file.

    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```