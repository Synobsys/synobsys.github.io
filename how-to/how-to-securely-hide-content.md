---
title: How to securely hide content in reactive web applications
---
# {{page.title}}

This how-to guide describes follows the  [Reactive web security best practices](https://success.outsystems.com/Documentation/Best_Practices/Security/Reactive_web_security_best_practices) and shows you how-to securely hide content from unauthorized users in the following situations:

* displaying sensitive data
* editing sensitive data
* redirecting users to a role based page

* TOC
{:toc}

## Showing sensitive data to authorized users only

### Fetch data from the database

When you fetch data from the database add a filter to the aggregate to check if the user has the required role e.g. `CheckEmployeeManagerRole()`

### Fetch data from other sources

Inside the Data Action start with a CheckRole and exit the action with empty output if the user does not have the role.

### Hiding elements using an _If_ widget

Using the same approach as for the hidden class set the condition of the if to `<UserHasSomeRole>()`
Be aware of side effects when you put some widgets inside an If widget e.g. hiding a TabsContentItem with an if will break the styling of the tabs.

## Editing sensitive data

Scenarios:

1. You have a page to edit a record and want to hide some fields from unauthorized users. E.g. not An unauthorized user cannot view or edit the salary of an employee
1. You want to disable editing of some sensitive data. E.g. An unauthorized user can see the price of a product but is not able to change it.
**Implementation steps**

* [ ] TODO

## Redirecting users to a role based page

To redirect a user to a specific page based on the user his authorization we can create a redirect page and use the JavaScript_API to check the roles to redirect the user. Each page is authorized to the specific role so even if the user is able to manipulate the page or goes directly to the page he will not have unauthorized access.

### Implementation steps

1. Create a redirect page and
1. Add an `OnInitialize` event to the page
1. * Use the [checkIfCurrentUserHasRole](https://success.outsystems.com/Documentation/11/Reference/OutSystems_APIs/JavaScript_API/Security#checkifcurrentuserhasrole) JavaScript_API function to redirect the user to a specific page.
E.g. If a user has the ProductManager role he will be redirected to the ProductDetail page, if he has the ProductViewer role he will be redirected to the ProductShow page otherwise an not authorized exception is raised.
![screenshot of OnInitialize flow](/images/ProductRedirect.png)
