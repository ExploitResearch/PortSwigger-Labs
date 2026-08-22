# Business logic vulnerabilities

Business Logic Vulnerabilities are flaws in the design and implementation of an application that allows an attacker to elicit unintended behaviour. This potentially enables attackers to manipulate legitimate functionality to achieve a malicious goal.

**Note:
**The term "business logic" simply refers to the set of rules that define how the application operates. As these rules aren't always directly related to a business, the associated vulnerabilities are also known as "application logic vulnerabilities" or simply "logic flaws".

Logic flaws are often invisible to people who aren't explicitly looking for them as they typically won't be exposed by normal use of the application. However, an attacker may be able to exploit behavioral quirks by interacting with the application in ways that developers never intended.

One of the main purposes of business logic is to enforce the rules and constraints that were defined when designing the application or functionality. Broadly speaking, the business rules dictate how the application should react when a given scenario occurs. This includes preventing users from doing things that will have a negative impact on the business or that simply don't make sense.

Logic-based vulnerabilities can be extremely diverse and are often unique to the application and its specific functionality. Identifying them often requires a certain amount of human knowledge. This makes them difficult to detect using automated vulnerability scanners. As a result, logic flaws are a great target for bug bounty hunters and manual testers in general. 

For example, they might be able to complete a transaction without going through the intended purchase workflow.

### [Examples of business logic vulnerabilities](https://portswigger.net/web-security/logic-flaws/examples)

### **Example 1 – Change Another User’s Password**

<u>**Functionality**</u>

The application has a password change for end users and administrators.

  - End users need to fill out the username, existing password, new password and confirm new password fields.
  - Administrators only need to fill out the username, new password and confirm new password fields.

<u>**Assumption**</u>

The client-side interface presented to users and administrators is different but the password change is controlled for both users by the same function.

<u>**Code**</u>

```javascript
String existingPassword = request.getParameter(“existingPassword”);
if (null == existingPassword) {
trace(“Old password not supplied, must be an administrator”);
return true;
}
else
{
trace(“Verifying user’s old password”);
...
```

<u>**Attack**</u>

A regular user submits a request to change another user’s password by simply not supplying the existing password.

### Example 2 – Bypass Checkout Functionality

<u>**Functionality**</u>

The application has a “place an order” functionality that follows the following stages:
• Browse the product catalogue and add items to the shopping basket.
• Return to the shopping basket and finalize the order.
• Enter the payment.
• Enter delivery information.

<u>**Assumption**</u>

The developers assumed that users would always access the stages in the intended sequence.

<u>**Attack**</u>

The user proceeds directly from stage 2 to stage 4, finalizing the order for delivery without paying for the order.
• Browse the product catalogue and add items to the shopping basket.
• Return to the shopping basket and finalize the order.
• Enter delivery information.

### Example 3 – Beating a Business Limit

<u>**Functionality**</u>

A banking application allows users to transfer funds between bank accounts. As a precaution against fraud, the application prevents users from transferring a value greater than $10,000

<u>**Assumption**</u>

The developers put a check in place to ensure that no transaction greater than $10,000 is allowed to go through.

<u>**Code**</u>

```javascript
bool CAuthCheck::RequiresApproval(int amount) {
if (amount <= m_apprThreshold)
return false;
else return true; }
...
```

<u>**Attack**</u>

The developers overlooked the possibility that a user would attempt to process a transfer for a negative amount. Any negative number would clear the approval test because it is less than the threshold value.
Therefore, a user who wants to transfer $20,000 from account A to account B could simply initiate a transfer -$20,000 from account B to account A bypassing the antifraud defence.

### Example 4 – Cheating on Bulk Discounts

<u>**Functionality**</u>

An e-commerce website allows users to order software products and qualify for bulk discounts if a suitable bundle of items was purchased. The following are the steps involved in the bulk discount functionality:

  1. User adds items in basket.
  1. If one of the items qualifies for a bulk discount, a discount is applied on the entire cart.
  1. User purchases order

<u>**Assumption**</u>

Users will purchase the chosen bundle after the discount is applied. 

<u>**Attack**</u>

User can exploit this logic flaw by performing the following steps:

  1. User adds items in basket including item that gives the user a bulk discount.
  1. The discount is applied on the entire cart.
  1. User goes back to the cart and removes the item that entitled him to a discount.
  1. Although the item is removed, the discount is still approved, and the user purchases the order at a discounted price.

### Impact of Business Logic Vulnerabilities

The impact is highly variable and depends on the functionality that contains the business logic flaw.
• Confidentiality – Access to other users’ data.
• Integrity – Access to update other users’ data
• Availability – Access to delete users and their data.

### How to Find & Exploit Business Logic Vulnerabilities

  - Map the application. Make note of each and every component in the application and how it operates.
- If you have access to the code, review the code responsible for each component.
  - For each component determine:
- The potential business flow.
- The assumptions that could have been made by the developers / architects during the design phase.
  - Test each component for all possible use cases that are outside of the intended business flow.

### Preventing Business Logic Vulnerabilities

  - Ensure that there is proper documentation of the application’s design that outlines every assumption that the designer(s) made.
  - Mandate that all source code is properly commented and includes the following items:
1. The purpose and intended use of each code component.
1. The assumptions made by each component about anything that is outside of its direct control.
1. References to all client-side code that uses the component.
  - Write code as clearly as possible.
  - Perform security-focused code reviews of the application’s design.

## Labs

- [Authentication bypass via encryption oracle](./Authentication_bypass_via_encryption_oracle.md)
- [Authentication bypass via flawed state machine](./Authentication_bypass_via_flawed_state_machine.md)
- [Bypassing access controls using email address parsing discrepancies](./Bypassing_access_controls_using_email_address_parsing_discrepancies.md)
- [Excessive trust in client-side controls](./Excessive_trust_in_client-side_controls.md)
- [Flawed enforcement of business rules](./Flawed_enforcement_of_business_rules.md)
- [High-level logic vulnerability](./High-level_logic_vulnerability.md)
- [Inconsistent handling of exceptional input](./Inconsistent_handling_of_exceptional_input.md)
- [Inconsistent security controls](./Inconsistent_security_controls.md)
- [Infinite money logic flaw](./Infinite_money_logic_flaw.md)
- [Insufficient workflow validation](./Insufficient_workflow_validation.md)
- [Low-level logic flaw](./Low-level_logic_flaw.md)
- [Weak isolation on dual-use endpoint](./Weak_isolation_on_dual-use_endpoint.md)
