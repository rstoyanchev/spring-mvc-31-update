
!SLIDE subsection
# URI Variables

!SLIDE small
# Data Binding & URI Variables

    @@@ java


	@RequestMapping(
        value="/people/{firstName}/{lastName}/SSN")

	public void search(Person person) {

	    // person.getFirstName() is populated
        // person.getLastName()  is populated

	}

!SLIDE incremental bullets small
# Rendering & Path Variables

* `@PathVariable` values
* merged into the model before rendering
* Individal `View` types _"opt out"_
* E.g. `MappingJacksonJsonView`, `MarshallingView`

!SLIDE small
# Example

    @@@java


    @RequestMapping("/apps/edit/{slug}")
    public String editForm(@PathVariable String slug){



    }

!SLIDE small transition=fade
# Example

    @@@java


    @RequestMapping("/apps/edit/{slug}")
    public String editForm(@PathVariable String slug){

        // No need to add "slug" to the model

    }

!SLIDE incremental bullets
# `"redirect:"` & URI Vars

* URI template redirect string
* Expanded from model values & current request URI vars
* Variables are encoded

!SLIDE small
# Example

    @@@java

    @RequestMapping(
        value="/{year}/{month}/{slug}/rooms",
        method=RequestMethod.POST)

    public String createRoom() {




        return "redirect:/{year}/{month}/{slug}";
    }

!SLIDE small
# Example

    @@@java

    @RequestMapping(
        value="/{year}/{month}/{slug}/rooms",
        method=RequestMethod.POST)

    public String createRoom() {

        // No need to add "year", "month", & "slug"


        return "redirect:/{year}/{month}/{slug}";
    }

!SLIDE small
# Example

    @@@java

    @RequestMapping(
        value="/{year}/{month}/{slug}/rooms",
        method=RequestMethod.POST)

    public String createRoom() {

        // No need to add "year", "month", & "slug"
        // They will be used in RedirectView

        return "redirect:/{year}/{month}/{slug}";
    }

!SLIDE incremental bullets small
# Model Attributes & URI Vars

* A URI variable (or request param) can be used to instantiate a `@ModelAttribute` argument
* If the model attribute name matches the URI variable (or request param) name
* And there is a registered `Converter<String, Account>`

!SLIDE
# Example

    @@@ java


    @RequestMapping(
            value="/{account}", 
            method = RequestMethod.PUT)

    public String update(Account account) {




    }

!SLIDE transition=fade
# Example

    @@@ java


    @RequestMapping(
            value="/{account}", 
            method = RequestMethod.PUT)

    public String update(Account account) {

        // Account was retrieved from DB 
        // via Converter<String, Account>

    }

!SLIDE
# Demo
<br><br>
<a href="https://github.com/rstoyanchev/spring-mvc-31-demo">https://github.com/rstoyanchev/spring-mvc-31-demo</a>
<br><br>
_CRUD Controller:_
<a href="https://github.com/rstoyanchev/spring-mvc-31-demo/tree/master/src/main/java/org/springframework/samples/mvc31/crudcontroller">`org.springframework.samples.mvc31.crudcontroller`</a>


