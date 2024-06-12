sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: the CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    Note right of server: status code: 304 Not Modified
    activate server
    server-->>browser: [{content: "y9", date: "2024-06-12T12:57:50.507Z"},…]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
