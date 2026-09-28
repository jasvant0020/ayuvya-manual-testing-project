# Screenshots / Evidence

No screenshots are stored in this folder yet. The original PDF report has no embedded images, so nothing could be extracted from it.

For four bugs the PDF gives Google Drive links as evidence (see the `Remarks` column in `Bug-Reports/Ayuvya_Bug_Report.xlsx`):

| Bug ID | Evidence link |
| --- | --- |
| BUG008 | https://drive.google.com/file/d/1UsWIYymHOcUm376wZe2PpAd39Hwez_Y3/view?usp=sharing |
| BUG009 | https://drive.google.com/file/d/1jcztzfC6Al3SYUKXp56bCqxkDCxIQ9zd/view?usp=sharing |
| BUG010 | https://drive.google.com/file/d/1GVUFHON5EYS0dm_oOYH6qmgFg90GTbCL/view?usp=sharing |
| BUG011 | https://drive.google.com/file/d/1gK8P24t5Peq_L3bxMRc3V1ieMmQy4RnD/view?usp=sharing |

## Suggested organization

Add only real screenshots taken during testing:

```text
Screenshots/
├── login/   # login page, phone number validation messages
├── otp/     # OTP screen, OTP errors, request limit message
├── api/     # Network tab requests and responses
└── bugs/    # evidence per bug, e.g. BUG008_hello-user-greeting.png
```

Naming suggestion: `<TestCaseID or BugID>_<short-description>.png`.

Before adding an image, check that it does not show a mobile number, OTP value, token, email or cookie/session data. Crop or blur it if it does.
