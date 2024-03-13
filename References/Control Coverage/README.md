# Security controls covered by the AAD Scanner

This page displays security controls that are scanned via AAD Scanner. Controls have a 'Severity' field to help distinguish issues by degree of risk. 

## Resource types supported by the AzSK.AAD scanner module

Below resource types can be checked for validating the security controls. 

|FeatureName|
|---|
|[AppRegistration](#AppRegistration)|
|[EnterpriseApplication](#EnterpriseApplication)|

## AppRegistration

<body>
<table><tr><th>Description & Rationale</th><th>ControlSeverity</th></tr>
<td>
<b>Ensure all return URLs configured for an application to use HTTPS endpoints.</b>
</br>
Ensuring that return URLs for an application exclusively use HTTPS endpoints is crucial for security. During authentication flows, tokens are often transmitted to these URLs after successful authentication. If a return URL lacks HTTPS encryption, it exposes tokens to potential interception, compromising sensitive data security.
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
Do not permit orphaned apps (i.e., apps with no owners) in the tenant.
</b> </br>
From a governance standpoint, it is important that every application has one or more owners who are responsible for the upkeep of the application's record in the tenant, rotating credentials, etc.
</td>
<td> High </td>
</tr>
<tr>
<td>
<b>
Enterprise (line of business) apps should be tenant scope only.
</b></br>
Line of business (LOB) applications are usually written to meet a specific company's business needs. Such applications should be restricted to the current tenant only (i.e., the tenant where they are registered).
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
Avoid the use of wildcard characters in redirect URIs.
</b> </br>
Including wildcard characters in redirect URIs introduces significant security vulnerabilities. Attackers can exploit this by creating fraudulent redirect URIs resembling legitimate ones, leading to potential phishing attacks and unauthorized access to authentication tokens. In the case of public clients, this can directly grant attackers access tokens, while for confidential apps, it can enable auth code injection attacks to obtain access tokens.
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
Implicit Flow should not be allowed in App Registration.
</b> </br>
Using implicit flow, exposes the access token in the URL fragment, and does not support PKCE, making it vulnerable to access token leage and token replay attacks.
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
Ensure redirect URIs have valid DNS ownership.
</b> </br>
Allowing redirect URIs with no DNS ownership allows attackers to get ownership of the URL before the actual owners, enabling them to get auth tokens by phishing users to these sites under attackers' controls.
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
All owners of the app registration should be FTE only.
</b> </br>
Owners of the app have access to critical app settings such as auth flows, credentials and API permissions. Providing ownership to FTE accounts only leads to better app governance and prevents malicious users from outside the enterprise from accessing critical data.
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
App Registrations should not have long expiry secrets.
</b> </br>
If client secrets are a must to be used, ensure that the secret expiry is not more than 90 days. Long expiry secrets can lead to unauthorized access for a longer window in case of secret compromise."
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
App Registrations should request the least permissions needed to various resources.
</b>
</br>
Apps should only require the least needed permission possible to prevent risky unauthorized access to enterprise resources. App permissions are riskier than delegated permissions as these do not require user consent.
</td><td> High </td>
</tr>
<tr>
<td>
<b>
App Registrations with no owners should not have long expiry secrets.
</b>
</br>
Apps without any ownership can either be legacy apps no longer being used or app whose owners have left the organization. If client secrets with secret expiry of more than 90 days are associated this could lead to a longer attack window of app compromise outside the enterprise. Ensuring enterprise security hygiene, either the app or the secret should be deleted and proper ownership should be defined.
</td> <td> High </td>
</tr>
<tr>
<td>
<b>
Enable app instance lock for multi-tenant apps on all properties.
</b>
</br>
App instance property lock prevents owners of Enterprise Applications in other tenants from creating credentials of the SPN. The credentials can allow misuse of SPNs to gain unauthorized access to critical Enterprise data.
</td> <td> High </td>
</tr>
</table>
</body>

## EnterpriseApplication

<body>
<table><tr><th>Description & Rationale</th><th>ControlSeverity</th></tr>
<td>
<b>
All owners of the enterprise application should be FTE only.
</b>
</br>
Owners of the enterprise app have access to critical app settings such as group permissions, credentials and user assignments. Providing ownership to FTE accounts only leads to better app governance and prevents malicious users from outside the enterprise from accessing critical data.
</td>
<td> High </td>
<tr>
<td>
<b>
Enterprise (line of business) apps should be granted the least permissions needed to various resources.
</b>
</br>
Apps should only be granted the least needed permission possible to prevent risky unauthorized access to enterprise resources. App permissions are riskier than delegated permissions as these do not require user consent.
</td>
<td> High </td>
</tr>
<tr>
<td>
<b>
Enterprise application should not use credentials.
</b>
</br>
Password credentials tend to be easier to compromise via various attacks. They are also symmetric leading to attack vectors on both ends of the flow.
</td> <td> High </td>
</tr>