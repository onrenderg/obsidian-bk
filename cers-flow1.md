┌─────────────────────────────────────────────────────────────────┐
│                    OBSERVER LOGIN FLOW                         │
└─────────────────────────────────────────────────────────────────┘

📱 LoginPage.xaml.cs
    ↓ User enters mobile number
    ↓ btn_getotp_Clicked()
    
🌐 API Call: CheckUserType_Get()
    ↓ URL: baseurl + "api/CheckUserType?MobileNo={encrypted_mobile}"
    ↓ Returns: UserType = "Observor"
    
🌐 API Call: observorlogin_Get()
    ↓ URL: baseurl + "api/ObservorLogin?MobileNo={encrypted_mobile}"
    ↓ Controller: ObservorLoginController.cs
    
🗄️  Stored Procedure: sec.Mobile_CERS_ObservorLogin
    ↓ Query: SELECT * FROM secExpense.sec.ObserverInfo 
    ↓        WHERE ObserverContact = @MobileNo
    
📱 After OTP verification → ObserverDashboardPage.xaml
    ↓ OnAppearing() loads observer wards


┌─────────────────────────────────────────────────────────────────┐
│                  OBSERVER WARDS LOADING FLOW                   │
└─────────────────────────────────────────────────────────────────┘

📱 ObserverDashboardPage.xaml.cs - Constructor
    ↓ Loads observer login details
    ↓ Loads observer wards from local database
    
🌐 API Call: ObserverWards_Get() (called during login)
    ↓ URL: baseurl + "api/ObserverWards?MobileNo={encrypted_mobile}"
    ↓ Controller: ObserverWardsController.cs
    
🗄️  Stored Procedure: sec.Mobile_getobserver_wards
    ↓ Query: SELECT Panchayat_Code, Panchayat_Name, Panchayat_Name_Local
    ↓        FROM [Observer Ward Mapping Table]
    ↓        WHERE ObserverContact = @MobileNo
    
📱 Local Storage: ObserverWardsDatabase.AddObserverWards()
    ↓ Populates picker_wards dropdown



┌─────────────────────────────────────────────────────────────────┐
│                OBSERVER WARD SELECTION FLOW                    │
└─────────────────────────────────────────────────────────────────┘

📱 ObserverDashboardPage.xaml.cs
    ↓ picker_wards_SelectedIndexChanged()
    ↓ Gets selected ward's Panchayat_Code
    
🌐 API Call: ObserverCandidates_Get()
    ↓ URL: baseurl + "api/ObserverCandidates?PanchWardCode={encrypted_code}"
    ↓ Controller: ObserverCandidatesController.cs
    
🗄️  Stored Procedure: sec.Mobile_getobserver_candidates
    ↓ Parameters: @PanchWardCode (e.g., '1309001001')
    ↓ Query: SELECT i.AUTO_ID, i.VOTER_NAME, SUM(c.amount) Amount
    ↓        FROM sec.CandidatePersonalInfo i
    ↓        LEFT JOIN sec.candidateRegister c ON c.AutoID = i.AUTO_ID
    ↓        WHERE CONSTITUENCY_CODE = @PanchWardCode
    ↓        AND c.ExpStatus = 'F'
    
📱 Local Storage: ObserverCandidatesDatabase.AddObserverCandidates()
    ↓ Displays candidates in listView_candidatedetails


┌─────────────────────────────────────────────────────────────────┐
│              OBSERVER CANDIDATE DETAILS FLOW                   │
└─────────────────────────────────────────────────────────────────┘

📱 ObserverDashboardPage.xaml.cs
    ↓ listView_candidatedetails_ItemTapped()
    ↓ Gets selected candidate's AUTO_ID
    
🌐 API Call: ObserverExpenditureDetails_Get()
    ↓ URL: baseurl + "api/ExpenditureDetailsObserver?AutoID={encrypted_id}"
    ↓ Controller: ExpenditureDetailsObserverController.cs
    
🗄️  Stored Procedure: sec.Mobile_getsaveData_observer
    ↓ Parameters: @AutoID (e.g., '12345')
    ↓ Query: SELECT * FROM sec.candidateRegister
    ↓        WHERE AutoID = @AutoID AND ExpStatus = 'F'
    
📱 Navigation: ExpenditureDateTypewiselistPage.xaml
    ↓ Shows detailed expenditure list for selected candidate
    ↓ Observer can add remarks and review expenses


┌─────────────────────────────────────────────────────────────────┐
│                    CANDIDATE COMPLETE FLOW                     │
└─────────────────────────────────────────────────────────────────┘

