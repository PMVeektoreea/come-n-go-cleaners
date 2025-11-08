# come-n-go-cleaners
A digital cleaning service platform for booking, managing, and tracking cleaning services for homes and offices.
# Come ’n’ Go Cleaners
**Your Trusted On-Demand Cleaning Service**

![Platform Badge](https://img.shields.io/badge/Platform-Mobile%20%26%20Web-blue) ![Tech Badge](https://img.shields.io/badge/Tech-React%2C%20Node.js%2C%20MongoDB-green) ![Status Badge](https://img.shields.io/badge/Status-Active-brightgreen)

Come ’n’ Go Cleaners is a two-sided platform connecting verified cleaners with customers who need short, hourly cleaning sessions. Pay only for the time you need — no long-term commitments, no surprises.

---

## Why This Matters
Maintaining a tidy home shouldn’t require a full-time house help. Many busy professionals, students, and families want occasional, reliable cleaning without the hassle of interviews, verification, or high fees.

Come ’n’ Go Cleaners provides:  
- Safe, verified cleaners on-demand  
- Flexible hourly bookings  
- Transparent pricing and payment  

This ensures convenience, trust, and peace of mind, addressing a real need in Nigerian households and small businesses.

---

## Who This Is For
- Busy professionals who need occasional cleaning  
- Families who prefer part-time domestic help  
- Individuals who want verified, safe cleaners without long-term hire

---

## What It Does
- Book cleaners by the hour in under a minute  
- See available cleaners nearby with skills and hourly rate  
- Pick specific chores for each session  
- View cleaner verification and ratings  
- Track session progress and cleaner arrival in real time  
- Make easy payments in Naira via Quickteller or Interswitch

---

## Key Features
- Pay-per-hour bookings with transparent pricing  
- Cleaner profiles with verification, ratings, and reviews  
- Customizable chore list per booking  
- Real-time status updates and arrival ETA  
- In-app receipts and simple refunds for issues

---

## Tech Summary
- **Mobile App:** React Native (iOS & Android)  
- **Web App:** React for browser access and admin dashboard  
- **Backend/API:** Node.js with Express, REST endpoints  
- **Database:** MongoDB (users, cleaners, bookings, payments, ratings)  
- **Cache/Worker Queue:** Redis + Bull/Bee Queue  
- **Payments:** Quickteller or Interswitch  
- **Notifications:** Firebase Cloud Messaging, SMS gateway  
- **Hosting:** AWS / Render / DigitalOcean, containerized with Docker  
- **CI/CD:** Automated tests, deployments, separate environments

---

## Payment & Booking Flow
1. User confirms a booking  
2. Backend creates a pending booking and payment intent  
3. Payment API called, returning reference/token  
4. User completes payment via secure provider flow  
5. Webhook confirms success/failure  
6. Backend updates booking & payment records  
7. Notifications sent to user & cleaner  

**Security Notes:**  
- No raw card details stored — tokenization or hosted pages used  
- Webhooks verified using provider signatures  
- HTTPS enforced for all endpoints

---

## Market Context & References
- **Growing Market:** Nigerian cleaning & hygiene market ~ USD 1,010.1M in 2024 → projected USD 1,502.2M by 2030 (Grand View Research)  
- **Facility Management Growth:** Nigeria’s facility-management services market USD 8.4B in 2019 → USD 12.7B by 2027 (Allied Market Research)  
- **Pricing Insight:** Residential cleaning services ₦10,000–₦50,000 per session (Palmacedar Cleaning)  
- **Market Opportunity:** Urbanization & hygiene awareness drive demand (6W Research)

---

## Vision
To make short-term cleaning simple, safe, and trustworthy for everyone in Nigeria while providing cleaners with verified, flexible work opportunities.

---

## Future Considerations
- Add a dispatcher service to optimize cleaner routing  
- Introduce analytics & reporting microservices  
- Expand to multi-city support & multiple currencies

---

## Installation & Usage
1. Clone the repo  
   ```bash
   git clone https://github.com/PMVeektoreea/come-n-go-cleaners.git
npm install
npm start
Run mobile app via Expo / Android Studio / Xcode

Contributing

Fork the repository

Create a new branch (git checkout -b feature-name)

Commit your changes (git commit -m "Add feature")

Push to the branch (git push origin feature-name)

Open a pull request 
## License
MIT License

