sequenceDiagram
participant browser
participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: the CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: [{content: "Damn that's a lot of notes", date: "2024-06-12T12:24:33.529Z"},…]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    Note right of server: status code: 302 Found
    activate server
    server-->>browser: The server asks the browser to perform a new HTTP GET request to the address defined in the header's Location - the address notes.
    deactivate server

    Note right of browser: The browser reloads the Notes page, fetching the style sheet (main.css), the JavaScript code (main.js), all with 304 status code (in the same way it did before), and finally the raw data of the notes (data.json).

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: [{content: "first exercise", date: "2024-06-12T19:52:43.293Z"},…]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes. Now the new note created by the user is rendered on the notes page.
