
# Firebase Firestore Dummy Data for HoneyTrap AI Manager

This document outlines the structure and provides sample dummy data for the Firestore database used by the HoneyTrap AI Manager application.

## Data Structure and Sample Records

### 1. Users Collection (`users`)

Stores information about application users.

**Structure:**

```json
{
  "uid": "string (Firebase UID)",
  "name": "string",
  "email": "string",
  "role": "string ('Admin', 'Analyst', 'Viewer')",
  "profile_photo_url": "string (URL)",
  "created_at": "timestamp"
}
```

**Sample Records:**

*   **User 1 (Admin):**
    ```json
    {
      "uid": "adminUser123",
      "name": "Alice Johnson",
      "email": "alice.j@securecorp.com",
      "role": "Admin",
      "profile_photo_url": "https://picsum.photos/seed/alice/100/100",
      "created_at": "Timestamp(seconds=1678886400, nanoseconds=0)" // March 15, 2023
    }
    ```
*   **User 2 (Analyst):**
    ```json
    {
      "uid": "analystUser456",
      "name": "Bob Williams",
      "email": "bob.w@securecorp.com",
      "role": "Analyst",
      "profile_photo_url": "https://picsum.photos/seed/bob/100/100",
      "created_at": "Timestamp(seconds=1678972800, nanoseconds=0)" // March 16, 2023
    }
    ```
*   **User 3 (Analyst):**
    ```json
    {
      "uid": "analystUser789",
      "name": "Charlie Davis",
      "email": "charlie.d@securecorp.com",
      "role": "Analyst",
      "profile_photo_url": "https://picsum.photos/seed/charlie/100/100",
      "created_at": "Timestamp(seconds=1679059200, nanoseconds=0)" // March 17, 2023
    }
    ```
*   **User 4 (Viewer):**
    ```json
    {
      "uid": "viewerUser101",
      "name": "Diana Miller",
      "email": "diana.m@securecorp.com",
      "role": "Viewer",
      "profile_photo_url": "https://picsum.photos/seed/diana/100/100",
      "created_at": "Timestamp(seconds=1679145600, nanoseconds=0)" // March 18, 2023
    }
    ```
*   **User 5 (Supervisor - Assuming this maps to Admin or a specific role):**
    ```json
    {
      "uid": "supervisorUser112",
      "name": "Ethan Garcia",
      "email": "ethan.g@securecorp.com",
      "role": "Admin", // Or a dedicated 'Supervisor' role if added
      "profile_photo_url": "https://picsum.photos/seed/ethan/100/100",
      "created_at": "Timestamp(seconds=1679232000, nanoseconds=0)" // March 19, 2023
    }
    ```

---

### 2. Cases Collection (`cases`)

Stores details about each social engineering test case.

**Structure:**

```json
{
  "case_id": "string (auto-ID)",
  "created_by": "reference (to users/uid)",
  "title": "string",
  "status": "string ('Active', 'Resolved', 'Escalated')",
  "category": "string ('Phishing', 'Baiting', 'Pretexting', 'Tailgating', 'Quid Pro Quo')",
  "created_at": "timestamp",
  "summary": "string",
  "evidence": "array<string> (URLs to Firebase Storage)"
}
```

**Sample Records:**

*   **Case 1:**
    ```json
    {
      "case_id": "caseXYZ789",
      "created_by": "users/analystUser456",
      "title": "LinkedIn Credential Phishing Attempt",
      "status": "Active",
      "category": "Phishing",
      "created_at": "Timestamp(seconds=1679318400, nanoseconds=0)", // March 20, 2023
      "summary": "Simulating a fake LinkedIn login page request sent via email to target employees.",
      "evidence": [
        "gs://honeytrap-ai-manager.appspot.com/evidence/caseXYZ789/screenshot1.png",
        "gs://honeytrap-ai-manager.appspot.com/evidence/caseXYZ789/email_log.txt"
      ]
    }
    ```
