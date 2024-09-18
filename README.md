# ReadMe

## Content
 * [Basics](#basics)
 * [Disclaimer and Warning](#disclaimer-and-warning)
 * [Release Notes](#release-notes)
 * [Ussage](*Ussage)

## Basics
Install the powershell module to download the folder and copy this files to your powershell module folder

# Import module
```
import-module -name "Microsoft_Graph_wrapper"
```

## Disclaimer and Warning
**Be careful!** THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


## Release notes
### Version 3.4.0
* Added get-groupmembers
* Added get-groupinfo
* added add-usertogroup
* Added more parameters in the add-Azureuser
* Bug fixes
### Version 3.2.0
* added add-azureuser
* fix unapproved verbs
* Change decode-lapspassword to Unlock-lapspassword
### Version 3.0.0
* added get-lapspassword<br>
* added Decode-lapspassword
### Version 2.0.0
* Added get-allmanageddevices<br>
* added Get-Lastloggedonuserandinfo<br>
* added get-graphmoduleversion
### Version 1.0.0
* Create Token for Azure Graph with the command get-tokengraph<br>
* Send mail with the Graph API.


## Ussage
## Create Token
Create a token
```
$accesstoken = get-tokengraph -clientid <Your ClientID> -clientsecret <Your Client Secret> -tenantid <Your TenantID>
```
## Send mail
Send an e-mail with Microsoft graph, you must have the userID of the user wich will send the mail.
```
send-emailgraph -token $accesstoken -fromuserid <ID of sending user> -Subject <Subject> -Content <HTML Content for body mail> -toadres <Sending e-mail to>
```

## Get all managed devices
Get all managed devices in intune
```
$devices = get-allmanageddevices -token $accesstoken
```

## Get last logged on user and more info
Get last logged on info based on all Intune devices, you get the following info: Date, DeviceID, UserID, Devicename, Operatingsystem, User Displayname, Emailaddress, Lastloggedon 
```
Get-Lastloggedonuserandinfo -alldevices $devices -exportcsv yes/no -csvpath C:\temp\devices.csv
```
## Get group info
Get info for groups based on name, you will get the following info: ID, Displayname and Mailnickname
```
Get-groupinfo -token $accesstoken -groupname <Groupname>
```
## Get all group members
Get all members of a group, You can use the Name or ID, export to csv is optional.
You will get the following information: displayName, givenName, surname, mail, userPrincipalName, jobTitle, id
```
Get-groupinfo -token $accesstoken -groupname <Groupname>
```
```
Get-groupinfo -token $accesstoken -groupname <Groupname> -exportcsv yes -csvpath $servicedeskengineercsv
```
```
Get-groupinfo -token $accesstoken -Groupid <GrouID> -exportcsv yes -csvpath $servicedeskengineercsv
```
## get Lapspassword
Get the laps password encrypted.
```
$password = get-lapspassword -token $accesstoken -Devicename <Devicename>
```
## Unlock Lapspassword
Unlock the laps password so you can Use it.
```
unlock-lapspassword -password $password.passwordBase64
```
## Add Azure AD User
Add a User in AzureAD, City, Country, Department, and preferredLanguage is automatic filled, and you cannot personalize it.
```
add-AzureUser -token $accesstoken -Firstname <Example> -lastname <User> -diplayname <Displayname> -jobtittle <Jobtittle> -mailnickname <e.user> -domain <Contoso.com> -userpass <thisismypassword>
```
## Add User to a group
Add a user to a group in Azure.
```
add-usertogroup -token $accesstoken -userid <Id of user> -groupid <Id of the group you want to add.>
```
## Get Moduleversion 
```
get-graphmoduleversion
```


