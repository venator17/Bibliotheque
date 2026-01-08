# Access Control

## ABOUT

Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management:

* **Authentication** confirms that the user is who they say they are.
* **Session management** identifies which subsequent HTTP requests are being made by that same user.
* **Access control** determines whether the user is allowed to carry out the action that they are attempting to perform.

Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:

* A hidden field.
* A cookie.
* A preset query string parameter.