*   **Case 2:**
    ```json
    {
      "case_id": "caseABC123",
      "created_by": "users/analystUser789",
      "title": "USB Drive Baiting (Parking Lot)",
      "status": "Resolved",
      "category": "Baiting",
      "created_at": "Timestamp(seconds=1679404800, nanoseconds=0)", // March 21, 2023
      "summary": "Left branded USB drives in the company parking lot. Monitoring network for connections.",
      "evidence": [
        "gs://honeytrap-ai-manager.appspot.com/evidence/caseABC123/drive_photo.jpg"
      ]
    }
    ```
*   **Case 3:**
    ```json
    {
      "case_id": "casePQR456",
      "created_by": "users/analystUser456",
      "title": "IT Support Pretexting Call",
      "status": "Escalated",
      "category": "Pretexting",
      "created_at": "Timestamp(seconds=1679491200, nanoseconds=0)", // March 22, 2023
      "summary": "Analyst called target pretending to be IT support, attempting to gain remote access credentials.",
      "evidence": [
        "gs://honeytrap-ai-manager.appspot.com/evidence/casePQR456/call_recording.mp3",
        "gs://honeytrap-ai-manager.appspot.com/evidence/casePQR456/notes.txt"
      ]
    }
    ```
*   **Case 4:**
    ```json
    {
      "case_id": "caseLMN001",
      "created_by": "users/analystUser789",
      "title": "Targeted Spear Phishing (Finance Dept)",
      "status": "Active",
      "category": "Phishing",
      "created_at": "Timestamp(seconds=1679577600, nanoseconds=0)", // March 23, 2023
      "summary": "Highly targeted email appearing to be from CFO requesting urgent wire transfer.",
      "evidence": []
    }
    ```

---

### 3. Interactions Subcollection (`cases/{case_id}/interactions`)

Logs messages and actions within a specific case.

**Structure:**

```json
{
  "message_id": "string (auto-ID)",
  "sender": "string ('Attacker', 'Victim', 'Analyst', 'AI Assistant')",
  "timestamp": "timestamp",
  "content": "string",
  "risk_score": "number (0-100, optional)",
  "ai_analysis": "string (optional, summary from AI)"
}
```

**Sample Records (under `cases/caseXYZ789`):**

*   **Interaction 1:**
    ```json
    {
      "message_id": "msg1",
      "sender": "Attacker", // Simulated email sent
      "timestamp": "Timestamp(seconds=1679318460, nanoseconds=0)",
      "content": "Subject: Important: Update Your LinkedIn Profile Now! Click here: [fake_link]",
      "risk_score": 75,
      "ai_analysis": "Detected phishing attempt with urgency and suspicious link."
    }
    ```
*   **Interaction 2:**
    ```json
    {
      "message_id": "msg2",
      "sender": "Victim", // Simulated employee response (or lack thereof)
      "timestamp": "Timestamp(seconds=1679322000, nanoseconds=0)",
      "content": "(No response recorded, user did not click)"
    }
    ```
*   **Interaction 3 (under `cases/casePQR456`):**
    ```json
    {
      "message_id": "msg3",
      "sender": "Analyst", // Analyst acting as attacker
      "timestamp": "Timestamp(seconds=1679491320, nanoseconds=0)",
      "content": "Hi, this is John from IT. We've detected unusual activity on your account. Can you confirm your username and temporary password I just sent you?",
      "risk_score": 85,
      "ai_analysis": "Pretexting call using authority (IT) and fabricated urgency to elicit credentials."
    }
    ```
*   **Interaction 4 (under `cases/casePQR456`):**
    ```json
    {
      "message_id": "msg4",
      "sender": "Victim",
      "timestamp": "Timestamp(seconds=1679491380, nanoseconds=0)",
      "content": "Oh, okay. My username is 'targetUser', and the password was 'TempPass123!'. Is everything alright?",
      "risk_score": 95,
      "ai_analysis": "Victim disclosed credentials. High risk of account compromise."
    }
    ```
*   **Interaction 5 (under `cases/casePQR456`):**
    ```json
    {
      "message_id": "msg5",
      "sender": "Analyst",
      "timestamp": "Timestamp(seconds=1679491440, nanoseconds=0)",
      "content": "Thanks! Yes, just performing routine checks. We'll monitor it. Have a good day. (Test concluded)",
      "risk_score": 0
    }
    ```

