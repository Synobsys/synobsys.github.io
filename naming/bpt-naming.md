---
title: Business Process Technology (BPT) naming conventions
---

# Business Process Technology (BPT) naming conventions

[ ] **tbd check for completeness**

> Adapted from [Fundamentals of Business Process Management](http:/fundamentals-of-bpm.org), Chapter 3 Essential Process Modeling.

## Process

To name a bpt process we should use a _noun_, potentially preceded by an **adjective**, e.g. `OrderFulfillment` or `ClaimHandling`.
Nouns in sequence form like `OrderToCash` and `ProcureToPay` indicating a sequence of main actions, are also possible.

## Activities

For activities the name should begin with a _verb_ in the imperative form followed by a _noun_, typically referring to a business object, e.g. `ApproveOrder`.
The noun may be preceded by an _adjective_, e.g. `IssueDriverLicense`, and the verb may be followed by a _complement_ to explain how the action is being done, e.g. `RenewDriverLicenseViaOfflineAgencies`.

## Events

For events the label should begin with a _noun_ (this would typically be a business object) and should en with a verb in past principle form, e.g. `InvoiceEmitted`, the verb is a past principle to indicate something has just happened. The name may be prefixed by an _adjective_, e.g. `UrgentOrderSent`.

General verbs like "to make", "to do", "to perform" or "to conduct" should be replaced with meaningful verbs that capture the specifics of the activity or event being performed.
