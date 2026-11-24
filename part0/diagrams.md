# Part 0 diagrams

Diagrams written from my reading of the Part 0 course text about the example notes app.

## 0.4: New note in traditional notes page

```mermaid
sequenceDiagram
participant browser
participant server

Note over browser: User types text into the form and clicks Save
browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
activate server
Note over server: Server creates a note object from the form data and pushes it to the notes array
server-->>browser: HTTP 302 redirect to /exampleapp/notes
deactivate server

Note over browser: Browser reloads the notes page because of the redirect

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
activate server
server-->>browser: HTML document
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
activate server
server-->>browser: CSS file
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
activate server
server-->>browser: JavaScript file
deactivate server

Note over browser: Browser runs main.js which requests the JSON data

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
activate server
server-->>browser: JSON list of notes including the new one
deactivate server

Note over browser: Event handler renders all notes to the page
```

## 0.5: Single page app

```mermaid
sequenceDiagram
participant browser
participant server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
activate server
server-->>browser: HTML document
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
activate server
server-->>browser: CSS file
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
activate server
server-->>browser: JavaScript file
deactivate server

Note over browser: Browser runs spa.js which requests the JSON data

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
activate server
server-->>browser: JSON list of notes
deactivate server

Note over browser: Event handler renders the notes to the page using DOM API
```

## 0.6: New note in single page app

```mermaid
sequenceDiagram
participant browser
participant server

Note over browser: User types text and clicks Save
Note over browser: JavaScript adds the new note to its local notes list and redraws the notes on the page without reloading

browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
activate server
Note over server: Request body is JSON with content and date
server-->>browser: HTTP 201 Created with a JSON message
deactivate server

Note over browser: Page stays as is, no further requests are needed
```
