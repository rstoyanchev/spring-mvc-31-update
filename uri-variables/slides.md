
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

!SLIDE incremental bullets
# Path Variables In Views

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

* Redirect string treated as URI template
* Expanded with model values
* Also with current request URI vars
* Expanded variables are encoded

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
        // They will be available to the view

        return "redirect:/{year}/{month}/{slug}";
    }

!SLIDE incremental bullets
# Model Attributes &
# URI Vars

* A URI variable can be used to instantiate a `@ModelAttribute` argument
* If the names match and there is a registered `Converter<String, Account>`

!SLIDE small
# Example

    @@@ java


    @RequestMapping(value="/{account}", 
                    method = RequestMethod.PUT)

    public String update(
               @ModelAttribute Account account) {

    }

!SLIDE
# Demo
<br><br>
<a href="https://github.com/rstoyanchev/spring-mvc-31-demo">https://github.com/rstoyanchev/spring-mvc-31-demo</a>
<br><br>
_CRUD Controller:_
<a href="https://github.com/rstoyanchev/spring-mvc-31-demo/tree/master/src/main/java/org/springframework/samples/mvc31/crudcontroller">`org.springframework.samples.mvc31.crudcontroller`</a>


