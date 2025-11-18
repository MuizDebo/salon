# salon
```mermaid
graph TD
    subgraph System Lifecycle
        direction TB

        %% 1. Initial Access & Setup
        A[Start: Customer/Admin Access App] --> B{User Type?};

        B -- Admin/Staff --> C[Admin/Staff Dashboard];
        B -- Customer --> D[Customer Portal];

        C --> C1[Manage Staff Availability & Services (Rules)];
        C1 --> C2[Update Real-Time Booking Engine Data];
        C2 --> D1; %% Feeds data to Customer Flow

        %% 2. Customer Booking & Payment (Phase 1)
        D --> D1[Browse Services & Check Availability];
        D1 --> D2{Slot Selected?};
        D2 -- No --> D1;
        D2 -- Yes --> D3[Customer Enters/Confirms Details];
        D3 --> D4[System Creates PENDING Booking Record];
        D4 --> D5[Payment Gateway (Paystack/Flutterwave)];
        D5 --> D6{Payment Success?};

        D6 -- Yes --> D7[System Updates Booking Status: CONFIRMED/PAID];
        D7 --> D8[System Sends Confirmation Email/SMS];
        D8 --> E[Booking Confirmed (Ready for Service Day)];

        D6 -- No --> D9[Display Payment Failed/Retry];
        D9 --> D5; 

        %% 3. Service Day Management (Phase 3)
        E --> F[Automated Reminder Sent (24-48 hrs Before)];
        F --> G[Service Day: Staff Checks Calendar];
        G --> H{Customer Arrives?};

        H -- No (No Show) --> I[Staff Marks as NO-SHOW];
        I --> J{Deposit Policy Enforced?};
        J -- Yes --> K[Deposit Retained (Fee)];
        J -- No --> L[Process Refund/Credit];
        K & L --> M[End Transaction & Update Reports];

        H -- Yes (Service Begins) --> N[Service Performed];
        N --> O[POS System Calculation];

        O --> P[Calculate Total Cost - Upfront Fee - Loyalty/Discount];
        P --> Q{Final Balance Due > 0?};

        Q -- Yes --> R[Process Final Payment (Card/Cash)];
        Q -- No --> S[Mark Transaction COMPLETED];

        R --> S;
        S --> T[Update Customer Loyalty Points];
        T --> U[Generate Receipt & Mark Booking COMPLETED];

        %% 4. Reporting & System Cycle
        U & M --> V[Financial & Service Data Flow];
        V --> W[Analytics & Reporting Dashboard (Admin View)];
        W --> X[End Workflow Cycle];
        
    end
```
