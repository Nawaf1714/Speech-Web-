# Speech-Web-

The code enables speech recognition by converting it to text, then transferring the text to the `controller.php` file using a POST request, the new result in an HTML element.

## HTML

Main content:
- The page contains a form (`<form>`) containing a `textarea` element with the `output` parameter to display the text converted from the voice and is read-only.

- A button (`<button>`) with the `converter` parameter to start the voice-to-text conversion process when clicked.

- An external JavaScript file (`speech-to-text.js`) is included to implement the speech recognition functions.

## Javascript

Speech Recognition Initialization:
- The `webkitSpeechRecognition` object is initialized to enable speech recognition, with the language set to English.

Start on Click:
- When the button with the identifier `converter` is clicked, the speech recognition process is started by `recognition.start()`.

Result Processing:
- When speech recognition is successful, the text is extracted from the first result (`event.results[0][0].transcript`) and sent to the `sendRequest` function.

Error Handling:
- If an error occurs during speech recognition, the error is logged in the console (`console.error`).

Sending the text to the server:
- The `sendRequest` function sends the text to the `controller.php` file using a POST request. The content type is set to `application/x-www-form-urlencoded` and the text is sent as part of the data (`body`).
- When the response is received from the server, the received data is displayed in an HTML element containing the identifier `output`.

## PHP
Database Connection:
- Database connection parameters such as `servername`, `username`, `password`, and database name `DBname` are set.
- Connection is established using `mysqli_connect`. If connection fails, the program is stopped and an error message is displayed.

Received data processing:
- Text is received from POST request (`$_POST['text']`) and sanitized with `mysqli_real_escape_string` to avoid SQL Injection attacks.
- Extra white spaces are removed with `trim`.

Data insertion into database:
- SQL statement is configured to insert text into `conSpeech` table in `speech` column.
- If insert succeeds, the received text is returned. If it fails, an error message is displayed.
