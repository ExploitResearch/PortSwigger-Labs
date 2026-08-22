# Access Control

<details><summary>Access Control Basic</summary>

Access control is a fundamental security concept that restricts access to resources. It is a way to limit access to systems, networks, physical spaces, and data to authorized users, processes, or devices.

Access control is dependent on authentication and session management:

  - <span style="color: #BE5B00">**Authentication**</span> confirms that the user is who they say they are.
  - <span style="color: #BE5B00">**Session management**</span> identifies which subsequent HTTP requests are being made by that same user.
  - <span style="color: #BE5B00">**Access control**</span>** **determines whether the user is allowed to carry out the action that they are attempting to perform.
</details>

<details><summary>Access control vs Authentication</summary>

**Authentication:**

- **Purpose:** Verifies the identity of someone trying to access a system or resource.
expand_more

- **Process:** Checks credentials like username and password, biometrics, or multi-factor authentication codes.
expand_more

- **Analogy:** Asking for ID at a bar; confirms you are who you say you are, but doesn't tell you what drinks you can order.
**Access Control:**

- **Purpose:** Determines what level of access an authenticated user has to a system or resource.
expand_more

- **Process:** Uses rules and policies based on the user's identity, role, and other factors to grant or deny access.
expand_more

- **Analogy:** Once verified at the bar, your age determines if you can buy alcohol (access control based on your identity).
**Key Differences:**

  - **Focus:** Authentication is about **who** you are, while access control is about **what** you can do.
  - **Timing:** Authentication happens first, confirming identity. Then, access control determines permissions based on that identity.
expand_more

  - **Example:** Logging into your bank account (authentication) allows you to see your balance (access control) but not edit other customers' information.

**Working Together:**

Think of them as a two-step process:

  1. **Authentication:** Are you really you?
  1. **Access Control:** If so, what can you do here?

Both are essential for robust security. Strong authentication prevents unauthorized access, while granular access control ensures users only have the permissions they need, minimizing damage if credentials are compromised.

</details>

<details><summary>Vertical, Horizontal and Context dependent access control</summary>

### Vertical Access Control

Vertical access control refers to the management of access rights in a hierarchical manner, typically based on different levels of authority within an organization. It controls access to resources based on the roles or ranks of users within the organization's hierarchy. For example, in a company, executives might have access to all documents within their department, managers might have access to a subset of those documents relevant to their teams, and individual employees might only have access to documents they create or are explicitly shared with them. This form of access control is common in role-based access control (RBAC) systems, where permissions are often organized in a top-down approach, reflecting the organizational structure.

### Horizontal Access Control

Horizontal access control manages access rights across peers or objects at the same level of hierarchy, rather than based on a vertical structure of authority. This type of control is concerned with ensuring that users or systems at the same level or role cannot access each other's resources without proper authorization. For instance, in a hospital information system, horizontal access control would ensure that one doctor can access only the medical records of their own patients, not those of patients under the care of another doctor, even though both doctors might hold the same rank or position within the hospital. Horizontal access control is crucial for enforcing the principle of least privilege and ensuring privacy and confidentiality among users or processes operating at the same level.

### Context-Dependent Access Control

Context-dependent access control (also known as contextual or situation-based access control) adjusts access permissions based on the context of the access request. Context can include a wide range of factors such as the location from which an access request is made, the time of day, the device being used, the network security level, or the current state of the system or user. For example, an employee might have access to sensitive financial records from within the office network during working hours but not from a public Wi-Fi hotspot after hours. Context-dependent access control allows for more dynamic and granular control of access rights, adapting to the specific circumstances under which access is requested to mitigate potential security risks.

</details>

## **Vertical privilege escalation**

## **Horizontal privilege escalation**

## Labs

- [Insecure direct object references](./Insecure_direct_object_references.md)
- [Method-based access control can be circumvented](./Method-based_access_control_can_be_circumvented.md)
- [Multi-step process with no access control on one step](./Multi-step_process_with_no_access_control_on_one_step.md)
- [Referer-based access control](./Referer-based_access_control.md)
- [URL-based access control can be circumvented](./URL-based_access_control_can_be_circumvented.md)
- [Unprotected admin functionality](./Unprotected_admin_functionality.md)
- [Unprotected admin functionality with unpredictable URL](./Unprotected_admin_functionality_with_unpredictable_URL.md)
- [User ID controlled by request parameter, with unpredictable user IDs](./User_ID_controlled_by_request_parameter,_with_unpredictable_user_IDs.md)
- [User ID controlled by request parameter](./User_ID_controlled_by_request_parameter.md)
- [User ID controlled by request parameter with data leakage in redirect](./User_ID_controlled_by_request_parameter_with_data_leakage_in_redirect.md)
- [User ID controlled by request parameter with password disclosure](./User_ID_controlled_by_request_parameter_with_password_disclosure.md)
- [User role can be modified in user profile](./User_role_can_be_modified_in_user_profile.md)
- [User role controlled by request parameter](./User_role_controlled_by_request_parameter.md)
