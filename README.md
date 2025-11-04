# Tamara Integration Handbook:
This guide outlines the backend steps for integrating the Tamara payment gateway.
> **📚 Highly Recommended:** Before starting, please review the [General Payment Integration Handbook](https://github.com/AhmedRaslan2022/payment-integration-handbook/tree/main) to understand the complete payment flow and core concepts like webhooks.

-----

## 1\. 📖 Review Documentation

Start by carefully reading the official Tamara API documentation to understand all available endpoints, request/response structures, and authentication methods.
  * **Official Tamara Docs:** [https://docs.tamara.co/](https://docs.tamara.co/docs/introduction-to-tamara)
  * **API Reference:** [https://docs.tamara.co/reference/tamara-api-reference-documentation](https://docs.tamara.co/reference/tamara-api-reference-documentation)
  
-----

## 2\. 🔗 Register Your Webhook

Register your webhook endpoint to receive payment updates from Tamara (e.g., payment status changes).
  * **API Doc:** [Register Webhook URL](https://docs.tamara.co/reference/registerwebhookurl)
  * If you are unfamiliar with webhooks, review the [General Payment Integration Handbook](https://github.com/AhmedRaslan2022/payment-integration-handbook/tree/main).
 * After a successful registration call, you must call the GET Retrieve all webhooks endpoint. Check the response list to confirm that your new webhook URL is present. This verifies that the registration was successful.
> 💡 **Tip:** If the registration API request fails in Postman, try sending the request using cURL. Alternatively, register via the Tamara Partner Portal: [Webhook Registration & Order Authorisation](https://docs.tamara.co/docs/transaction-authorisation).

-----

## 3\. 🔀 Implement Redirection URLs

After the user attempts payment on Tamara's page, they will be redirected back to your site. You must create endpoints to handle these return URLs.
  * **Success URL:** Handles successful payments.
  * **Failure URL:** Handles failed payments.
  * **Cancel URL:** Handles user-canceled payments.
  * **API Doc:** [Direct Online Checkout](https://docs.tamara.co/docs/direct-online-checkout)
   
-----

## 4\. 🛠 Implement "Create Checkout Session" Endpoint

Implement the "Create Checkout Session" API call. This is the core endpoint to initiate a payment **when the user selects Tamara**.
  * **API Doc:** [https://docs.tamara.co/reference/createcheckoutsession](https://docs.tamara.co/reference/createcheckoutsession)
  * **Ensure all required fields** are included in your request.
> 🔎 **Debugging Tip:** Use a tool like JsonGrid to facilitate debugging and quickly find any missing fields or data formatting errors.

-----

## 5\. 📢 Handle Webhook Events

Implement the server logic to process asynchronous webhook notifications from Tamara. This is critical for confirming payment status independently of the user's redirection.
> **❗ CRITICAL:** You **must** respond to the webhook request with an **HTTP 200 OK** status code *immediately* before processing any business logic.
>
> Failure to do so will cause Tamara to assume the notification failed and repeatedly retry sending it.
  * Refer to the [General Payment Integration Handbook](https://github.com/AhmedRaslan2022/payment-integration-handbook/tree/main) for best practices on handling webhooks.
  * **API Doc:** [Direct Online Checkout](https://docs.tamara.co/docs/transaction-authorisation)
  
-----

## 6\. 📋 Authorise the Order

Call the Authorise Order endpoint to authorize the payment once you receive the `approved` status in the webhook.
  * **API Doc:** [Authorise Order](https://docs.tamara.co/reference/authoriseorder)
  
-----

## 7\. 💰 Capture the Payment

Call the Capture Payment endpoint to transfer the authorized amount to the merchant account once the order is shipped or fulfilled.
  * **API Doc:** [Capture Payment](https://docs.tamara.co/reference/capturepayment)
-----
 
## 8\. 🧪 Testing & Go-Live Checklist (Frontend Collaboration)

The final phase involves a joint effort with the frontend teams to validate the customer journey, UI experience, and full end-to-end processing across all scenarios using the **Sandbox environment**.

[Testing Guide](https://docs.tamara.co/docs/testing-scenarios)

[Go-Live Testing Checklist](https://docs.tamara.co/docs/testing-checklist)

[Testing Cards](https://docs.tamara.co/docs/testing-cards)



