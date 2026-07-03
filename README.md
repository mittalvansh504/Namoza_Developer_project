### Integration Design

I would use a **direct backend API integration** instead of Zapier or Make because it gives better control over the complete workflow and makes it easier to handle validation, errors, retries, and monitoring.

When a patient submits the consultation form, the request first goes to the backend (Spring Boot/Node.js). The backend validates the form data and then checks HubSpot using the **Contacts API** to see if a contact with the same phone number already exists. Since HubSpot normally uses **email** for deduplication and this form doesn't collect email, I would handle phone number deduplication in the backend. If the phone number already exists, I would update the existing contact; otherwise, I would create a new contact with Name, Phone, Clinic Preference, Source = "Google Ads - Consultation Landing Page", and Lead Status = "New Enquiry".

After the contact is successfully created or updated, the backend sends a confirmation WhatsApp message through the **Karix WhatsApp Business API**. Once the form submission is successful, Google Tag Manager fires the **consultation_form_submitted** event, which is sent to GA4 and imported into Google Ads as a conversion. This allows Google Ads to optimize campaigns based on successful consultation form submissions.

The biggest challenge in this setup is **phone number deduplication**. If I rely only on HubSpot's default behavior, duplicate contacts may be created because HubSpot identifies contacts using email by default. To avoid this, my backend always searches for an existing contact using the phone number before creating a new one. If the HubSpot API is temporarily unavailable, I would save the lead in a database or queue and retry the request automatically so that no enquiry is lost.

To make sure the WhatsApp message is sent within **2 minutes**, I would monitor API response times, maintain logs for every request, implement automatic retries for temporary failures, and configure alerts if message delivery is delayed or fails. This helps ensure the integration remains reliable while meeting the required SLA.
