User Form with Validation
This is a Vue.js form component that allows users to edit and submit their profile information, including fields such as name, surname, job title, phone number, address, interests, links, and avatar. The form includes validation rules for required fields, input lengths, and format checks. It also allows toggling between an "edit" and "view" mode, saving the data to local storage.

Features:
Form Fields: Name, surname, job title, phone, email, address, pitch, interests, hobbies, links.
Validation: Custom validation for each field with error messages.
Edit/View Mode: Toggle between editing and viewing profile data.
Local Storage: Saves form data in local storage for persistence across sessions.
Responsive: Works on all screen sizes.
Validation Rules:
Name & Surname: Required, 2-50 characters, letters and spaces only.
Job Title: Optional, up to 100 characters, letters, numbers, and spaces.
Phone: Required, valid phone number format with country code (+<country_code><number>).
Address: Optional, up to 200 characters, letters, numbers, commas, periods, hyphens, and spaces.
Interests & Links: Optional, tags or links with specific formats and lengths.