# Adding, Editing, and Deleting Users

Administrative users can add, edit and delete other users at the root of User Management.

## Adding Users

New users can be added in the Product Menu:

1. From the Product Menu, go to _Control Panel → Users → Users and Organizations_.

2. In the Users tab, click the _Add_ button .

![Figure 1: Add Users from the Users and Organizations section of the Control Panel.](./img/1-user-add-edit-delete.png "Users and Organizations section")

3. Click _Save_ after filling the user form to save the newly created user. It is required to provide at least a Screen Name, First Name, Last Name, and Email Address to allow the form to be saved. 

 Note: A screen name can't contain an ```@``` symbol because it's used in the URL to a User’s private page. 
 
 The Add User functionality is split over several independent forms. Saving the first form creates the User, and then you’ll see a success message saying 

	Success. Your request completed successfully.

After the first form is submited, a second form will be displayed. By default, the Information section is selected. On the navigation pane on the left you can check what the current section is, and configure the user being added by going through the different sections. The tabs on top change the options from the menu on the left when clicked on. All the applicable information from the user can be filled by going through the three tabs on top: General, Contact and Preferences.

![Figure 2: Enter at least a screen name, email address, and first name to create a new user account. You'll then be taken to the Information form and can continue configuring the user.](./img/2-user-add-edit-delete.png "Form sections")

After the user account is created, a password is automatically generated. If Liferay is correctly installed and a mail server is correctly set up, an email message with the User’s new password will be sent to the User’s email address.

If a mail server isn't set up, a new password can be manually assigned by clicking on the _Password_ item from the General menu. The new password must be provided twice.

![Figure 3: Enter the password twice to manually set the password for a user. Select whether to require the user to reset their password by the first time they sign in to the portal. The current Password Policy being used must be configured to allow this feature.](./img/3-user-add-edit-delete.png "Set a Password")

## Editing Users

To edit users, click on _Users and Organizations_ in the Control Panel. The list of current registered Users will be shown. To change something about a specific user, click the _Actions_ button (Actions) next to that user. The following options will be shown:

* _Edit_: goes to the Edit User page where any aspect of the User account can be modified, including the screen name, email address, first name, last name, Site, Organization memberships, Roles, etc.

* _Permissions_: can change which Roles have permissions to edit the selected User.

* _Manage Pages_: allows to configure the personal pages of a User.

* _Impersonate User_: opens a new browser window which loads the site as if you were the User, for testing purpouses. This can be used to make sure the desired behavior was achived without having to repeatedly log out of the administrator account and into the User’s account.

* _Deactivate_: deactivates the user’s account. The User will still be in the database, along with all other Users, although the account will be in a deactivated state, which doesn't allow the User to sign in to the portal. To view deactivated users, you can toggle between active and inactive Users in the Users view. If all the Users are active, this filtering option won’t be displayed.

* _Erase Personal Data_: deletes the User’s personal data.

* _Export Personal Data_: allows the the User’s personal data to be exported and downloaded.

![Figure 4: You can choose whether to view active or inactive (deactivated) portal users in the users list found at *Product Menu* → *Control Panel* → *Users* → *Users and Organizations*.](./img/4-user-add-edit-delete.png "Filter")

Most of the actions listed above require administrator privilege to be accessed.

## Deleting Users

User deletion should be taken with care. To avoid accidental deletion of Users, a two-step process must be followed so a user can be deleted: deactivation first, then deletion.

1. Select the User to delete in the Users tab of _Control Panel → Users → Users and Organizations_. In a system with many users, you can save time by searching the user.

2. Click the _Actions_ menu for the User and select _Deactivate_. A confirmation for user deactivation will show up. Click OK to confirm the deactivation. 
After that, a success message will apear, and the User will not be displayed anymore, even though he wasn't deleted yet.

3. By default, the Users table displays Active users only. By Clicking on _Filter and order_ on top of the table, a dropdown menu appears. By clicking on _Inactive_, the inactive users will show.

4. Click on the Actions menu of the user to be deleted, then click Delete. Confirm the User deletion, then the User will be permanently deleted.

**Deactivating a User** disables the User login to the portal. Disabled users also lose privileges in the Sites and pages of the portal, even though the account still exists.

Users can be reactivated by an administrator in the Users table. By making sure that the filter is set to _Inactive users_, click on the Actions menu of the desired user to be reactivated, and select _Activate_. The user is then automatically restored to an Active status without a confirmation window.

For more information on additional topics on User Management, follow the link to the next article.


