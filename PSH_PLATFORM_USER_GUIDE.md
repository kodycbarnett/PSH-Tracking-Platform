# PSH Housing Application Tracker - User Guide

*For Claude Desktop instances with email + web automation*

## 🎯 **QUICK START**

**Platform URL**: http://localhost:5175/

**Purpose**: Track PSH (Permanent Supportive Housing) applications through an 11-stage process from unit availability to tenant move-in.

---

## 🏗️ **PLATFORM OVERVIEW**

### **What You're Looking At**
- **Left Panel**: Selected applicant details (when clicked)
- **Center**: Kanban board with 11 workflow stages
- **Right Panel**: Statistics dashboard + active action items

### **Key Numbers to Track**
- **Total Applicants**: 8 (in demo)
- **In Progress**: 7 
- **Need Appeals**: 1
- **Completed**: 0

---

## 📋 **THE 11-STAGE WORKFLOW**

| Stage | What We're Waiting For | Key Actions |
|-------|------------------------|-------------|
| 1️⃣ **Waiting for JOHS Referral** | Property manager notifies JOHS, gets referral | Notify JOHS, inspect unit |
| 2️⃣ **Waiting on Application Packet** | Case manager helps applicant complete forms | Call referring case manager, verify application |
| 3️⃣ **Waiting on Background Check** | Property manager runs background check | Send background check, alert when results received |
| 4️⃣ **Waiting on Appeal Documentation** | If background check fails, need appeal docs | Ensure case manager understands appeal process |
| 5️⃣ **Tax Credit Paperwork Appointment** | Schedule tax credit appointment | Schedule appointment, ensure applicant knows what to bring |
| 6️⃣ **Waiting for HF Intake Packet** | Home Forward processes intake | Property manager submits packet |
| 7️⃣ **HF Intake Packet Appointment** | Home Forward appointment scheduled | Coordinate with HF team |
| 8️⃣ **Waiting for Video Intake** | Video interview with Home Forward | Check on packet processing |
| 9️⃣ **Contract and Lease Signing Meeting** | Final paperwork and key handoff | Schedule signing, hand off keys |
| 🔟 **Wraparound Support Appointment** | Connect with ongoing support services | Welcome resident, schedule wraparound meeting |
| 1️⃣1️⃣ **Completed** | Process finished | Celebrate! 🎉 |

---

## 🎮 **HOW TO USE THE PLATFORM**

### **Viewing Applicant Details**
1. **Click any applicant card** to open left sidebar
2. **See complete profile**: Name, unit, phone, email, case manager info
3. **Check document status**: Green ✅ = collected, Red ❌ = missing
4. **Review process log**: Complete history of all actions

### **Managing Action Items** 
1. **Red ✗ = Pending action** - needs to be done
2. **Green ✓ = Completed** - click to toggle
3. **Auto-logging**: Checking items creates process log entries automatically

### **Stage Information**
1. **Click ℹ️ button** on any stage header
2. **See detailed info**: Description, duration, stakeholders, required actions, common delays, pro tips
3. **Access forms**: Required documents for each stage

### **Email Templates**
1. **Click applicant** → **Process Log** → **📧 Email button**
2. **Templates include**: New referral requests, document requests, status updates, appeal documentation
3. **Auto-filled variables**: {{applicantName}}, {{unit}}, {{caseManagerEmail}}, etc.
4. **One-click copy** to clipboard

### **🎯 Active Action Items Panel**
1. **Real-time monitoring** - Right sidebar shows urgent issues across all applicants
2. **Priority indicators**: 🔴 Urgent, 🟡 Warning, ℹ️ Info
3. **Clickable details** - Items marked "👆 Click for details" open detailed popups
4. **Smart alerts** - Automatically detects:
   - Appeals needed (urgent)
   - Missing documents (warning)
   - Pending action items (info)

### **📋 Detailed Action Items Popups**
1. **Click any action item** with "👆 Click for details" indicator
2. **Detailed popup appears** below the Kanban board showing:

#### **Missing Documentation View**
- **Per-client breakdown** with completion progress (e.g., "3/5 documents complete")
- **Specific missing items** with red ❌ indicators
- **Family member documents** included for household tracking
- **Visual organization** by applicant with avatars and unit numbers