📱 LoginPage.xaml.cs
    ↓ btn_getotp_Clicked(mobile: "9876543210")
    
🌐 HitServices.CheckUserType_Get("9876543210")
    ↓ POST: baseurl + "api/CheckUserType?MobileNo=encrypted_mobile"
    ↓ Controller: CheckUserTypeController.cs
    
🗄️  EXEC sec.Mobile_getusertype @MobileNo='9876543210'
    ↓ RETURNS: UserType = "Candidate"
    ↓ Preferences.Set("UserType", "Candidate")
    
🌐 HitServices.userlogin_Get("9876543210")
    ↓ GET: baseurl + "api/UserLogin?MobileNo=encrypted_mobile"
    ↓ Controller: UserLoginController.cs
    
🗄️  EXEC sec.Mobile_CERS_AppLogin @MobileNo='9876543210'
    ↓ SELECT AUTO_ID=12345, CONSTITUENCY_CODE='1309001001', VOTER_NAME='John Doe'
    ↓ FROM sec.CandidatePersonalInfo WHERE MOBILE_NUMBER='9876543210'
    
📱 UserDetailsDatabase.AddUserDetails()
    ↓ LOCAL STORAGE: AutoID=12345, CONSTITUENCY_CODE=1309001001
    
🌐 HitServices.GetOtp("9876543210") → OTP Verification → Dashboard
    
📱 DashboardPage.xaml.cs - OnAppearing()
    
🌐 HitServices.ExpenseSources_Get()
    ↓ GET: baseurl + "api/ExpenseSource"
    
🗄️  EXEC sec.getExpenseSource
    ↓ RETURNS: Transport, Food, Accommodation, etc.
    
🌐 HitServices.PaymentMode_Get()
    ↓ GET: baseurl + "api/PaymentMode"
    
🗄️  EXEC sec.Mobile_getPaymentModes
    ↓ RETURNS: Cash, Cheque, Online Transfer
    
📱 User clicks "Add Expenses" → AddExpenditureDetailsPage.xaml
    ↓ User fills: Date=2024-01-15, Type=Transport, Amount=5000
    ↓ btn_save_Clicked()
    
🌐 HitServices.SaveExpenditure(AutoID=12345, expDate="2024-01-15", 
                               expCode="001", amount="5000", ...)
    ↓ POST: baseurl + "SaveExpenditureDetails.aspx"
    ↓ ASPX Page: SaveExpenditureDetails.aspx.cs
    
🗄️  EXEC sec.Mobile_saveData 
    ↓     @AutoID=12345, @expDate='2024-01-15', @expCode='001', @amount=5000
    
    BEGIN TRANSACTION
    
    -- Get candidate's ward
    DECLARE @candidatepanchayat char(10)
    SET @candidatepanchayat = (
        SELECT PANCHAYAT_CODE FROM sec.CandidatePersonalInfo 
        WHERE AUTO_ID = 12345
    )  -- Returns: '1309001001'
    
    -- Insert expenditure
    INSERT INTO sec.candidateRegister (
        AutoID,         -- 12345
        expDate,        -- 2024-01-15
        expCode,        -- 001 (Transport)
        amount,         -- 5000
        PanchayatCode,  -- 1309001001 (Ward from candidate profile)
        ExpStatus       -- 'P' (Pending)
    )
    
    COMMIT
    ↓ RETURNS: 200, "Successfully Saved"
    
📱 Navigate back to DashboardPage.xaml



┌─────────────────────────────────────────────────────────────────┐
│                    OBSERVER COMPLETE FLOW                      │
└─────────────────────────────────────────────────────────────────┘

📱 LoginPage.xaml.cs
    ↓ btn_getotp_Clicked(mobile: "9123456789")
    
🌐 HitServices.CheckUserType_Get("9123456789")
    ↓ POST: baseurl + "api/CheckUserType?MobileNo=encrypted_mobile"
    
🗄️  EXEC sec.Mobile_getusertype @MobileNo='9123456789'
    ↓ RETURNS: UserType = "Observor"
    ↓ Preferences.Set("UserType", "Observor")
    
🌐 HitServices.observorlogin_Get("9123456789")
    ↓ GET: baseurl + "api/ObservorLogin?MobileNo=encrypted_mobile"
    ↓ Controller: ObservorLoginController.cs
    
🗄️  EXEC sec.Mobile_CERS_ObservorLogin @MobileNo='9123456789'
    ↓ SELECT ObserverName='Jane Smith', ObserverDesignation='District Observer'
    ↓ FROM secExpense.sec.ObserverInfo WHERE ObserverContact='9123456789'
    
