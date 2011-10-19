
!SLIDE subsection bullets smaller
# Agenda

* Code-based Config
* @MVC Support Classes
* Consumes & Produces
* URI Variables
* __Redirect Scenarios__
* UriComponentsBuilder
* Multipart Requests

!SLIDE small
# What will the redirect URL be?

    @@@ java

    @Controller
    @SessionAttributes("foo")
    public class SomeController {

        @ModelAttribute
        public void populate(Model model) {

            // ...
        }

        @RequestMapping("/path")
        public String save(Model model) {

            // ...

            return "redirect:/action";
        }
    }

!SLIDE incremental
# Answer:
## (Up until Spring 3.1)

* Depends on the content of the model
* Simple type attrs appended to query
* May lead to surprises

.notes Example surprises ROO-2158, SPR-6796

!SLIDE smaller
# What Usually Makes Sense ...

    @@@ java

    @RequestMapping("/path")
    public String save(Foo foo, Errors errors, Model model) {

        if (errors.hasErrors()) {
          // Re-render using "default" model
          return "edit";
        }

        // 1. Clear the model content!

        model.asMap().clear()

        // 2. Add attributes for redirect

        return "redirect:/action";
    }

!SLIDE smaller
# Spring 3.1 Redirect Example

    @@@ java

        @RequestMapping("/path")
        public String save(Entity entity, Errors errors, 
                           RedirectAttributes redirectAttrs){

          if (errors.hasErrors()) {
            // Re-render form using "default" model
            return "edit"; 
          }

          // ...

          redirectAttrs.addAttribute("id", 123);
          redirectAttrs.addAttribute("date", new Date());

          return "redirect:/action/{id}";

        }

!SLIDE incremental
# `RedirectAttributes`

* Used __only if__ controller redirects
* Initially empty
* Attributes formatted with DataBinder
* Intended for use in redirect URL
* ... i.e. as URI vars or query params

!SLIDE incremental
# Flash Attributes

* Another kind of redirect attributes
* But without impact on the URL
* Temporily stored in the session
* Removed immediately after the redirect

!SLIDE smaller
# Flash Attributes Example

    @@@ java

      @RequestMapping("/path")
      public String save(Entity entity, Errors errors, 
                         RedirectAttributes redirectAttrs){

        if (errors.hasErrors()) {
          return "edit"; 
        }

        redirectAttrs.addFlashAttribute("message", "Success!");

        // Attribute "message" will appear in model of
        // the controller after the redirect

        return "redirect:/action";
      }

!SLIDE code
# Demo 

<a href="https://github.com/SpringSource/spring-mvc-showcase">https://github.com/SpringSource/spring-mvc-showcase</a>

<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/form/FormController.java">__`FormController.java`__</a>


!SLIDE incremental
# Flash Attributes

* Zero configuration required
* Multi-tiered support
* Use `RedirectAttributes` within @MVC
* Or access `FlashMap` directly elsewhere

!SLIDE small
# Direct Access To FlashMap

    @@@ java

    // Some code not in @Controller
    // Save attributes prior to a redirect..

    FlashMap flashMap = 
      RequestContextUtils.getOutputFlashMap(request);
        
    flashMap.put("message", "Success!");


!SLIDE incremental
# Flash Attributes &
# Concurrency

* A redirect is relatively short lived
* Another async request may come in
* E.g. polling, resource request, etc.
* FlashMap may be consumed too early

!SLIDE incremental
# Solution: Set Request Info
# on FlashMap 

* `setTargetRequestPath(String)`
* `addTargetRequestParam(String,String)`
* Automatically done when using `"redirect:"` or `RedirectView`



