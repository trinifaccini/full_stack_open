``` mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: STEP 1: The browser generates the HTML code for<br/>the existing notes by running the JavaScript code it got<br/>from the server. The code gets the notes from the server<br/>as JSON data and adds HTML elementsto display the notes<br/>on the page using the DOM-API

    Note right of browser: STEP 2: The user clicks on the button form<br/>1: The event handler creates a new object named "note",<br/>which has the content of thenote (the user input) and the timestamp<br/>2:adds the note to the notes list <br/>3: rerenders the note list on the page, doing the same as the previous step<br/>4: sends the new note to the server

    
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    Note left of server: The server creates a new note object containing the user input and <br/> adds it to the array of notes.
    server-->>browser: HTTP 201 Created
    deactivate server

```
