# GTM Event Schema

| Event Name | Trigger Type | Key Parameters | GA4 Report / Audience |
|------------|--------------|----------------|------------------------|
| booking_step_complete | Custom Event (dataLayer) | step_number, step_name, clinic_location, specialty | Funnel Exploration |
| booking_completed | Custom Event (dataLayer) | booking_id, clinic_location, specialty, booking_status | Conversions, Google Ads |
| call_now_click | Click Trigger (Click URL starts with `tel:`) | clinic_location, page_location, button_position, device_type | Engagement Report, Ads Remarketing Audience |
| whatsapp_click | Click Trigger (Click URL contains `wa.me`) | clinic_location, page_location, button_position, device_type | Engagement Report, Click Analysis |
| patient_guide_form_submit | Form Submission Trigger | guide_name, clinic_location, form_status, page_location | Lead Generation Report |
| patient_guide_download | Link Click Trigger (URL ends with `.pdf`) | guide_name, clinic_location, page_location, download_type | File Download Report |
| clinic_page_view | Page View Trigger (Page Path contains `/clinic/`) | clinic_location, page_title, page_url, traffic_source | Landing Page Report |
| blog_scroll | Scroll Depth Trigger (25%, 50%, 75%, 90%) | article_title, scroll_percent, page_url, author_name | Content Engagement Report |


> **Note:** The `booking_step_complete` events are triggered via custom `dataLayer.push()` calls implemented by the frontend developer. GTM listens for these custom events and forwards them to GA4, enabling step-level funnel analysis in GA4 Funnel Exploration.



#JSON format for APPOINTMENT BOOKING is this
{  
 'event': 'booking_step_complete',
'step_number': 1,
'step_name': 'location_specialty_selected',
'clinic_location': '{{clinic_name}}',
'specialty': '{{specialty_selected}}'
}

{
'event': 'booking_step_complete',
'step_number': 2,
'step_name': 'patient_details_entered',
'phone_provided': true,
'preferred_date': '{{preferred_date}}'
}

{
'event': 'booking_step_complete',
'step_number': 3,
'step_name': 'booking_confirmed',
'clinic_location': '{{clinic_name}}',
'specialty': '{{specialty_selected}}',
'booking_id': '{{booking_id}}'
}

{
'event': 'booking_completed',
'booking_id': '{{booking_id}}',
'clinic_location': '{{clinic_name}}',
'specialty': '{{specialty_selected}}',
'booking_status': '{{booking_status}}'
}

#JSON format for CALL NOW is this
{
'event': 'call_now_click',
'clinic_location': '{{clinic_name}}',
'page_location': '{{page_location}}',
'button_position': '{{button_position}}',
'device_type': '{{device_type}}'
}

#JSON format for WHATSAPP CHAT WIDGET is this
{
'event': 'whatsapp_click',
'clinic_location': '{{clinic_name}}',
'page_location': '{{page_location}}',
'button_position': '{{button_position}}',
'device_type': '{{device_type}}'
}

#JSON format for DOWNLOAD PATIENT GUIDE is this
{
'event': 'patient_guide_form_submit',
'guide_name': '{{guide_name}}',
'clinic_location': '{{clinic_name}}',
'form_status': '{{form_status}}',
'page_location': '{{page_location}}'
}

#JSON format for CLINIC PAGE VIEWED is this
{
'event': 'clinic_page_view',
'clinic_location': '{{clinic_location}}',
'page_title': '{{page_title}}',
'page_url': '{{page_url}}',
'traffic_source': '{{traffic_source}}'
}

#JSON format for BLOG SCROLL is this
{
'event': 'blog_scroll',
'article_title': '{{article_title}}',
'scroll_percent': '{{scroll_percent}}',
'page_url': '{{page_url}}',
'author_name': '{{author_name}}'
}

#Explanation
Funnel explanation
GTM trigger for each step
JSON for Step 1
JSON for Step 2
JSON for Step 3
JSON for booking completed
GA4 Funnel Exploration explanation
Google Ads conversion explanation