#### **Pending Action Items View**
- **Client-separated sections** with current stage context
- **Role-based assignments** (e.g., "Property Manager: Contact JOHS")
- **Checkbox-style indicators** for each pending task
- **Count summaries** showing pending actions per client

3. **Close popup** using the × button in top-right corner

---

## 📧 **EMAIL-TO-ACTION WORKFLOW**

### **Common Email Scenarios & Platform Actions**

#### **📨 "Unit Available" Email**
→ **Action**: Click "✨ New Unit Available / New Applicant"
→ **Add**: Applicant name, unit number, case manager details

#### **📨 "JOHS Sent Referral" Email** 
→ **Find**: Applicant in "Waiting for JOHS Referral" stage
→ **Action**: Drag to "Waiting on Application Packet" stage
→ **Add note**: "Received JOHS referral for [applicant name]"

#### **📨 "Background Check Results" Email**
→ **Find**: Applicant in "Waiting on Background Check" stage
→ **If approved**: Drag to "Tax Credit Paperwork Appointment"
→ **If denied**: Drag to "Waiting on Appeal Documentation"
→ **Check action items**: Mark background check steps complete

#### **📨 "Documents Submitted" Email**
→ **Find**: Applicant in relevant stage
→ **Update documents**: Click applicant → check off received documents ✅
→ **Check action items**: Mark document-related tasks complete

#### **📨 "Appeal Successful" Email**
→ **Find**: Applicant in "Waiting on Appeal Documentation"
→ **Action**: Drag to "Tax Credit Paperwork Appointment"
→ **Add note**: "Appeal approved, moving to next stage"

---

## ⚡ **QUICK ACTIONS CHEATSHEET**

| Task | Steps |
|------|-------|
| **Add new applicant** | "✨ New Unit Available" → Fill form → Save |
| **Move between stages** | Drag applicant card OR click card → edit stage |
| **Mark action complete** | Click red ✗ to turn green ✓ |
| **Add process note** | Click applicant → Process Log → "+ Add Note" |
| **Send email** | Click applicant → Process Log → "📧 Email" → Copy template |
| **Check stage details** | Click ℹ️ on any stage header |
| **View detailed action items** | Click "👆 Click for details" in Active Action Items panel |
| **See missing documents** | Click "Missing Documentation" → View per-client breakdown |
| **Check pending actions** | Click "Pending Action Items" → See role-based assignments |

---

## 🎯 **SAMPLE APPLICANTS (Demo Data)**

- **Jane Smith** (Unit 204) - Waiting for JOHS Referral
- **Michael Johnson** (Unit 301) - Waiting on Application Packet  
- **Maria Rodriguez** (Unit 105) - Waiting on Background Check
- **Robert Chen** (Unit 207) - Waiting on Appeal Documentation
- **Sarah Williams** (Unit 302) - Tax Credit Paperwork Appointment
- **David Brown** (Unit 408) - Waiting for Video Intake
- **Lisa Garcia** (Unit 501) - Contract and Lease Signing Meeting
- **James Wilson** (Unit 203) - Wraparound Support Appointment

---

## 💡 **PRO TIPS FOR EMAIL + WEB AUTOMATION**

1. **Always check action items** - They tell you exactly what needs to happen next
2. **Use stage info modals** - Click ℹ️ for detailed process guidance  
3. **Process log is your friend** - Complete audit trail of all actions
4. **Email templates save time** - Pre-written with variables, just copy and paste
5. **Document tracking prevents delays** - Green ✅ = ready to proceed
6. **Appeals stage is critical** - 10 business day window to keep unit on hold
7. **Click for detailed insights** - Use "👆 Click for details" on action items for comprehensive breakdowns
8. **Monitor the right panel** - Active Action Items panel shows real-time system-wide issues
9. **Use detailed popups** - Get client-specific information without clicking through multiple cards

---

## 🚨 **IMPORTANT REMINDERS**

- **Data persists** - All changes auto-save to browser localStorage
- **Stage order matters** - Don't skip stages without good reason
- **Time is critical** - PSH process has deadlines (3 weeks for JOHS, 10 days for appeals)
- **Multiple stakeholders** - Property managers, case managers, JOHS, Home Forward all involved
- **Documentation is key** - Missing docs = process delays

---

**🎯 This platform transforms email chains and spreadsheet chaos into an organized, trackable workflow that helps people get housed faster!**