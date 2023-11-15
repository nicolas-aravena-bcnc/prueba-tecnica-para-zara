The new HU We need to develop this HU on this sprint: "_Modify the login process so that in addition to username and password, it is mandatory to accept a privacy policy check before clicking the submit button._"

According to the attached previous info, we need to:

Definition of the acceptance criteria of the HU defined a few lines above.
As a user, I won't be able to proceed without accepting the privacy policy. After accepting the security policies, I can complete the login normally.

### Writing the BDD Gherkin test cases to validate the HU

```gherkin
Scenario: User accepts the privacy policy check
  Given the user is on the login page
  When the user enters the username and password
  And the user accepts the privacy policy check
  Then the user clicks the submit button
  And the login is successfully completed
  
Scenario: User does not accept the privacy policy check
  Given the user is on the login page
  When the user enters the username and password
  And the user does not accept the privacy policy check
  Then the user clicks the submit button
  And the system displays an error message indicating that the check is mandatory
  
Note: Below, I am adding some cases that, according to the criteria I have used, 
should already be in the system as they are not exclusively related to the new HU.

Scenario Outline: User provides invalid input after accepting the privacy policy
 Given the user is on the login page
 And the user accepts the privacy policy check
 When the user enters "<invalid_username>" and "<invalid_password>"
 Then the user clicks the submit button
 And an error message is displayed

 Examples:
   | invalid_username | invalid_password |
   | invalidUser      | invalid          |
   | UserInvalid   | a                |
  

Scenario Outline: User provides empty username or password
 Given the user is on the login page
 When the user enters "<empty_username>" and "<empty_password>"
 And the user accepts the privacy policy check
 Then the user clicks the submit button
 And an error message is displayed

 Examples:
   | empty_username | empty_password |
   |               | validPassword  |
   | validUser     |               |
   |               |               |

```

### Taking into account that this HU has implementation of both Web, iOS,Android and backend, comment on what tools you would use to validate this HU in each discipline in a manual way.

* To do it manually, for the Web, I would use Chrome's Browser Developer Tools as they seem the most comprehensive and easy to use. This way, I could access the test environment and check the page elements, both new and existing.

* For iOS or Android, I would need multiple mobile devices to manually check the application from different OS versions, ensuring that all new elements in the login are visible and clickable.

* For the backend, I would use Postman to make an API call to the login API and check that it does not allow me to proceed if I don't fill in all the mandatory fields. Additionally, I would verify that the received data matches the expected data, such as an access token or other measures to enter the application.

### As a QA engineer within a Scrum team, share with us what ceremonies and meetings you think will exist during the week of the sprint.
* Sprint Planning: Planning tasks for the sprint.
* Daily Standup: Daily meeting to share updates and obstacles.
* Sprint Review: Reviewing what was completed during the sprint.
* Sprint Retrospective: Evaluation and continuous improvement at the end of the sprint.
* Backlog Refinement (Grooming): Preparing and detailing future tasks to be ready for the next Sprint Planning.

### As a final step, we would like to incorporate validation of this new use case into our automatic regression plan.

#### a. Which tools would you use to automate the Web, iOS, Android, and backend platform?

Web: Selenium using Java, Python, etc.
iOS Automation: XCTest for Swift using XCode.
Android Automation: Espresso for Android using Android Studio.
Backend/API Automation: Karate DSL, Newman.

#### b. Which CI/CD tools do you think could be used to schedule the regression launch in a planned and manual way?

* Jenkins: is a widely used open-source tool that makes it easy to create pipelines, as well as manually trigger test builds, for example.
* GitHub Actions: It is a tool that, in addition to having capabilities to create pipelines and automate processes, can launch specific builds. What makes it interesting is its tight integration with GitHub and, in turn, with Git. This facilitates collaboration among developers.

### Imagine that our PO tells us on Thursday morning that we have to put a new HU in this sprint that closes Friday at noon, and you still lack 1 development of this HU to receive from the developers and try it. Could you share any alternative to try to achieve the PO's goal?

If I still haven't received the task from the developer and there are no critical bugs or tasks that need higher priority review, we could review the task proposed by the PO and see if it's sufficiently scoped to be completed before the end of the sprint.
