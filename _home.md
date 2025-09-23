



## BaseApp

[[_baseapp]]



## CERS

[[_cers]]
# NicVc


[[_nicvc]]





## tsql

[[_tsql_base1]]

### tsql logic isolation

[[_tsql_logic_isolation]]

## **Visual Flow Diagram**

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