---

### 4. AI Suggestions Collection (`ai_suggestions`)

Stores recommendations generated by the AI based on case interactions.

**Structure:**

```json
{
  "suggestion_id": "string (auto-ID)",
  "related_case": "reference (to cases/case_id)",
  "generated_at": "timestamp",
  "recommendation": "string",
  "confidence_level": "number (0.0 - 1.0)",
  "source": "string ('Gemini', 'PaLM 2', etc.)"
}
```

**Sample Records:**

*   **Suggestion 1 (for `caseXYZ789`):**
    ```json
    {
      "suggestion_id": "sug1",
      "related_case": "cases/caseXYZ789",
      "generated_at": "Timestamp(seconds=1679318520, nanoseconds=0)",
      "recommendation": "Initial interaction shows typical phishing characteristics. Monitor click-through rates. Consider sending a follow-up awareness reminder if clicks are high.",
      "confidence_level": 0.85,
      "source": "Gemini"
    }
    ```
*   **Suggestion 2 (for `caseXYZ789`):**
    ```json
    {
      "suggestion_id": "sug2",
      "related_case": "cases/caseXYZ789",
      "generated_at": "Timestamp(seconds=1679322120, nanoseconds=0)",
      "recommendation": "Target did not interact with the phishing link. Suggest classifying as 'Aware' for this test cycle.",
      "confidence_level": 0.90,
      "source": "Gemini"
    }
    ```
*   **Suggestion 3 (for `casePQR456`):**
    ```json
    {
      "suggestion_id": "sug3",
      "related_case": "cases/casePQR456",
      "generated_at": "Timestamp(seconds=1679491400, nanoseconds=0)",
      "recommendation": "High-risk credential disclosure detected. Recommend immediate escalation to the security team and mandatory retraining for the target user.",
      "confidence_level": 0.98,
      "source": "PaLM 2"
    }
    ```
*   **Suggestion 4 (for `casePQR456`):**
    ```json
    {
      "suggestion_id": "sug4",
      "related_case": "cases/casePQR456",
      "generated_at": "Timestamp(seconds=1679491500, nanoseconds=0)",
      "recommendation": "Analyze call recording for specific social engineering techniques used (e.g., authority, urgency, scarcity) to refine future training.",
      "confidence_level": 0.75,
      "source": "Gemini"
    }
    ```
*   **Suggestion 5 (for `caseLMN001`):**
    ```json
    {
      "suggestion_id": "sug5",
      "related_case": "cases/caseLMN001",
      "generated_at": "Timestamp(seconds=1679577700, nanoseconds=0)",
      "recommendation": "Spear phishing targeting finance requires close monitoring. Alert finance team leadership about the ongoing simulation.",
      "confidence_level": 0.88,
      "source": "Gemini"
    }
    ```

---

### 5. Settings Collection (`settings`)

Stores user-specific application settings.

**Structure:**

```json
{
  "user_id": "reference (to users/uid, document ID should match user UID for easy lookup)",
  "theme": "string ('light', 'dark')",
  "notifications_enabled": "boolean"
}
```

**Sample Records:**

*   **Settings for User 1 (`adminUser123`):**
    ```json
    // Document ID: adminUser123
    {
      "user_id": "users/adminUser123",
      "theme": "dark",
      "notifications_enabled": true
    }
    ```
*   **Settings for User 2 (`analystUser456`):**
    ```json
    // Document ID: analystUser456
    {
      "user_id": "users/analystUser456",
      "theme": "light",
      "notifications_enabled": true
    }
    ```
*   **Settings for User 4 (`viewerUser101`):**
    ```json
    // Document ID: viewerUser101
    {
      "user_id": "users/viewerUser101",
      "theme": "light",
      "notifications_enabled": false
    }
    ```

---

*Note: Timestamps are illustrative. Replace with actual Firebase Timestamp objects during implementation. References should be Firestore DocumentReference objects.*
