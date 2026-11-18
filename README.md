README.md
AD361 Learning Practice 08 — Defect Management
Student: Bashir Abdulkadir
What I Did
I reviewed the North Vacation Booking requirements and documented four findings related to guest limits, reservation dates, availability, and the cleaning fee. I wrote a complete defect report and assigned severity and priority to each finding. I also prepared retest steps and suggested improvements.

I ran the application locally and confirmed that it saved a Beachfront Condo reservation for 13 guests. The other findings came from an AI-assisted source review and still need browser testing.
Project Files
File	Purpose
DEFECT_MANAGEMENT.md	My classifications, defect report, severity and priority ratings, tracking, and suggested improvements.
evidence/source-review.txt	Numbered source excerpts supporting the source-review findings.
ASSIGNMENT.md	Original assignment instructions.
APP_README.md	Original application setup information.
src/	Application source code.
db.json	Rental data used by JSON Server.


Run the Application
Open a terminal in the folder containing package.json and db.json:
npm ci
npx json-server@0.17.4 --watch db.json --port 3001

Keep that terminal running. Open a second terminal in the same folder:
npm run dev

Open the address Vite displays. My application ran at http://localhost:5174.

Visit Home first and wait for the rental listings to load. Then use Add Booking and Bookings without refreshing, because reservations are stored in memory.
Testing Status
I confirmed this result in the browser:
Rental: Beachfront Condo Date: 2026-12-10 Guests: 13

This violates the requirement that reservations allow only 1–12 guests. I documented the defect as NVB-001, with High severity, High priority, and New status.

I have not completed browser testing for the other findings, fixed the defects, or verified a production build.
GitHub Submission
Create an empty public GitHub repository named AD361-Learning-Practice-08. From the project folder, run:
git init
git add .
git commit -m "Document Week 8 defect management findings"
git branch -M main
git remote add origin https://github.com/Bashir3355/AD361-Learning-Practice-08.git
git push -u origin main

After pushing, verify that the repository is public and that the application files and defect report are visible. Submit the repository URL to Canvas.
AI Transparency
I used AI to help examine the source code and organize my documentation. I personally ran the application and reproduced the 13-guest reservation defect. I distinguished that confirmed result from findings that still need browser testing.

