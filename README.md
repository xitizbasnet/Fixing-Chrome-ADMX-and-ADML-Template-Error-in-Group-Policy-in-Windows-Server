# Fixing-Chrome-ADMX-and-ADML-Template-Error-in-Group-Policy-in-Windows-Server
---

# 🛠️ Fix: Chrome ADMX Template Error in Group Policy

A step-by-step guide to resolving the missing Chrome administrative template error in the **Group Policy Editor** on Windows systems.


## ❗ Problem Statement

When opening Group Policy Editor (`gpedit.msc`), the following error is displayed:


```

An appropriate resource file could not be found for file. C:\Windows\PolicyDefinitions\chrome.admx (error = 2): The system cannot find the file specified.

```

### Root Cause

This occurs when:

- `chrome.admx` is missing from the `PolicyDefinitions` folder.
- The corresponding `chrome.adml` file is missing from the system’s language folder (e.g., `en-US`).


### ✅ Resolution Steps


### Step 1: Download Chrome ADMX Templates

1. Navigate to the official Google Chrome Enterprise site:  
   👉 [https://chromeenterprise.google/policies/](https://chromeenterprise.google/policies/)
2. Download the **Google Chrome Enterprise Bundle** (.zip).
3. Extract the contents to a local directory.

   **Typical extracted structure: ADMX**
```

GoogleChromeEnterpriseBundle/
└── Configuration/
└── admx/
├── chrome.admx

```

   **Typical extracted structure: ADML**
```

GoogleChromeEnterpriseBundle/
└── Configuration/
└── en-US/
└── chrome.adml

```

---

### Step 2: Copy ADMX/ADML Files to Appropriate Locations

Choose based on your environment:

#### 🖥️ Local Group Policy (Single Machine)

| File           | Destination Folder                                |
|----------------|---------------------------------------------------|
| `chrome.admx`  | `C:\Windows\PolicyDefinitions\`                   |
| `chrome.adml`  | `C:\Windows\PolicyDefinitions\en-US\`             |

#### 🌐 Domain Group Policy (Active Directory Central Store)

| File           | Destination Folder                                                                 |
|----------------|--------------------------------------------------------------------------------------|
| `chrome.admx`  | `\\<xitiztechservices.local>\SYSVOL\xitiztechservices.local\Policies\PolicyDefinitions\`                            |
| `chrome.adml`  | `\\xitiztechservices.local\SYSVOL\xitiztechservices.local\Policies\PolicyDefinitions\en-US\`                      |

> 🔁 Replace `en-US` with your system locale if different.

---

### Step 3: Validate

1. Reopen **Group Policy Editor** (`gpedit.msc`) or **Group Policy Management Console**.
2. Navigate to:
```

Computer/User Configuration > Administrative Templates > Google > Google Chrome

````
3. Verify that the error is resolved and Chrome policies are visible.

---

## 🧪 Optional: Verify System Language

Run the following PowerShell command to check the system’s locale:

```powershell
Get-WinSystemLocale
````

Example output:

```
LCID             Name
----             ----
1033             en-US
```

→ This tells you the correct subfolder for `.adml` files (`en-US`, `en-GB`, etc.).

---

## 📌 Notes

* **Error Code 2** = File not found (either `.admx` or `.adml`)
* **Both files are required** for policy templates to function
* Always use the **central store** for domain-based GPO for consistency

---

## 📎 References

* [Chrome Enterprise Policy List](https://chromeenterprise.google/policies/)
* [Managing Chrome with Group Policy (Google Docs)](https://support.google.com/chrome/a/answer/187202)

---

## 🔒 Maintained By

**IT Department**
## 📧 [it@xitiztechservices.com](mailto:it@xitiztechservices.com)
## 🛠️ Last updated: June 26, 2025

---

> 📂 Contributions welcome. Fork the repo, make your changes, and submit a pull request.
