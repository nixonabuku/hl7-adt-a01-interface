# HL7 ADT A01 Interface – Mirth Connect Project

This project demonstrates how to build a real-world **HL7 healthcare integration workflow** using **Mirth Connect (NextGen)**.  
It reads an **HL7 ADT^A01 (patient admission)** message, transforms the data into **JSON** using JavaScript, and saves it to a file directory — simulating how hospitals exchange patient data between systems.

---

## Table of Contents
- [Overview](#-overview)
- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Project Folder Structure](#-project-folder-structure)
- [HL7 Sample Message](#-hl7-sample-message)
- [Workflow & Screenshots](#-workflow--screenshots)
- [JSON Output Example](#-json-output-example)
- [How to Run This Project](#-how-to-run-this-project)
- [Future Enhancements](#-future-enhancements)
- [Author](#-author)

---

##  Overview

This interface performs the following actions:

✔ Reads `.txt` HL7 files from a local directory using a **File Reader**  
✔ Extracts key patient data (MSH, PID, PV1) in a **JavaScript Transformer**  
✔ Builds a structured JSON object from the HL7 message  
✔ Outputs the JSON file to a target folder with a timestamped filename  
✔ Fully tested and successfully running inside Mirth Connect

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| HL7 File Input | Reads ADT^A01 messages from a folder |
|  JavaScript Transformer | Parses PID, PV1 and MSH segments |
| HL7 → JSON Conversion | Converts clinical data to JSON format |
|  File Writer Output | Saves JSON to a folder using timestamp naming |
| Real HL7 Data Used | Message created using patient name “Nixon Abuku” |

---

##  Technology Stack

| Tool | Purpose |
|------|---------|
| **Mirth Connect (NextGen)** | Interface Engine |
| **HL7 v2.x** | Healthcare Messaging Standard |
| **JavaScript** | Transformation Logic |
| **JSON** | Output Data Format |
| **macOS** | Local Development Environment |

---

## 📁 Project Folder Structure

```
hl7-adt-a01-interface/
├── sample_hl7/
│   └── nixon_admit.txt
├── json_output/
│   └── 20251107_103955_NIXON_ABUKU.json
├── screenshots/
│   ├── 00_dashboard_overview.png
│   ├── 01_file_reader_source_settings.png
│   ├── 02_source_transformer_PID_extraction.png
│   ├── 03_to_json_transformer_script.png
│   ├── 04_channel_messages_raw_success.png
│   ├── 05_file_writer_destination_settings.png
│   ├── 06_json_output_preview_vscode.png
│   └── 07_github_repo_overview.png
└── README.md
```

---

## 🧪 HL7 Sample Message

```
MSH|^~\&|HOSPITAL_SYS|EAST_ORANGE_HOSPITAL|MIRTH_CONNECT|LOCAL|20251107103000||ADT^A01|MSG00001|P|2.5
EVN|A01|20251107103000
PID|1||NA0001||ABUKU^NIXON^MATARA||20000101|M|||123 MAIN ST^^EAST ORANGE^NJ^07017
PV1|1|I|ER^01^Room1|||||||||||ADM|A0|20251107103000
```

---

## 🖥 Workflow & Screenshots

###  Step 1 – Channel Running in Dashboard  
`![Dashboard](screenshots/00_dashboard_overview.png)`

###  Step 2 – File Reader Source Settings  
`![File Reader](screenshots/01_file_reader_source_settings.png)`

###  Step 3 – JavaScript Source Transformer (Extract MSH/PID/PV1)  
`![Source Transformer](screenshots/02_source_transformer_PID_extraction.png)`

###  Step 4 – JSON Builder Script  
`![JSON Script](screenshots/03_to_json_transformer_script.png)`

###  Step 5 – File Writer Output Settings  
`![File Writer](screenshots/05_file_writer_destination_settings.png)`

###  Step 6 – Successful Message Processed  
`![Success Message](screenshots/04_channel_messages_raw_success.png)`

###  Step 7 – JSON Output in VS Code  
`![JSON Output](screenshots/06_json_output_preview_vscode.png)`

---

## JSON Output Example

```json
{
  "meta": {
    "controlId": "MSG00001",
    "messageType": "ADT^A01",
    "version": "2.5",
    "receivedAt": "2025-11-07T15:39:55.093Z"
  },
  "sending": {
    "application": "HOSPITAL_SYS",
    "facility": "EAST_ORANGE_HOSPITAL"
  },
  "patient": {
    "name": {
      "last": "ABUKU",
      "first": "NIXON",
      "full": "NIXON ABUKU"
    },
    "mrn": "NA0001",
    "dob": "20000101",
    "gender": "M"
  },
  "visit": {
    "patientClass": "I",
    "location": "ER"
  }
}
```

---

## ⚙ How to Run This Project

###  1. Create Input & Output Directories
```
/Users/YourName/HL7_IN
/Users/YourName/HL7_PROCESSED
/Users/YourName/HL7_JSON
```
Place `nixon_admit.txt` inside `HL7_IN`.

---

###  2. Create Channel in Mirth Connect
- Source: **File Reader** → points to HL7_IN  
- Source Transformer: **JavaScript** (extract & JSON build)  
- Destination 1: **File Writer** → HL7_JSON  
- File Name Pattern:  
  ```
  ${date.get('yyyyMMdd_HHmmss')}_NIXON_ABUKU.json
  ```

---

###  3. Deploy & Test
- Deploy the channel  
- Drop HL7 file into HL7_IN  
- Check Dashboard → Messages → JSON Output Appears 

---

## 🚀 Future Enhancements

- Add support for ORU^R01 (Lab Results) or ORM^O01 (Orders)  
- Send JSON to REST API instead of file  
- Add error handling & validation of HL7 fields  
- Dockerize Mirth + folders automatically  

---

## 👤 Author

**Nixon Abuku**  
*HL7 & Mirth Connect Integration Developer*  
📌 GitHub: https://github.com/nixonabuku  
📌 LinkedIn: https://www.linkedin.com/in/nixon-abuku-020bb3332/

---


