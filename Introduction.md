# Introduction #

This project aims to address the problems involved in Mobile to Web communications.

We currently have developed only on J2ME and expect to roll-out to other platforms (Including Android, iPhone). Support is needed from the community to establish this as a standardized communications framework. The following is a description of how the framework operates:

  * You can add a paramater to the request
  * You can add a file to the request
  * You can add a photo to the request

## Sample J2ME code ##

```
    private boolean sendToServer() {
        boolean isSuccessful = false;

        Message message = new Message();

        // Add 2 parameters

        message.addParameter("parameterA", valueATextField.getString());
        message.addParameter("parameterB", valueBTextField.getString());

        // Add a photo and a file

        message.addPhoto("parameterB", photoBytes);
        message.addFile("parameterB", fileBytes);

        try {
            ServerCommunication serverCommunication = new ServerCommunication("http://localhost:8080/MobiWebTest/APITest", true);
            ServerResponse serverResponse = serverCommunication.sendPostMessage(message);
            serverCommunication.closeConnection();

            if(serverResponse.getStatusMessage().equals("error")) {
                isSuccessful = false;
            }
            else {
                returnMessage = serverResponse.getMainMessage().toString();
                isSuccessful = true;
            }

        } catch (ConnectionException ex) {
            ex.printStackTrace();
            return false;
        }
        
        return isSuccessful;
    }
```

## Sample server side code ##

This code is posted in a Servlet (e.g. an App Engine Servlet)

```
    protected void processRequest(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

        MobileMessage mobileMessage = new MobileMessage(request);

        String ParameterA = null;
        String ParameterB = null;
        String PhotoA = null;
        String FileA = null;

        if(mobileMessage.isHeaderValid()) {
            try {
                // Retrieve 2 parameters

                ParameterA = mobileMessage.getParameter("parameterA").getParameterValue();
                ParameterB = mobileMessage.getParameter("parameterB").getParameterValue();

                // Retrieve a file and a photo

                PhotoA = mobileMessage.getPhoto("photoA").getPhotoValue();
                FileA = mobileMessage.getFile("fileA").getFileValue();
            } catch (InvalidHeaderException ex) {
                Logger.getLogger(APITest.class.getName()).log(Level.SEVERE, null, ex);
            }
        }

        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        
        try {
            out.println("Parameter A: " + ParameterA + " & Parameter B: " + ParameterB);
        } finally { 
            out.close();
        }
    } 

    /** 
     * Handles the HTTP <code>GET</code> method.
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        processRequest(request, response);
    } 

    /** 
     * Handles the HTTP <code>POST</code> method.
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        processRequest(request, response);
    }

    /** 
     * Returns a short description of the servlet.
     * @return a String containing servlet description
     */
    @Override
    public String getServletInfo() {
        return "Short description";
    }

```