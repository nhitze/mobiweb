# Java Website API #

pakage / namespace: org.mobiweb.web

## org.mobiweb.web.MobileMessage ##

  * ` isHeaderValid() `: Returns true if the parsing of the header was valid
  * ` MobileMessage(HttpServletRequest request) `: Initializes the class by reading from the mobile request.
  * ` prepareHeaders() `: Splits the request into strings that can be used by populateHeaders()
  * ` populateHeaders(String [] value) `: Populates an in class collection of parameters, files and photos from the processed string.
  * ` getParameter(String name) `: Gets a parameter with specified name.
  * ` getFile(String name) `: Gets a file with specified name.
  * ` getPhoto(String name) `: Gets a photo with specified name.

## org.mobiweb.web.data.File ##

File data type used by MobileMessage

## org.mobiweb.web.data.Parameter ##

Parameter data type used by MobileMessage

## org.mobiweb.web.data.Photo ##

Photo data type used by MobileMessage

## org.mobiweb.web.expeptions.InvalidHeaderException ##

Customized exception to track whether we request to get a mobile message file, photo, or parameter with an invalid header