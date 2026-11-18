Learning Practice 08: Defect Management
Student: Bashir Abdulkadir
Application: North Vacation Booking
Report date: November 18, 2026

I reviewed the application requirements and used AI to help examine the source code. I ran the application locally and confirmed that it saved a reservation for 13 guests, even though the maximum allowed is 12. The other findings are based on source review and still need browser testing.
Requirements
ID	Requirement
R1	Reservations allow 1–12 guests.
R2	Reservations last 1–31 nights.
R3	Check-in must occur before checkout.
R4	All requested nights must be available.
R5	Each valid reservation includes a one-time $50 cleaning fee.
R6	Invalid information must produce an error.


Step 1: Classify the Findings
Finding	Classification	My explanation
NVB-001: Reservations allow more than 12 guests	Product defect — reproduced in the browser	I entered 13 guests for Beachfront Condo on December 10, 2026. The application saved the reservation without an error, which violates R1 and R6.
NVB-002: Missing checkout date and stay-length validation	Product defect — identified through source review	I found that the form provides only one date field. There is no checkout date or number-of-nights field to support the required stay length and date-order checks in R2 and R3.
NVB-003: Missing availability validation	Product defect — identified through source review	With AI assistance, I found that the booking function adds reservations without checking existing bookings or availability. This does not enforce R4, but I have not yet reproduced a conflicting reservation in the browser.
NVB-004: Missing cleaning-fee calculation	Product defect — identified through source review	I found no cleaning-fee or reservation-total calculation in the reviewed booking code. This does not support R5; I have not tested an actual payment or confirmed a financial loss.


I classified these findings as product defects because they relate to stated requirements. A test expecting 13 guests to be accepted would be a test issue, while a request for discount codes would be a requested change. A result without enough evidence to explain it would require further investigation.
Step 2: Complete Defect Report
Field	Information
Defect ID	NVB-001
Title	Application saves reservations with more than 12 guests
Date reported	November 18, 2026
Reporter	Bashir Abdulkadir
Application or feature	North Vacation Booking — Add Booking
Test environment	Windows computer using Microsoft Edge; application at http://localhost:5174 and JSON Server at http://localhost:3001.
Preconditions	I started JSON Server and Vite, opened Home, and waited for the rental listings to load.
Steps to reproduce	1. Open Home. 2. Click Add Booking. 3. Select Beachfront Condo. 4. Enter December 10, 2026. 5. Enter 13 guests. 6. Click Confirm Booking. 7. Click Bookings without refreshing.
Expected result	The application should display an error explaining that only 1–12 guests are allowed and should not save the reservation.
Actual result	I saw the saved entry: “Rental: Beachfront Condo Date: 2026-12-10 Guests: 13.” The application accepted the invalid guest count without an error.
Severity	High — the reservation feature accepts information that violates a major booking requirement.
Priority	High — this should be fixed before the next release to prevent invalid reservations.
Initial status	New — reproduced and awaiting a fix.
Related requirement or test case	R1 and R6; TC-GUEST-13.
Supporting evidence	Source excerpts are available in evidence/source-review.txt. A screenshot of the saved 13-guest reservation should be attached as NVB-001-13-guests.png.


Step 3: Assign Severity and Priority
Defect	Severity	Priority	My explanation
NVB-001: Guest maximum	High	High	I confirmed that the application accepts an invalid guest count. This affects reservation correctness and should be fixed before release.
NVB-002: Missing stay range	High	High	The booking form cannot represent the required check-in and checkout range. This affects a major part of making a reservation.
NVB-003: Missing availability check	High	High	The reviewed code does not prevent conflicting reservations. This should be addressed before release and verified through browser testing.
NVB-004: Missing cleaning fee	High	High	The required fee is absent from the reviewed reservation calculations. This should be implemented and tested before release.


I used severity to describe each defect’s impact and priority to explain how soon it should be fixed.
Tracking and Retesting
Defect	Current status	My planned retest
NVB-001	New — reproduced	I will check that 1 and 12 guests are accepted and that 0, 13, and blank input are rejected without saving a reservation.
NVB-002	New — source review	I will test 1- and 31-night stays, then check that invalid lengths and incorrect date order produce errors.
NVB-003	New — source review	I will attempt overlapping reservations for the same rental and check that available dates remain bookable.
NVB-004	New — source review	I will verify that Beachfront Condo totals $250 for one night and $450 for two nights, including the $50 cleaning fee exactly once.


I have not fixed or closed these defects. After a fix is available, I will retest it and close the defect only if the expected behavior is confirmed. If the problem remains, I will reopen it.
Possible Root Causes and Process Improvements
Finding	Possible cause	My suggested improvement
Guest maximum	The form includes a minimum guest limit but no upper-limit validation.	I recommend validating the full 1–12 range and displaying a clear error.
Missing stay range	The booking model stores only one date.	I recommend adding check-in and checkout fields with date-order and stay-length checks.
Missing availability check	The booking function saves data without checking for conflicts.	I recommend checking every requested night before accepting a reservation.
Missing cleaning fee	The pricing requirement was not included in the reviewed booking logic.	I recommend using one calculation for the nightly total and one-time cleaning fee.


These are possible explanations based on the code, rather than confirmed causes from the development team.
AI Transparency
I used AI to help review the source code, organize the findings, and draft the documentation. I ran the application locally and confirmed the 13-guest reservation defect myself. The remaining findings are based on source review and still need browser testing.