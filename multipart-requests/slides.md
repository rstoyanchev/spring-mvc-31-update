
!SLIDE subsection bullets smaller
# Agenda

* Code-based Config
* @MVC Support Classes
* Consumes & Produces
* URI Variables
* Redirect Scenarios
* UriComponentsBuilder
* __Multipart Requests__

!SLIDE incremental
# Servlet 3.0 Multipart 
# Request Parsing

* `StandardServletMultipartResolver`
* Use of above resolver is optional
* Required only if using `MultipartFile`
* May use `javax.servlet.http.Part` instead

!SLIDE incremental smaller
# Multipart Request Examples

    @@@ java

	@RequestMapping(method = RequestMethod.POST)
	public void create(
            @RequestParam("file") MultipartFile file){

        InputStream in = file.getInputStream();

        // ...
	}


	@RequestMapping(method = RequestMethod.POST)
	public void create(
            @RequestParam("file") Part part){

        InputStream in = part.getInputStream();

        // ...
	}
    
!SLIDE incremental
# `@RequestPart`

* Like `@RequestBody` but targets the part of a `"multipart/form-data"` request
* The body of the part is read with an `HttpMessageConverter`

!SLIDE smaller
# Request with 
# __JSON__ Part & __Binary File__ Part

    POST /someUrl
    Content-Type: multipart/mixed
     
    --edt7Tfrdusa7r3lNQc79vXuhIIMlatb7PQg7Vp
    Content-Disposition: form-data; name="meta-data"
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

!SLIDE smaller
# Example: `@RequestPart`

    @@@ java


    @RequestMapping(
        method = RequestMethod.POST, 
        consumes = { "multipart/form-data" })

    public ResponseEntity<Object> void create(
            @RequestPart("json-data") @Valid JavaBean javaBean, 
            @RequestPart("file-data") MultipartFile file) {
 
       // ...

    } 

!SLIDE incremental small
# `@Valid`

* Supported on `@RequestBody` and `@RequestPart` args
* ... `MethodArgumentNotValidException` on errors
* Handled by `DefaultHandlerExceptionResolver`
* ... `SC_BAD_REQUEST` (`400`) response  code