📱 ObservorLoginDetailsDatabase.AddObservorLoginDetails()
    ↓ LOCAL STORAGE: Observer details
    
🌐 HitServices.GetOtp("9123456789") → OTP Verification
    
🌐 HitServices.ObserverWards_Get("9123456789")
    ↓ GET: baseurl + "api/ObserverWards?MobileNo=encrypted_mobile"
    ↓ Controller: ObserverWardsController.cs
    
🗄️  EXEC sec.Mobile_getobserver_wards @MobileNo='9123456789'
    ↓ SELECT Panchayat_Code, Panchayat_Name, Panchayat_Name_Local
    ↓ FROM [Observer Ward Mapping] WHERE ObserverContact='9123456789'
    ↓ RETURNS: 
    ↓   - Panchayat_Code='1309001001', Panchayat_Name='Ward 1'
    ↓   - Panchayat_Code='1309001002', Panchayat_Name='Ward 2'
    
📱 ObserverWardsDatabase.AddObserverWards()
    ↓ LOCAL STORAGE: Available wards for observer
    ↓ Navigate to ObserverDashboardPage.xaml
    
📱 ObserverDashboardPage.xaml.cs - Constructor
    ↓ picker_wards populated with: Ward 1, Ward 2
    ↓ picker_wards.SelectedIndex = 0 (Auto-select Ward 1)
    
📱 picker_wards_SelectedIndexChanged() - User selects "Ward 1"
    ↓ panchayatcode = "1309001001"
    
🌐 HitServices.ObserverCandidates_Get("1309001001")
    ↓ GET: baseurl + "api/ObserverCandidates?PanchWardCode=encrypted_code"
    ↓ Controller: ObserverCandidatesController.cs
    
🗄️  EXEC sec.Mobile_getobserver_candidates @PanchWardCode='1309001001'
    
    SELECT 
        i.AUTO_ID,              -- 12345
        i.VOTER_NAME,           -- 'John Doe'
        ISNULL(CONVERT(VARCHAR(50), SUM(c.amount)), 'No Info.') Amount  -- '5000'
    FROM sec.CandidatePersonalInfo i
    LEFT JOIN secExpense.sec.candidateRegister c 
        ON c.AutoID = i.AUTO_ID 
        AND c.ExpStatus = 'F'   -- Only finalized expenses visible
    WHERE 
        NOMINATION_STATUS = 'l'           -- Valid candidates
        AND CONSTITUENCY_CODE = '1309001001'  -- Selected ward
    GROUP BY i.AUTO_ID, i.VOTER_NAME
    
    ↓ RETURNS: 
    ↓   - AUTO_ID=12345, VOTER_NAME='John Doe', Amount='5000'
    ↓   - AUTO_ID=12346, VOTER_NAME='Jane Doe', Amount='3000'
    
📱 ObserverCandidatesDatabase.AddObserverCandidates()
    ↓ LOCAL STORAGE: Candidates in selected ward
    ↓ listView_candidatedetails populated with candidates
    
📱 listView_candidatedetails_ItemTapped() - User taps "John Doe"
    ↓ autoid = "12345"
    
🌐 HitServices.ObserverExpenditureDetails_Get("12345")
    ↓ GET: baseurl + "api/ExpenditureDetailsObserver?AutoID=encrypted_id"
    ↓ Controller: ExpenditureDetailsObserverController.cs
    
🗄️  EXEC sec.Mobile_getsaveData_observer @AutoID=12345
    
    SELECT 
        ExpenseID, AutoID, expDate, expCode, amount, payeeName,
        voucherBillNumber, remarks, ObserverRemarks, ExpStatus
    FROM secExpense.sec.candidateRegister 
    WHERE AutoID = 12345 AND ExpStatus = 'F'  -- Only finalized expenses
    ORDER BY expDate DESC
    
    ↓ RETURNS: Detailed expenditure list for John Doe
    ↓   - ExpenseID=1001, expDate='2024-01-15', amount=5000, ExpStatus='F'
    ↓   - ExpenseID=1002, expDate='2024-01-16', amount=2000, ExpStatus='F'
    
📱 ObserverExpenditureDetailsDatabase.AddObserverExpenditureDetails()
    ↓ LOCAL STORAGE: Candidate's expenditure details
    ↓ Navigate to ExpenditureDateTypewiselistPage.xaml
    ↓ Observer can review expenses and add remarks



