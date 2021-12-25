### Connect Python and Microsoft Graph / Office 365
#### Problem
You want to write Python custom-built applications to work with Office 365, such as Email, Teams, OneDrive, etc. 

#### Dependencies

* Python 3.8.6
* Python `requests` package
  * `pip install requests`
* `O365` package 
  * `pip install O365`
* Office 365 Business Account (business account used here, should work with personal)

#### References

* 

#### Theory

For this to work, the python application must authenticate itself with Office 365 using Azure Active Directory. 

#### Setup on portal.azure.com

We will first set up an application on Azure by going to portal.azure.com, logging in with our office 365 credentials, and adding a new application (lets call it "o365py-test"):

* Sign in to portal.azure.com
  * Sign in with your business o365 account
* Register a new application
  * Go to (search if you don't see it) *App Registrations* to add a *New registration*
  * Enter "o365py-test" in *Name*, and in *Supported account types* select the "Accounts in this organizational directory only (single tenant)" radio button for now
  * In *Overview*, you should now see values for *Application (client) ID*, *Directory (tenant) ID*
* Authentication setting, and adding a redirect URI 
  * Click on "Add a Redirect URI", then *+Add a platform*
    * Select the *Mobile and Desktop Applications* panel (our app will interact through API calls from a terminal)
    * Activate: https://login.microsoftonline.com/common/oauth2/nativeclient (a check box option for this may already be available)
    * In Supported account types, check the Radio button: *Accounts in this organizational directory only (Single tenant)*
    * Turn the toggle on *Allow public client flows* to **Yes**
* Create a Client Secret
  * One the left pane, go to *Certificates & secrets*
  * Click on *+ New client secret*. Give is any description, and set expiry to "Never"
    * Copy the value and store it, it will be hidden after this moment (for ever)
      * A good place to store it is in a "config.py" file in your local Python application folder
* Add API permissions
  * One the left pane, go to *API permissions*
    * Permission "User.read" is set by default