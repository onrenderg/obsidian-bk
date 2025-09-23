

Looking at the [loadexpdatewisedata()](cci:1://file:///c:/Users/Parth/Desktop/2025/sep11/CERS-basetwo-git/CERS-basetwo-git/CERS/DashboardPage.xaml.cs:195:8-234:9) method, the date-wise data comes from the **local SQLite database**, not from an API endpoint.

The date-wise data is **NOT** fetched from any API endpoint or stored procedure. It comes from the **local SQLite database**.

## **Data Source for Date-wise View:**

**Local Database Query** (lines 201-208):
```sql
Select * 
,expDateDisplay||' '||(case when ObserverRemarks <> '' then '#' else '' end) as displaytitle
,sum(amount)amount
,sum(amount)Totalamount
,'Date' as lblexptype
,'Amount' as lblAmount
from ExpenditureDetails 
group by expDate
```

**Database Table:** `ExpenditureDetails` (local SQLite)
**Method:** `expenditureDetailsDatabase.GetExpenditureDetails(query)`

## **How Data Gets Into Local Database:**

The expense data is initially populated from API calls, but the date-wise view reads from local storage:

1. **API Call:** [ExpenditureDetails_Get()](cci:1://file:///c:/Users/Parth/Desktop/2025/sep11/CERS-basetwo-git/CERS-basetwo-git/CERS/WebApi/HitServices.cs:731:8-809:9) in [HitServices.cs](cci:7://file:///c:/Users/Parth/Desktop/2025/sep11/CERS-basetwo-git/CERS-basetwo-git/CERS/WebApi/HitServices.cs:0:0-0:0) fetches data from server
2. **Local Storage:** Data is stored in local SQLite `ExpenditureDetails` table  
3. **Date-wise Display:** Groups local data by `expDate` field

So the date-wise view shows **locally stored expense data grouped by date**, not live API data.

















# Observer Flow to View Candidate Entries - Step by Step

## **Complete Observer Journey: Login → View Candidate Expenses**

### **Step 1: Observer Login**
```
📱 Observer opens CERS app
    ↓ Enters mobile number: "9123456789"
    ↓ Clicks "Get OTP"
    
🌐 API: CheckUserType → Returns "Observor"
🌐 API: observorlogin_Get → Validates observer credentials
🌐 API: GetOtp → Sends OTP to observer's phone
    
📱 Observer enters OTP received via SMS
    ↓ Clicks "Submit OTP"
    
🌐 API: checkotp_Get → Validates OTP
    ↓ If valid → Navigate to Observer Dashboard
```

### **Step 2: Load Observer's Assigned Wards**
```
📱 ObserverDashboardPage loads
    ↓ Shows observer info: Name, Designation, Contact
    
🌐 API: ObserverWards_Get(observer_mobile)
🗄️  Procedure: sec.Mobile_getobserver_wards
    ↓ Returns wards assigned to this observer:
    ↓ Ward 1: "1309001001" - "Shimla Ward 1"
    ↓ Ward 2: "1309001002" - "Shimla Ward 2"
    ↓ Ward 3: "1309001003" - "Shimla Ward 3"
    
📱 Ward dropdown populated with observer's assigned wards
```

### **Step 3: Observer Selects Ward**
```
📱 Observer clicks ward dropdown
    ↓ Selects "Shimla Ward 1" (code: 1309001001)
    ↓ picker_wards_SelectedIndexChanged() triggered
    
🌐 API: ObserverCandidates_Get("1309001001")
🗄️  Procedure: sec.Mobile_getobserver_candidates
    ↓ Query: SELECT candidates WHERE CONSTITUENCY_CODE = '1309001001'
    ↓ Returns candidates in selected ward:
    
    Candidate 1: AUTO_ID=12345, Name="John Doe", Total Amount="₹15,000"
    Candidate 2: AUTO_ID=12346, Name="Jane Smith", Total Amount="₹8,500"
    Candidate 3: AUTO_ID=12347, Name="Bob Wilson", Total Amount="No Info."
    
📱 Candidate list displayed with names and total expenses
```

### **Step 4: Observer Selects Specific Candidate**
```
📱 Observer taps on "John Doe" from candidate list
    ↓ listView_candidatedetails_ItemTapped() triggered
    ↓ Gets AUTO_ID = 12345
    
🌐 API: ObserverExpenditureDetails_Get("12345")
🗄️  Procedure: sec.Mobile_getsaveData_observer
    ↓ Query: SELECT * FROM candidateRegister 
    ↓        WHERE AutoID = 12345 AND ExpStatus = 'F'
    ↓ Returns John Doe's finalized expenses:
    
    Expense 1: Date=2024-01-15, Type=Transport, Amount=₹2,000, Payee="Fuel Station"
    Expense 2: Date=2024-01-16, Type=Food, Amount=₹5,000, Payee="Catering Service"
    Expense 3: Date=2024-01-17, Type=Advertising, Amount=₹8,000, Payee="Print Shop"
    
📱 Navigate to ExpenditureDateTypewiselistPage
    ↓ Shows detailed expense list for John Doe
```

### **Step 5: Observer Reviews Individual Expense**
```
📱 Observer sees detailed expense list
    ↓ Can tap on any expense to see full details
    ↓ Views: Date, Amount, Payment Mode, Vendor, Bill Number, Evidence File
    ↓ Can add observer remarks: "Verified - Receipt authentic"
    ↓ Can flag suspicious expenses for further investigation
```

## **Visual Flow Diagram**

```
Observer Login
    ↓
┌─────────────────────┐
│ Observer Dashboard  │
│ - Name: Jane Smith  │
│ - Role: Observer    │
│ - Wards: [Dropdown] │
└─────────────────────┘
    ↓ Select Ward
┌─────────────────────┐
│   Ward: Shimla 1    │
│ ┌─────────────────┐ │
│ │ John Doe  ₹15K  │ │ ← Candidate entries
│ │ Jane Smith ₹8K  │ │   made via mobile app
│ │ Bob Wilson  -   │ │
│ └─────────────────┘ │
└─────────────────────┘
    ↓ Tap John Doe
┌─────────────────────┐
│ John Doe's Expenses │
│ ┌─────────────────┐ │
│ │ 15-Jan Transport│ │ ← Individual expense
│ │ ₹2,000 Fuel     │ │   entries made by
│ │ 16-Jan Food     │ │   candidate
│ │ ₹5,000 Catering │ │
│ │ 17-Jan Ads      │ │
│ │ ₹8,000 Printing │ │
│ └─────────────────┘ │
└─────────────────────┘
```

## **Key Points**

### **What Observer Can See:**
- ✅ **Only Finalized Expenses** - ExpStatus = 'F' (submitted by candidate)
- ✅ **Only Their Assigned Wards** - Can't see other wards
- ✅ **All Candidates in Ward** - Complete transparency within their jurisdiction
- ✅ **Detailed Expense Info** - Date, amount, vendor, evidence files
- ✅ **Real-time Updates** - As candidates submit expenses

### **What Observer Cannot See:**
- ❌ **Draft Expenses** - ExpStatus = 'P' (candidate still working on)
- ❌ **Other Wards** - Only assigned wards visible
- ❌ **Personal Candidate Info** - Only expense-related data
- ❌ **Edit Expenses** - Read-only access, can only add remarks

### **Security & Data Flow:**
```
Candidate (Mobile: 9876543210) → Enters expense → Saves to DB
    ↓
Database: candidateRegister table
    ↓ AutoID=12345, PanchayatCode=1309001001, ExpStatus='F'
    ↓
Observer (Mobile: 9123456789) → Selects Ward 1309001001 → Sees candidate expenses
```

**In essence**: Observer login → Select assigned ward → View candidates in that ward → Drill down to see individual candidate's expense entries made through their mobile app.