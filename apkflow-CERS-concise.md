
 * 

### Page-by-Page API and Procedure Flow

Detailed sequence mapping UI actions to backend procedures.

---

#### **1. Login Page (`LoginPage.xaml.cs`)**

This page handles user authentication in two main steps: getting the OTP and submitting it.

**A. Get OTP Flow**

1.  **UI Action**: User enters their mobile number and clicks the "Get OTP" button.
2.  **Event Handler**: This triggers the `btn_getotp_Clicked` event handler in `LoginPage.xaml.cs`.
3.  **App-Side Logic**: The handler makes a series of API calls to validate the user and generate an OTP.
    *   **Call 1: Check User Type**
        *   **API Endpoint Hit**: `POST /api/CheckUserType` (handled by `CheckUserTypeController`).
        *   **Stored Procedure Called**: `Mobile_getusertype` is executed to determine if the user is a Candidate, Agent, or Observer.
    *   **Call 2: Validate Credentials**
        *   **API Endpoint Hit**: `POST /api/UserLogin` (handled by `UserLoginController`) for Candidates/Agents OR `POST /api/ObservorLogin` (handled by `ObservorLoginController`) for Observers.
        *   **Stored Procedure Called**: `Mobile_CERS_AppLogin` or `Mobile_CERS_ObservorLogin` is executed to validate the user's credentials and nomination status.
    *   **Call 3: Generate and Save OTP**
        *   **API Endpoint Hit**: `POST /api/GetOTP` (handled by `GetOTPController`).
        *   **Stored Procedure Called**: `Mobile_CERS_SaveOtp` is executed to generate a new OTP and save it to the database, associated with the user's mobile number.

**B. Submit OTP Flow**

1.  **UI Action**: User enters the received OTP and clicks the "Submit OTP" button.
2.  **Event Handler**: This triggers the `btn_submitotp_Clicked` event handler in `LoginPage.xaml.cs`.
3.  **App-Side Logic**: The handler first verifies the OTP. If successful, it proceeds to download the necessary initial data for the user.
    *   **Call 1: Verify OTP**
        *   **API Endpoint Hit**: `POST /api/CheckOtp` (handled by `CheckOtpController`).
        *   **Stored Procedure Called**: `Mobile_CERS_CheckOtp` is executed to validate the entered OTP against the one stored in the database.
    *   **Call 2: Download Initial Data (after successful OTP check)**
        *   **For Candidates/Agents**:
            *   **API Endpoint Hit**: `POST /api/ExpenditureDetails` (handled by `ExpenditureDetailsController`).
            *   **Stored Procedures Called**: `getExpenseSource`, `Mobile_getPaymentModes`, and `Mobile_getsaveData` are executed to load master data and existing expenditure records.
        *   **For Observers**:
            *   **API Endpoint Hit**: An endpoint (likely in a dedicated `ObserverController`) is called.
            *   **Stored Procedure Called**: `Mobile_getobserver_candidates` is executed to get the list of candidates assigned to that observer.

---

#### **2. Dashboard Page (`DashboardPage.xaml.cs`)**

This is the main landing page for Candidates/Agents after login.

**A. Final Submit Flow**

1.  **UI Action**: User clicks the "Final Submit" button to submit all their expenditure records.
2.  **Event Handler**: This triggers the `btn_finalsubmit_Clicked` event handler in `DashboardPage.xaml.cs`.
3.  **App-Side Logic**: The handler calls the API to mark all saved data as final.
    *   **API Endpoint Hit**: An endpoint like `POST /api/FinalSubmit` (likely handled by a controller like `AddExpenditureController` or a new `FinalSubmitController`).
    *   **Stored Procedure Called**: `Mobile_finalsaveData` is executed to update the status of all expenditure records for the user to "Final Submitted".

---

#### **3. Add Expenditure Page (`AddExpenditureDetailsPage.xaml.cs`)**

This page is for creating a new expenditure entry.

**A. Save Expenditure Flow**

1.  **UI Action**: User fills in the expenditure details and clicks the "Save" button.
2.  **Event Handler**: This triggers the `btn_save_Clicked` event handler.
3.  **App-Side Logic**: The handler gathers all the form data, including any attached files, and sends it to the API to be saved.
    *   **API Endpoint Hit**: `POST /api/AddExpenditure` (handled by `AddExpenditureController`).
    *   **Stored Procedure Called**: `Mobile_saveData` is executed to insert a new expenditure record into the database.

---

#### **4. Edit Expenditure Page (`EditExpenditureDetailsPage.xaml.cs`)**

This page is for modifying an existing expenditure entry.

**A. Update Expenditure Flow**

1.  **UI Action**: User modifies the expenditure details and clicks the "Update" button.
2.  **Event Handler**: This triggers the `btn_update_Clicked` event handler.
3.  **App-Side Logic**: The handler sends the updated data to the API.
    *   **API Endpoint Hit**: An endpoint like `PUT /api/UpdateExpenditure` (likely handled by `AddExpenditureController` or a similar controller).
    *   **Stored Procedure Called**: `Mobile_updatesaveData` is executed to update the existing expenditure record in the database.

This detailed breakdown should give you the clear, end-to-end connection from the UI to the database for each key action in the application. Let me know if you'd like me to elaborate on any other page or flow