# J2ME API #

package / namespace: org.mobiweb.mobile

## org.mobiweb.mobile.Message ##

Composes a Message to be sent as a request.

  * ` addFile(String name, byte [] fileData) `: Adds a file's content to the mobile request message.
  * ` addParameter(String name, String param) `: Adds a parameter to the mobile request message.
  * ` addPhoto(String name, byte [] photoData) `: Adds a photo's content to the mobile request message.
  * ` getMessageContent() `: Retrieves the request content generated after all operations are done.

## org.mobiweb.mobile.ServerCommunication ##

Handles communications to the HTTP server

  * ` ServerCommunication(String url, boolean openConnection) `: Constructor, initializes the URL and either opens or does not open connection
  * ` closeConnection() `: Closes the connection (if open).
  * ` getServerUrl() `: Returns the set URL.
  * ` makeResponseError(ServerResponse serverResponse) `: Sets the flags to indicate there was an error in the response from the server.
  * ` openConnection() `: Opens the HTTP connection if not open.
  * ` sendPostMessage(Message message) `: Sends a message constructed from the Message class to the server.
  * ` setServerUrl(String serverUrl) `: Sets the URL for the server request.

## org.mobiweb.mobile.ServerCommunicationThread ##

Automatically initiates a thread to do server communication in the background

  * ` ServerCommunicationThread(Message message, String url) `: Constructor, contains the Message and URL for the communication.

## org.mobiweb.mobile.exceptions.ConnectionException ##

Customized exception to track errors in the connection.

## org.mobiweb.mobile.util.Common ##

Common functions (static / non static)

## org.mobiweb.mobile.util.FileBrowser ##

Basic file browsing / file system functionality to help track down and work with file systems.

  * ` getAttributes(String filePath) `: Retrieves the attributes of the file selected (either file, folder, or non-existent file).
  * ` getCurrDir(String currDirName) `: Retrieves a Vector collection of files in the currDirName folder

## org.mobiweb.mobile.util.ServerCommunicationStatus ##

Is used by the ServerCommunicationThread to synchronize info about the status of the response from the server.

## org.mobiweb.mobile.util.ServerResponse ##

Tracks down the response from the server.

  * ResponseMessage: Response from the server.
  * StatusMessage: Server HTTP status.
  * MainMessage: Message body sent from the server.

  * ` ServerResponse(String responseMessage) `: Custom constructor, initializes the response message.