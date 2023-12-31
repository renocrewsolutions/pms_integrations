# pms_integrations
PMS integrations service
# hotelpms.py
The code is a Python module that defines a class PMS and its subclasses PMS_Clock, PMS_Stayntouch, and PMS_Guestline. This module is a part of a larger application built using the Django web framework.

The PMS class and its subclasses define methods for interacting with different Property Management Systems (PMS) used in the hotel industry. The code includes methods for handling webhooks, retrieving and updating reservation information, validating data, and performing various PMS-specific operations such as checking for breakfast reservations.

# Some of the notable methods in the PMS class and its subclasses are:

## validate_webhook: Validates the data received in a webhook call from the PMS.
## push_task: Handles a guest's request to contact the hotel.
## get_products: Retrieves the products offered by the hotel.
## push_dialogue: Handles a new dialogue from a guest.
## can_check_for_breakfast: Determines whether the PMS supports checking if a guest has breakfast reserved.
## has_breakfast: Checks if a stay includes breakfast.
## can_book_breakfast: Determines whether the PMS supports booking breakfast for a stay.
## book_breakfast: Books breakfast for a stay.
## store_guest_with_stay: Stores guest information along with a stay in the database.
## touch: A method called periodically (every 15 minutes) to retrieve new and changed reservations.

These classes provide a way to interface with different PMS systems within the application and perform PMS-specific operations.

### The PMS class serves as a base class and contains various methods and properties related to PMS functionality. It defines common methods that can be overridden by its subclasses to provide specific implementations based on different PMS systems.

### The PMS_Clock class is a subclass that provides specific functionality for integrating with the Clock PMS system. It includes methods such as has_breakfast, validate_webhook, and handle_webhook that handle specific tasks related to the Clock PMS system.

### The PMS_Stayntouch class is another subclass that provides functionality for integrating with the Stayntouch PMS system. Similarly, it defines methods for handling webhooks and other PMS-related tasks.

### The PMS_Guestline class is a subclass specific to the Guestline PMS system. It includes methods such as _call_guestline, _callLogin, and _callBookingSearch that interact with the Guestline PMS API.

Overall, these classes provide a framework for integrating with different PMS systems by defining common methods and allowing specific implementations for each PMS system.


# urls.py
The code  is a snippet from a Django urls.py file, which is used to define the URL patterns for your Django web application.

In this snippet, the path() function from the django.urls module is imported, along with the views module from the current package.

The urlpatterns list is a list of URL patterns for your application. Each URL pattern is defined using the path() function. In your example, there is one URL pattern defined:

## python code

```console
path('webhook/<str:pms_name>/<str:pms_path_info>/', views.webhook, name="webhook"),
```
## This pattern maps the URL webhook/<str:pms_name>/<str:pms_path_info>/ to the views.webhook function. The <str:pms_name> and <str:pms_path_info> are dynamic segments of the URL, which can match any string value. The values captured by these segments will be passed as arguments to the webhook function.

The name="webhook" parameter is optional but is often used to provide a name for the URL pattern. This name can be used in other parts of  code to reference this specific URL pattern, such as when generating URLs using the reverse() function.

Overall, this code defines a URL pattern that matches requests to the webhook/<str:pms_name>/<str:pms_path_info>/ URL and routes them to the views.webhook function.

# views.py

The code imports various modules and defines two functions: process_webhook() and webhook().

## process_webhook(pms_name, cleaned_data, pms_path_info): 
This function takes three parameters: pms_name, cleaned_data, and pms_path_info. It calls the get_pms() function from the hotelpms module to retrieve a specific PMS (Property Management System) based on the pms_name. Then, it calls the handle_webhook() method of the retrieved PMS object, passing cleaned_data and pms_path_info as arguments. Finally, it returns the result of the handle_webhook() method.

## @csrf_exempt decorator: 
This decorator is applied to the webhook() function. It exempts the function from Cross-Site Request Forgery (CSRF) protection. CSRF protection is a security measure in Django to prevent unauthorized POST requests. In this case, the decorator allows the webhook() function to process POST requests without CSRF validation.

## webhook(request, pms_name, pms_path_info): 
This function is the view function that handles the webhook requests. It takes three parameters: request, pms_name, and pms_path_info. The request parameter represents the HTTP request object sent to the view.

It first checks if the request method is not POST. If it's not a POST request, it raises an Http404 exception with the message "Request method must be POST."

It then calls the get_pms() function from the `hotelpms` module to retrieve a specific PMS object based on the pms_name. If the PMS object does not exist (returns None), it raises an Http404 exception with the message "Not a valid PMS name."

Next, it uses json.loads(request.body) to parse the request body (assumed to be in JSON format) and passes it to the validate_webhook() method of the PMS object along with pms_path_info. The validate_webhook() method is responsible for validating the webhook data. If the cleaned_data returned from validate_webhook() is None, it raises an Http404 exception with the message "Content invalid."

If the cleaned_data is valid, it calls the process_webhook() function, passing the pms_name, cleaned_data, and pms_path_info as arguments. This function will further process the webhook data.

Finally, it returns an HTTP response with the content "Thanks for the update." This response indicates that the webhook request was successfully processed.

Overall, this code defines a view function webhook() that handles POST requests to a specific URL pattern. It performs various checks and validations before processing the webhook data using the process_webhook() function.



You can learn more about integration in the [StayNTouch documentation](https://www.stayntouch.com/developers).
Visit Us [Runnr.ai](https://www.runnr.ai/).
#   p m s _ i n t e g r a t i o n s  
 #   p m s _ i n t e g r a t i o n s  
 #   p m s _ i n t e g r a t i o n s  
 