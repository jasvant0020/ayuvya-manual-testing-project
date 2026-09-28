# Ayuvya Website — Manual Testing Project

Manual testing of the **Login / Authentication module** of the Ayuvya website, documented as test cases, a bug report, an execution summary and a full PDF report.

## Project Overview

| Item | Details |
| --- | --- |
| Website tested | https://ayuvya.com/login?next=menu |
| Module tested | Login / Authentication (mobile number + OTP login, logout, session behavior) |
| Testing type | Manual Testing |
| Browser | Chrome |
| Test date / submission date | 07/07/2026 |
| Candidate | Jasvant |

**Purpose / scope:** validate the login functionality of the application, covering phone number input validation, OTP generation and verification, OTP request limits, login and logout, session behavior, and the login API response as seen in the browser's Network tab. This was done as a QA interview assignment.

## Testing Scope

Categories used in the report:

- Functional Testing
- Validation Testing
- Negative Testing
- UI Testing
- API Testing

No automation testing was performed in this project.

## Test Execution Summary

The PDF report contains two sets of numbers that do not fully agree. Both are shown below and the original report has not been modified.

| Result | Reported in PDF summary | Count from PDF test case table |
| --- | ---: | ---: |
| Passed | 18 | 17 (includes TC014, "Pass (Bug Observed)") |
| Failed | 1 | 2 (TC011, TC019) |
| Blocked | 1 | 1 (TC015) |
| Not Executed | 0 | 0 |
| **Total** | **20** | **20** |

## Defect Summary

Severity counts match between the PDF summary and the bug list.

| Severity | Count |
| --- | ---: |
| Critical | 0 |
| High | 2 |
| Medium | 6 |
| Low | 3 |
| **Total** | **11** |

Status: 10 Open, 1 Needs Confirmation (BUG005).

## Key Areas Tested

- Login page load and UI elements
- Mobile number validation (empty, fewer than 10 digits, more than 10 digits, invalid starting digit, alphabetic and special characters)
- OTP generation, incorrect OTP, incomplete OTP
- Login with a valid OTP, and session persistence across refresh and a new tab
- Logout, browser Back behavior, and protected pages
- Page refresh on the OTP screen
- OTP validity after requesting a new OTP
- OTP request limit behavior
- Toast notification behavior on hover
- Rapid clicks on Generate OTP (blocked, see TC015)
- API behavior for OTP generation, request limit exceeded, and invalid input

## API Testing

Observed using Chrome Developer Tools → Network tab (TC018, TC019, TC020).

| Item | Details |
| --- | --- |
| Endpoint | `https://backend.ayuvya.com/api/user/login/` |
| Method | POST |
| Valid mobile number | HTTP 200 OK in about 796 ms. Body: `{"status":200, "message":"success", "data":"<encrypted_token>"}`. The OTP was not exposed in the response. (TC018, Pass) |
| OTP request limit exceeded | HTTP 200 OK, but the body contained `"status": 400` and `"message": "failed"`. Expected an HTTP error status such as 429. (TC019, Fail; BUG011) |
| Invalid mobile number (1234567890) | Client-side validation message shown; no API request appeared in the Network tab. (TC020, Pass) |

No tokens, OTPs or credentials are recorded in this repository.

## Defects Identified

11 defects were logged (BUG001 to BUG011). They fall into these groups:

- **OTP request limit handling:** user can reach the OTP screen while the limit is active but no OTP is sent (BUG007, High); generation requests and verification attempts share one limit counter (BUG010, High); reset time, remaining attempts and Resend OTP cooldown behavior are not communicated (BUG003, BUG004, BUG006).
- **OTP expiry:** no validity timer shown (BUG002); no specific expiry message observed (BUG005, Needs Confirmation).
- **API:** HTTP 200 returned for a failed OTP request (BUG011).
- **UI / content:** grammar in a validation message (BUG001); "welcome back" greeting for a first-time user (BUG008); cart count flickers after logout (BUG009).

Evidence links for BUG008 to BUG011 are given in the bug report (Google Drive links taken from the PDF). BUG001 to BUG007 are listed with no screenshot in the source.

## Repository Structure

```text
ayuvya-manual-testing-project/
├── README.md
├── Test-Cases/
│   └── Ayuvya_Login_Test_Cases.xlsx
├── Bug-Reports/
│   └── Ayuvya_Bug_Report.xlsx
├── Test-Report/
│   └── Ayuvya_Manual_Testing_Report.pdf
├── Test-Summary/
│   └── Test_Execution_Summary.xlsx
└── Screenshots/
    ├── README.md
    ├── login/
    ├── otp/
    ├── api/
    └── bugs/
```

## Tools Used

- Google Chrome
- Chrome Developer Tools (Network tab) for API inspection
- Microsoft Excel / spreadsheets for test case and bug documentation (the workbooks in this repo)

## Documentation

| What | Where |
| --- | --- |
| Test cases (TC001 to TC020) | `Test-Cases/Ayuvya_Login_Test_Cases.xlsx` |
| Bug reports (BUG001 to BUG011) | `Bug-Reports/Ayuvya_Bug_Report.xlsx` |
| Execution and defect summary, testing types, key findings | `Test-Summary/Test_Execution_Summary.xlsx` |
| Complete original report (unmodified) | `Test-Report/Ayuvya_Manual_Testing_Report.pdf` |
| Screenshots / evidence | `Screenshots/` (see its README) |

Fields that the original report does not contain (for example test case description, preconditions and priority) are marked `Not Available` in the workbooks.

## Disclaimer

This repository contains testing documentation for portfolio and educational purposes. It is not affiliated with or endorsed by Ayuvya. No passwords, OTP values, authentication tokens or other sensitive information should be added to this repository.
