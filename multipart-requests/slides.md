
!SLIDE subsection
# Multipart Requests

!SLIDE incremental bullets
# Servlet 3.0 Support

* `StandardServletMultipartResolver`
* Use of resolver is optional
* Required only with use of `MultipartFile`
* Not for `javax.servlet.http.Part` args

!SLIDE incremental smaller
# `MultipartFile` Example

    @@@ java

	@RequestMapping(method = RequestMethod.POST)
	public void create(
            @RequestParam("file") MultipartFile file){

        InputStream in = file.getInputStream();

        // ...

	}

!SLIDE incremental smaller transition=scrollLeft
# `javax.servlet.http.Part` Example

    @@@ java

	@RequestMapping(method = RequestMethod.POST)
	public void create(
            @RequestParam("file") Part part){

        InputStream in = part.getInputStream();

        // ...

	}
    
!SLIDE incremental bullets
# `@RequestPart`

* Like `@RequestBody` but for the part of a `"multipart/form-data"` request
* Request part content processed with `HttpMessageConverter`

!SLIDE smaller
# Example

    @@@ java


    @RequestMapping(
        method = RequestMethod.POST, 
        consumes = { "multipart/form-data" })

    public ResponseEntity<Object> void create(
            @RequestPart("json-data") @Valid JavaBean javaBean, 
            @RequestPart("file-data") MultipartFile file) {
 
       // ...

    } 

!SLIDE smaller
# Multipart Request with JSON

    POST /someUrl
    Content-Type: multipart/mixed
     
    --edt7Tfrdusa7r3lNQc79vXuhIIMlatb7PQg7Vp
    Content-Disposition: json-data; name="meta-data"
    Content-Type: application/json; charset=UTF-8
    Content-Transfer-Encoding: 8bit
     
    {
      "name": "value"
    }
    --edt7Tfrdusa7r3lNQc79vXuhIIMlatb7PQg7Vp
    Content-Disposition: form-data; name="file"; filename="file.properties"
    Content-Type: text/xml
    Content-Transfer-Encoding: 8bit
    ... File Data ...

!SLIDE incremental bullets small
# `@Valid`

* Supported on `@RequestBody` & `@RequestPart` args
* Produces `MethodArgumentNotValidException`
* Handled in `DefaultHandlerExceptionResolver`.. `SC_BAD_REQUEST` (`400`) response  code


