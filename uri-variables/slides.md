
!SLIDE subsection bullets smaller
# Agenda

* Code-based Config
* @MVC Support Classes
* Consumes & Produces
* __URI Variables__
* Redirect Scenarios
* UriComponentsBuilder
* Multipart Requests

!SLIDE small
# URI Variables In
# Data Binding

    @@@ java


	@RequestMapping(
        value="/people/{firstName}/{lastName}/SSN")

	public void search(Person person) {

	    // person.getFirstName() is populated
        // person.getLastName()  is populated

	}

!SLIDE small
# URI Variable 
# To Instantiate Model Attribute

    @@@ java

      // 1. URI variable name = model attr name
      // 2. Registered Converter<String, Account>

	  @RequestMapping(value="/{account}", 
                      method = RequestMethod.PUT)

	  public String update(Account account) {

        // ...

      }

!SLIDE code
# Demo 

https://github.com/rstoyanchev/spring-mvc-31-demo

`org.springframework.samples.mvc31.crudcontroller`


!SLIDE incremental
# Path Variables
# In Rendering

* Path variables merged in the model
* Prior to rendering
* Individal `View` types can opt out
  * `MappingJacksonJsonView`
  * `MarshallingView`


!SLIDE small
# Example

    @@@java


    @RequestMapping("/develop/apps/edit/{slug}")

    public String editForm(@PathVariable String slug){

        // No need to add "slug" to the model
        // Will be available for rendering

    }

!SLIDE smaller
# URI Variables 
# In Redirect Strings 

    @@@java

        @RequestMapping(
            value="/{group}/{year}/{month}/{slug}/rooms",
            method=RequestMethod.POST)

        public String createRoom() {

            // No need to add "group"/"year"/.. to the model
            // Will be available for the redirect string

            return "redirect:/{group}/{year}/{month}/{slug}";
        }


