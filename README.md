# 🎓 Student Support Ticket Router (Laya AI)

A smart, lightweight AI capability that reads student support tickets, decides **which campus department** should handle them, and calculates their **urgency level**.

Built using the open-weight **Laya** decision model (`convaiinnovations/laya`) for **Assignment A6 (Week 08: Platform Development)**.

---

## 💡 What is this? (Decision Model vs. Chatbot)

> **Important:** This is a **decision capability**, not a chatbot like ChatGPT.  
> It does not chat with students or write essay replies. Instead, it works behind the scenes like an automated switchboard: it reads a student's problem and instantly routes it to the right department with a priority rating.

---

## ⚡ Quick Start (2 Steps)

### Step 1: Install Requirements
Open PowerShell or your terminal and run:

```bash
pip install laya torch transformers pydantic
```

*(On the very first run, it will automatically download the free Laya model weights to your computer. After that, it works completely offline.)*

### Step 2: Run the Program
Navigate to this folder:
```bash
cd "C:\Users\ADMIN\Desktop\Lab8_Assignment"
```

---

## 🚀 How to Use It

You have **two simple ways** to use this program:

### Option 1: Test Your Own Custom Tickets (Interactive Mode) 🌟

If you want to type your own questions and see how the AI classifies them live, run:

```bash
python ticket_router.py -i
```
*(or `python ticket_router.py --interactive`)*

The program will prompt you:
1. **Enter Ticket Subject:** (e.g. `I lost my dorm keycard`)
2. **Enter Ticket Body:** (e.g. `I am locked out of my room in Hall B and my roommate is away`)
3. **Enter Student Year:** (e.g. `Freshman`)

**What you will see:**
```text
-------------------------------------------------------
  Department:   STUDENT_HOUSING (46.6% confidence)
  Urgency:      P2_URGENT (43.9% confidence)
  Method:       Laya-Model (2568 ms)
  Probabilities:
    STUDENT_HOUSING   :  46.6%  █████████
    ACADEMIC_ADVISING :  21.4%  ████
    FINANCIAL_AID     :  12.7%  ██
    IT_HELPDESK       :  10.3%  ██
    REGISTRAR_RECORDS :   9.1%  █
-------------------------------------------------------
```
*(Type `exit` or `quit` whenever you want to stop.)*

---

### Option 2: Run the Official Assignment Tests (Automated Mode)

To run the 5 official test cases required for your course assignment and update the grading results file:

```bash
python ticket_router.py --test
```

This runs:
- **Test 1:** Blackboard login issue before midterm exam ➔ `IT_HELPDESK` (`P1_CRITICAL`)
- **Test 2:** Prerequisite override for CS 301 ➔ `ACADEMIC_ADVISING` (`P2_URGENT`)
- **Test 3:** FAFSA financial aid disbursement delay ➔ `FINANCIAL_AID` (`P3_STANDARD`)
- **Test 4:** Official sealed transcript for graduate school ➔ `REGISTRAR_RECORDS` (`P2_URGENT`)
- **Test 5:** Dormitory roommate conflict in Evergreen Hall ➔ `STUDENT_HOUSING` (`P2_URGENT`)
- **Fallback Test:** Simulates network outage to show instant backup rule execution (0.48 ms).

It automatically saves all outputs to `test_results.json`.

---

## 🏢 The 5 Departments It Routes To

| Department | Handles Inquiries About |
|---|---|
| **`IT_HELPDESK`** | Blackboard/Canvas LMS, campus Wi-Fi, login errors, password resets. |
| **`ACADEMIC_ADVISING`** | Course prerequisites, adding/dropping classes, major declarations. |
| **`FINANCIAL_AID`** | Scholarships, tuition billing, FAFSA, student loans, payment delays. |
| **`REGISTRAR_RECORDS`** | Official transcripts, diplomas, enrollment verification letters. |
| **`STUDENT_HOUSING`** | Dorm room assignments, roommate conflicts, room transfer requests. |

---

## ⏱️ The 4 Urgency Priority Levels

* **`P1_CRITICAL`** ➔ Immediate emergency or exam/system lockout today.
* **`P2_URGENT`** ➔ Action needed within 24–48 hours (e.g. deadline tomorrow).
* **`P3_STANDARD`** ➔ Standard routine inquiry (2–3 business day response).
* **`P4_LOW`** ➔ General question or low priority request.

---

## 🛡️ Safety Fallback (What if the AI fails?)

If the model ever takes too long, crashes, or gets an ambiguous input like *"Help"*:
- It instantly switches to a **deterministic backup rule** in **0.48 milliseconds**.
- If confidence is too low (< 40%), it routes the ticket to **`GENERAL_TRIAGE`** so a human staff member can review it, ensuring no student ticket is ever lost or misrouted.

---

## 📂 Project Files Summary

* **`ticket_router.py`**: The main Python application (contains both the AI model and interactive mode).
* **`A6_6731503055.pdf`**: The completed 7-page assignment report ready for submission.
* **`test_results.json`**: Saved live output from the 5 test cases.
* **`A6_StudentSubmission.md`**: Markdown version of the submission report.
* **`A6_StudentSubmission.html`**: HTML version of the submission report.
* **`README.md`**: This guide.

---

**Student:** Hein Zaw (ID: 6731503055)  
**Course:** Platform Development — Week 08 Assignment A6
