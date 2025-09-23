┌─────────────────────────────────────────────────────────────────┐
│                    CANDIDATE LOGIN FLOW                        │
└─────────────────────────────────────────────────────────────────┘

📱 LoginPage.xaml.cs
    ↓ User enters mobile number
    ↓ btn_getotp_Clicked()
    
🌐 API Call: CheckUserType_Get()
    ↓ URL: baseurl + "api/CheckUserType?MobileNo={encrypted_mobile}"
    ↓ Controller: CheckUserTypeController.cs
    
🗄️  Stored Procedure: sec.Mobile_getusertype
    ↓ Returns: UserType = "Candidate" or "Agent"
    
🌐 API Call: userlogin_Get()
    ↓ URL: baseurl + "api/UserLogin?MobileNo={encrypted_mobile}"
    ↓ Controller: UserLoginController.cs
    
🗄️  Stored Procedure: sec.Mobile_CERS_AppLogin
    ↓ Query: SELECT AUTO_ID, VOTER_NAME, CONSTITUENCY_CODE, ...
    ↓        FROM sec.CandidatePersonalInfo 
    ↓        WHERE MOBILE_NUMBER = @MobileNo
    
📱 Local Storage: UserDetailsDatabase.AddUserDetails()
    ↓ Stores: AutoID, CONSTITUENCY_CODE, VOTER_NAME, etc.




┌─────────────────────────────────────────────────────────────────┐
│                    CANDIDATE LOGIN FLOW    2                     │
└─────────────────────────────────────────────────────────────────┘

📱 LoginPage.xaml.cs
    ↓ User enters mobile number: "9876543210"
    ↓ btn_getotp_Clicked()
    
🌐 API Call: CheckUserType_Get("9876543210")
    ↓ URL: baseurl + "api/CheckUserType?MobileNo={encrypted_mobile}"
    ↓ Controller: CheckUserTypeController.cs
    ↓ RETURNS: HTTP Status Code (int)
    
🗄️  Stored Procedure: sec.Mobile_getusertype @MobileNo='9876543210'
    ↓ RETURNS: UserType = "Candidate" or "Agent"
    ↓ Preferences.Set("UserType", "Candidate")
    
🌐 API Call: userlogin_Get("9876543210")
    ↓ URL: baseurl + "api/UserLogin?MobileNo={encrypted_mobile}"
    ↓ Controller: UserLoginController.cs
    ↓ RETURNS: HTTP Status Code (int) - 200, 300, 400, 500
    
🗄️  Stored Procedure: sec.Mobile_CERS_AppLogin @MobileNo='9876543210'
    ↓ RETURNS 2 DataTables:
    ↓ 
    ↓ Table 1 (Status):
    ↓   statuscode: 200, Msg: "Successfully Logged In"
    ↓   OR statuscode: 300, Msg: "Invalid Contestant"
    ↓ 
    ↓ Table 2 (User Data - if statuscode = 200):
    ↓   AUTO_ID: "12345"
    ↓   EPIC_NO: "ABC1234567"
    ↓   VOTER_NAME: "John Doe"
    ↓   MOBILE_NUMBER: "9876543210"
    ↓   CONSTITUENCY_CODE: "1309001001"  ← WARD CODE
    ↓   Panchayat_Name: "Ward 1 - Block Name, District"
    ↓   LoggedInAs: "Self" or "Agent"
    ↓   NominationForName: "Panchayat Member"
    ↓   LimitAmt: "500000"
    ↓   ExpStatus: "N" (No expenses yet)
    ↓   expStartDate: "2024-01-01"
    ↓   expEndDate: "2024-02-20"
    ↓   + 20+ more fields...
    
📱 Local Storage: UserDetailsDatabase.AddUserDetails()
    ↓ Clears existing data: userDetailsDatabase.DeleteUserDetails()
    ↓ Decrypts all encrypted fields from API response
    ↓ Creates UserDetails object with:
    ↓   item.AUTO_ID = "12345"
    ↓   item.CONSTITUENCY_CODE = "1309001001"  ← KEY FIELD
    ↓   item.VOTER_NAME = "John Doe"
    ↓   item.LimitAmt = "500000"
    ↓   item.LoggedInAs = "Self"
    ↓   item.ExpStatus = "N"
    ↓   ... (all other fields)
    ↓ 
    ↓ Stores in SQLite: userDetailsDatabase.AddUserDetails(item)
    
🔄 Method Return Values:
    ↓ CheckUserType_Get() → int (200=success, 404=not found)
    ↓ userlogin_Get() → int (200=success, 300=invalid, 500=error)
    
✅ Success Path (if both return 200):
    ↓ Generate OTP: service.GetOtp(mobile)
    ↓ Show OTP input screen
    ↓ After OTP verification → DashboardPage.xaml
    
❌ Error Paths:
    ↓ 300: "Invalid Contestant" or "Nomination pending"
    ↓ 404: "User not found"
    ↓ 500: "Server error"
    ↓ 101: "No internet connection"
    
💾 Data Available After Login:
    ↓ Throughout app, access via:
    ↓ userDetailslist = userDetailsDatabase.GetUserDetails().ToList()
    ↓ AUTO_ID = userDetailslist[0].AUTO_ID           // "12345"
    ↓ WARD_CODE = userDetailslist[0].CONSTITUENCY_CODE // "1309001001"
    ↓ LIMIT = userDetailslist[0].LimitAmt            // "500000"
    ↓ STATUS = userDetailslist[0].ExpStatus          // "N", "P", "F"


┌─────────────────────────────────────────────────────────────────┐
│                 CANDIDATE EXPENSE ENTRY FLOW                   │
└─────────────────────────────────────────────────────────────────┘

📱 DashboardPage.xaml.cs - OnAppearing()
    ↓ Load reference data
    
🌐 API Call: ExpenseSources_Get()
    ↓ URL: baseurl + "api/ExpenseSource"
    ↓ Controller: ExpenseSourceController.cs
    
🗄️  Stored Procedure: sec.getExpenseSource
    ↓ Returns: Expense types (Transport, Food, etc.)
    
🌐 API Call: PaymentMode_Get()
    ↓ URL: baseurl + "api/PaymentMode"
    ↓ Controller: PaymentModeController.cs
    
🗄️  Stored Procedure: sec.Mobile_getPaymentModes
    ↓ Returns: Payment modes (Cash, Cheque, Online)
    
📱 User clicks "Add Expenses" → AddExpenditureDetailsPage.xaml
    ↓ User fills form and clicks Save
    ↓ btn_save_Clicked()


┌─────────────────────────────────────────────────────────────────┐
│                    SAVE EXPENDITURE FLOW                       │
└─────────────────────────────────────────────────────────────────┘

📱 HitServices.SaveExpenditure()
    ↓ Creates HTTP POST request
    
🌐 API Endpoint: SaveExpenditureDetails.aspx
    ↓ URL: baseurl + "SaveExpenditureDetails.aspx"
    ↓ Method: POST with form data
    
🗄️  Stored Procedure: sec.Mobile_saveData
    ↓ Parameters: @AutoID, @expDate, @expCode, @amount, etc.
    
🔍 Logic in Stored Procedure:
    ↓ 1. Get candidate's panchayat code
    ↓ 2. Check for duplicate entries
    ↓ 3. Insert into candidateRegister
    ↓ 4. Save evidence file if provided


    