---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-31"

keywords: Authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

subcollection: appid

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Troubleshooting: General
{: #troubleshooting}

If you have problems while you're working with {{site.data.keyword.appid_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}

## Getting help and support
{: #ts-gettinghelp}

You can get help by searching for information or by asking questions through a forum. You can also open a support ticket. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
  * If you have technical questions about {{site.data.keyword.appid_short_notm}}, post your question on <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and tag your question with "ibm-appid".
  * For questions about the service and getting started instructions, use the <a href="https://developer.ibm.com/" target="_blank">IBM Developer Answers <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> forum. Include the `appid` tag.
  * Reach out directly to the development team on [Slack](https://ibm-container-service.slack.com)! 

For more information about getting support, see [how do I get the support that I need](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## A user is not redirected to the app after sign in
{: #ts-signin-fail}

{: tsSymptoms}
A user signs in to your application through an identity provider's sign in page, and either nothing happens or the sign-in fails.

{: tsCauses}
Sign in might fail for the following reasons:

* Your redirect URL was not properly added to [the whitelist](/docs/services/appid?topic=appid-faq#faq-redirect).
* The user is not authorized.
* The user tried to sign in with the wrong credentials.

{: tsResolve}
For a redirect to occur:

* Verify that your redirect URL is correct. It must be exact for the redirect to work.
* Be sure that your user is signing in with the right credentials
* Check that they're configured in your identity provider user settings.



## A custom URI is rejected
{: #ts-custom-uri}

{: tsSymptoms}
When you enter a web redirect URL that uses a custom URL Scheme it is rejected by the {{site.data.keyword.appid_short_notm}} console.

{: tsCauses}
Your URL might be rejected for the following reasons:

* The URL does not follow an `http` or `https` scheme
* The URL ends with `://`
* There is a typographical error in your URL

The limitations are in place for security purposes.

{: tsResolve}
To resolve the issue, verify that the URL is correct. If your URL does not meet the requirements, you can create an HTTPS endpoint in your app to redirect the received grant code to your custom URL. Specify the created endpoint as your redirect URL in the {{site.data.keyword.appid_short_notm}} console. For more information about redirect URIs, see [Adding redirect URIs](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)

## A user is not redirected to the identity provider
{: #ts-redirect}

{: tsSymptoms}
A user tries to sign in to your application, but the sign-in page doesn't display when prompted.

{: tsCauses}
The identity provider can fail for several reasons:

* Your configured redirect URL is incorrect.
* The identity provider doesn't recognize the authentication request.
* The identity provider expects HTTP-POST binding.
* The identity provider expects a signed AuthnRequest.

{: tsResolve}
You can try some of these solutions:

* Update your sign-in URL. This URL is sent as part of the AuthnRequest and must be exact.
* Be sure that your {{site.data.keyword.appid_short_notm}} metadata is set correctly in your identity provider settings.
* Configure your identity provider to accept the AuthnRequest in the HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} does not support signing AuthnRequests.

If none of the solutions work, it is possible that you might have a connection issue.
{: tip}


## An attribute is showing the wrong value
{: #ts-saml-attribute}

{: tsSymptoms}
An attribute value exists in a user profile, but it's not associated with the correct attribute.

{: tsCauses}
The user profile attribute is not mapped correctly.

{: tsResolve}
Map the attribute in your identity provider settings. {{site.data.keyword.appid_short_notm}} expects the following attributes:
* `name`
* `email`
* `locale`
* `picture`



## Error: Too many requests
{: #ts-requests}

{: tsSymptoms}
You attempt to view the home page of your app but receive the following error:

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
You might receive a "too many requests" error if you are performing automated testing with only one virtual user. Each user is limited to five sign in attempts in a one-minute time span. Sign in attempts are limited in order to prevent brute force DDoS and other types of similar attacks.

{: tsResolve}
To resolve the issue, you might want to use multiple virtual users when you perform testing.
</br>
