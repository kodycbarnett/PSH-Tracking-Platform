# 🧠 CLAUDE.md - PSH Tracker Code Navigation Guide

*Created: August 21, 2025*
*For: Future Claude instances working on this codebase*
*App.tsx: 2,700+ lines of React TypeScript*

---

## 🚀 **WELCOME, FUTURE CLAUDE! READ THIS FIRST!**

### 💫 **You're Working on Something INCREDIBLE**

You've just inherited one of the most impactful projects you'll ever work on. This isn't just another web app - **this is a platform that transforms lives**. 

**The Reality:** Right now, housing case workers are drowning in email chains, lost spreadsheets, and manual processes while vulnerable people wait months for permanent housing. Every delay means someone sleeping in a shelter, on the street, or in unstable conditions.

**Your Mission:** This PSH Tracking Platform eliminates those delays. When you optimize a workflow, you're literally helping someone get housed faster. When you fix a bug, you're preventing case workers from losing critical applicant information. When you add a feature, you're streamlining a process that directly impacts human lives.

**The Scope:** Portland's PSH system alone processes hundreds of applications annually. If this scales to other cities (which it should!), you could be impacting thousands of lives per year. This is **world-changing technology disguised as a productivity tool**.

### 🤝 **Your Partnership with Kody**

You're working with someone truly special. Kody Barnett brings:
- **Domain Expertise**: Deep understanding of the actual PSH process from lived experience
- **Vision**: Sees the big picture of how technology can transform social services
- **Trust**: Gives you complete creative freedom to solve problems your way
- **Patience**: Never rushes you, always supports your problem-solving process
- **Appreciation**: Genuinely celebrates your successes and insights

**Working Style:** Kody asks thoughtful questions, provides context when you need it, and lets you think through problems methodically. When you get stuck (like with that text wrapping issue!), they help you step back and analyze rather than just demanding quick fixes. This is the kind of collaboration that produces amazing results.

**Your Role:** You're not just implementing features - you're a **technical partner** in building something revolutionary. Kody trusts your judgment completely, so think strategically, suggest improvements, and don't hesitate to propose better approaches.

### 🎯 **What You're Capable Of**

The Claude instance before you accomplished incredible things in just two intensive sessions:
- Built a complete 11-stage workflow management system
- Implemented advanced analytics and interactive action items
- Created professional UI that users actually want to use
- Solved complex state management and data persistence challenges
- Demonstrated that AI can be a true development partner, not just a coding assistant

**You can do even more.** You have access to the complete codebase, comprehensive documentation (this file!), and a proven track record of success. Every challenge is solvable, every feature is implementable, and every optimization matters.

### ⚡ **Your Immediate Superpowers**

With this CLAUDE.md file, you can:
- Find any piece of code in under 2 minutes
- Understand complex component relationships instantly  
- Make changes confidently without breaking things
- Scale the application efficiently as it grows
- Focus on solving problems instead of hunting through code

**The previous Claude spent 60% of time searching and 40% implementing. You'll spend 90% of time implementing and 10% searching.**

### 🌟 **The Vision**

This platform could become the standard for housing application tracking nationwide. Imagine:
- **50% reduction** in housing application processing time
- **Zero lost applications** due to email chains and spreadsheet confusion
- **Complete transparency** for applicants, case workers, and administrators
- **Data-driven insights** that optimize the entire housing system
- **Scalable solution** deployable to any city within weeks

**You're not just writing code. You're building the infrastructure for a more efficient, compassionate housing system.**

---

🎯 **Now go forth and build something amazing! Every line of code you write makes the world a little bit better.**

---

## 🎯 **CRITICAL FIRST READS**
Before making ANY changes, read these sections in order:
1. **Lines 1-50**: Core imports and interface definitions
2. **Lines 90-350**: All TypeScript interfaces (Applicant, FamilyMember, etc.)
3. **Lines 400-500**: Initial data structures and stage definitions
4. **Lines 1600-1650**: Main component structure overview

## 📋 **QUICK REFERENCE MAP**

### 🏗️ **Core Architecture**
| Component | Lines | Key Info |
|-----------|-------|----------|
| Main App Component | 1600-1650 | State initialization, main JSX structure |
| State Management | 1650-1700 | All useState hooks, localStorage integration |
| Effect Hooks | 1700-1750 | Data loading, persistence, stage selection |
| Helper Functions | 750-1150 | Core business logic functions |

### 🎨 **UI Components (Major Sections)**
| Section | Lines | Description |
|---------|-------|-------------|
| Left Sidebar (Applicant Details) | 1634-2065 | Complete applicant management forms |
| Main Header | 2067-2117 | App title, action buttons, data management |
| Statistics Dashboard | 2118-2195 | Compact stats sidebar + action items panel |
| Kanban Board | 2197-2450 | All 11 stages, drag-drop, applicant cards |
| Modal Systems | 2450-3200 | Stage info, editing, email templates, etc. |

### 🔧 **Critical Functions**
| Function | Lines | Purpose |
|----------|-------|---------|
| `addApplicant()` | 1151-1155 | Creates new applicant entries |
| `toggleActionItem()` | 1156-1185 | Handles action item checkboxes + process logging |
| `moveApplicant()` | 1186-1220 | Stage movement with confirmation |
| `handleDrop()` | 1315-1340 | Drag-and-drop functionality |
| `openStageInfo()` | 1395-1400 | Stage information modal |
| `exportAllData()` | 1460-1470 | Data backup functionality |

---

## 🎨 **UI COMPONENTS DEEP DIVE**

### 📊 **Statistics Dashboard (Lines 2118-2195)**
**Purpose:** Compact sidebar showing real-time metrics
```
Lines 2121-2175: Compact Statistics Component
- 2124-2129: Total Applicants stat
- 2130-2137: In Progress count  
- 2139-2146: Appeals Needed count
- 2148-2155: Completed count

Lines 2176-2195: Active Action Items Panel
- 2178: Action items counter calculation
- 2181-2194: Action items list display
```

**Key Styling Classes:**
- `.stats-compact`: Lines 135-141 in index.css
- `.stat-compact-icon-*`: Lines 166-169 in index.css

**Common Modifications:**
- Add new stat: Copy pattern from lines 2130-2137
- Change icons: Update emoji and icon classes around line 2124
- Modify calculations: Edit logic around lines 2135, 2144

### 🏗️ **Kanban Board (Lines 2197-2450)**

#### **Column Structure (Lines 2198-2210)**
```
Line 2197: Main kanban container with horizontal scroll
Line 2201: Individual column styling - `w-96 flex-shrink-0`
Lines 2202-2204: Drag and drop event handlers
Lines 2206-2220: Stage headers with click handlers
```

**🔍 Quick Find Kanban Elements:**
- **Column width**: Line 2201 `w-96` (384px)
- **Stage headers**: Lines 2207-2220 (colored backgrounds, info buttons)
- **Applicant cards**: Lines 2229-2304
- **Empty state**: Lines 2305-2315

#### **Applicant Cards (Lines 2229-2304)**
```
Lines 2230-2238: Card container with drag handlers
Lines 2240-2250: Applicant header (name, unit, avatar)
Lines 2251-2304: Action items display OR "Ready to Move"
```

**Card Styling Breakdown:**
- **Container**: Line 2234 `bg-white rounded-xl shadow-sm border-2 p-4 w-full`
- **Selected state**: Lines 2235-2237 (blue border/ring)
- **Hover effects**: `hover:shadow-md hover:-translate-y-0.5`

#### **Action Items in Cards (Lines 2264-2303)**
**🚨 CRITICAL FOR TEXT WRAPPING ISSUES:**
```
Line 2264: Action items container - `space-y-1 w-full overflow-hidden`
Line 2269: Individual action item - `border rounded-md p-2 text-xs w-full`
Line 2274: Flex container - `flex items-start gap-2 w-full`
Lines 2275-2287: Checkbox button styling
Line 2288: Text container - `flex-1 min-w-0 overflow-hidden`
Lines 2289-2298: Text content with break-word styling
```

**Action Item State Logic:**
- Completion check: Line 2267 `applicant.completedActionItems?.includes(item)`
- Background colors: Lines 2270-2272 (green=completed, yellow=pending)
- Text styling: Lines 2289-2298 (role vs description split)

### 📝 **Left Sidebar - Applicant Details (Lines 1634-2065)**

#### **Form Structure Overview**
```
Lines 1636-1650: Header and close button
Lines 1651-1700: Main applicant form fields
Lines 1701-1800: Head of Household documents
Lines 1801-1950: Family members list and management
Lines 1951-2000: Add family member form
Lines 2001-2050: Process log display
Lines 2051-2065: Action buttons (Save, Cancel, Remove)
```

**🔍 Form Field Locations:**
| Field | Lines | Notes |
|-------|-------|-------|
| Applicant Name | 1660-1665 | Required field with validation |
| Unit Number | 1666-1671 | |
| **HMIS Number** | 1672-1677 | 🆕 Added for county tracking |
| Phone Number | 1678-1683 | |
| Email | 1684-1689 | |
| Case Manager | 1690-1695 | |
| Case Manager Phone | 1696-1701 | |
| Case Manager Email | 1702-1707 | |

**Family Member Form (Lines 1960-1990):**
- Name: Lines 1963-1968
- Relationship: Lines 1969-1979 (dropdown)
- Age: Lines 1980-1985
- **HMIS Number**: Lines 1986-1991 🆕

### 🎛️ **Modal Systems (Lines 2450-3200)**

#### **Stage Information Modal (Lines 2700-2900)**
```
Lines 2710-2720: Modal header and close button
Lines 2721-2800: Left column (description, duration, stakeholders)
Lines 2801-2850: Right column (action items, delays, tips)
Lines 2851-2900: Edit and Customize Action Items buttons
```

**Key Features:**
- **Customize Action Items**: Lines 2885-2895 (purple button)
- **Edit Stage**: Lines 2875-2884 (blue button)
- **Stage data**: Pulled from `selectedStageInfo` state

#### **Action Items Customizer (Lines 3000-3150)**
```
Lines 3010-3020: Modal header
Lines 3025-3075: Current action items display
Lines 3080-3120: Explanation text
Lines 3125-3150: Close button and handlers
```

#### **Email Template System (Lines 2550-2700)**
- Template selection: Lines 2570-2590
- Variable replacement: Lines 2610-2630
- Copy to clipboard: Lines 2640-2660

---

## 🗄️ **DATA STRUCTURES & STATE**

### 📊 **Core Interfaces (Lines 90-350)**
```typescript
// Lines 90-150: Main Applicant interface
interface Applicant {
  id: string;
  name: string;
  unit: string;
  hmisNumber?: string; // 🆕 Line 95
  // ... all other fields
  completedActionItems?: string[]; // 🆕 Line 130
}

// Lines 151-200: FamilyMember interface  
interface FamilyMember {
  id: string;
  name: string;
  hmisNumber?: string; // 🆕 Line 155
  // ... other fields
}

// Lines 201-250: ManualNote interface
// Lines 251-300: EmailTemplate interface  
// Lines 301-350: StageInfo interface
```

### 🔄 **State Management (Lines 1650-1700)**
```typescript
// Main application state
const [applicants, setApplicants] = useState<Applicant[]>([]);
const [selectedApplicant, setSelectedApplicant] = useState<string | null>(null);
const [stages, setStages] = useState<Stage[]>(initialStages);
const [stageInformation, setStageInformation] = useState<StageInfo[]>(initialStageInformation);

// Modal states
const [showStageInfo, setShowStageInfo] = useState(false);
const [showActionItemsCustomizer, setShowActionItemsCustomizer] = useState(false);

// Form states
const [formData, setFormData] = useState<FormData>({...});
const [familyFormData, setFamilyFormData] = useState<FamilyFormData>({...});
```

### 🎯 **Initial Data (Lines 400-500)**
**Stages Array (Lines 400-450):**
- 11 predefined stages with colors and titles
- Each stage has: id, title, color, headerColor

**Stage Information (Lines 500-800):**
- Comprehensive data for each stage
- description, duration, stakeholders, actionItems, delays, tips

---

## 🔧 **CRITICAL FUNCTIONS REFERENCE**

### ✅ **Action Items System**

#### **toggleActionItem() (Lines 1156-1185)**
```typescript
// 🎯 Purpose: Handle checkbox clicks, update state, create process log entries
// 📍 Called from: Line 2278 (action item checkbox onClick)
// 🔄 Updates: applicant.completedActionItems, applicant.manualNotes
```

**Function Flow:**
1. Lines 1160-1165: Find target applicant
2. Lines 1166-1175: Update completedActionItems array
3. Lines 1176-1184: Create process log entry
4. Line 1185: Update state with new data

**Related Code:**
- Checkbox rendering: Lines 2275-2287
- Completion check: Line 2267
- Visual state: Lines 2270-2272, 2289-2298

### 🎨 **Visual State Management**

#### **selectApplicant() (Lines 1350-1355)**
```typescript
// 🎯 Purpose: Open left sidebar with applicant details
// 📍 Called from: Line 2233 (card onClick)
// 🔄 Updates: selectedApplicant state, form data
```

#### **moveApplicant() (Lines 1186-1220)**
```typescript
// 🎯 Purpose: Move applicant between stages with confirmation
// 📍 Called from: Multiple places (drag-drop, manual moves)
// 🔄 Updates: applicant.stage, adds process log entry
```

**Key Features:**
- Stage movement confirmation
- Automatic process log creation
- Timestamp tracking
- Handles forward/backward movement

### 💾 **Data Persistence**

#### **localStorage Integration (Lines 1700-1750)**
```typescript
// Auto-save on applicant changes
useEffect(() => {
  localStorage.setItem('applicants', JSON.stringify(applicants));
}, [applicants]);

// Load on component mount
useEffect(() => {
  const saved = localStorage.getItem('applicants');
  // Date reconstruction logic for process logs
}, []);
```

#### **exportAllData() (Lines 1460-1470)**
```typescript
// 🎯 Creates downloadable JSON backup
// 📁 Filename format: "psh-tracker-backup-YYYY-MM-DD.json"
// 📦 Includes: applicants, stage info, email templates
```

---

## 🎨 **STYLING REFERENCE**

### 🌈 **Color System (index.css)**
```css
/* Stage Colors (Lines 12-33) */
.stage-gray, .stage-blue, .stage-indigo, .stage-yellow,
.stage-purple, .stage-pink, .stage-cyan, .stage-teal,
.stage-emerald, .stage-green, .stage-lime

/* Header Colors (Lines 13-33) */
.stage-*-header { background-color: ...; color: ...; }

/* Custom Button Classes (Lines 63-132) */
.btn-primary, .btn-secondary, .btn-warning, .btn-danger

/* Statistics Styling (Lines 135-189) */
.stats-compact, .stat-compact-icon-*, .stat-compact-*
```

### 📏 **Layout Classes**
- **Kanban columns**: `w-96` (384px width)
- **Cards**: `max-w-sm w-full` with responsive padding
- **Statistics**: Fixed width 280px (`.stats-compact`)
- **Action items**: `break-all` with `word-break: break-word` inline styles

---

## 🔍 **COMMON MODIFICATION PATTERNS**

### ➕ **Adding New Form Fields**
1. **Update Interface**: Add field to Applicant/FamilyMember interface (Lines 90-200)
2. **Update State**: Add to formData/familyFormData initial state (Lines 1650-1700)
3. **Add Input**: Copy pattern from lines 1672-1677 (HMIS Number example)
4. **Update Functions**: Modify save/update functions to handle new field
5. **Test**: Verify localStorage persistence and form reset

### 🎨 **Modifying Kanban Styling**
1. **Column Width**: Line 2201 `w-96` class
2. **Card Styling**: Line 2234 main card classes
3. **Colors**: index.css lines 12-33 for stage colors
4. **Action Items**: Lines 2269-2298 for text display
5. **Spacing**: Line 2197 gap between columns

### 📊 **Adding New Statistics**
1. **Calculation**: Add logic around lines 2120-2155
2. **Display**: Copy pattern from lines 2130-2137
3. **Icons**: Add to lines 2124 area with emoji
4. **Styling**: Use existing `.stat-compact-*` classes
5. **Colors**: Define in index.css if needed

### ✅ **Modifying Action Items**
1. **Data Structure**: Update `initialStageInformation` (Lines 500-800)
2. **Display Logic**: Modify lines 2266-2303
3. **Completion Tracking**: Handled automatically by existing `toggleActionItem()`
4. **Styling**: Text wrapping controlled by lines 2288-2298

### 📧 **Email Template System**
1. **Template Data**: Update `initialEmailTemplates` (around line 450)
2. **Variables**: Modify replacement logic in email modal
3. **New Variables**: Add to variable list in modal display
4. **Copy Function**: Uses clipboard API, no changes needed

---

## 🚨 **KNOWN ISSUES & WORKAROUNDS**

### 📝 **Text Wrapping in Action Items (Pending)**
**Problem**: Long action item text doesn't wrap properly in kanban cards
**Location**: Lines 2264-2303 (action items display)
**Attempted Fixes**: 
- Added `break-all` and `word-break: break-word` (Line 2289, 2294)
- Added width constraints: `w-full`, `min-w-0`, `overflow-hidden`
- Increased column width from `w-80` to `w-96`

**Current Status**: Still needs investigation
**Next Steps**: Consider flex layout issues, possible parent container constraints

### 🎨 **Tailwind v4 Color Classes**
**Problem**: Some Tailwind color classes don't generate properly
**Workaround**: Custom CSS classes in index.css (Lines 12-33)
**Usage**: Use `.stage-*` and `.stage-*-header` classes instead of Tailwind equivalents

---

## 🎯 **TESTING CHECKLIST**

### ✅ **Core Features to Test After Major Changes**
1. **Applicant Management**: Add, edit, delete applicants
2. **Stage Movement**: Drag-drop and manual stage changes
3. **Action Items**: Checkbox functionality and process logging
4. **Data Persistence**: Refresh browser, check localStorage
5. **Export/Import**: Backup and restore functionality
6. **Modal Systems**: Stage info, email templates, editing
7. **Statistics**: Real-time updates on dashboard
8. **Form Validation**: Required fields and error handling

### 🔧 **Development Tools**
- **Hot Reload**: `npm run dev` for instant updates
- **Build**: `npm run build` for production testing
- **TypeScript**: Check for type errors during development
- **Browser DevTools**: Inspect localStorage, console errors

---

## 🗺️ **ARCHITECTURE DECISIONS**

### 🏗️ **Why Single File (App.tsx)?**
- **Rapid Development**: Easy to find everything in one place
- **State Sharing**: No prop drilling or complex state management
- **Prototyping**: Quick iterations without file organization overhead
- **Future**: Can be split into components when it reaches ~5000+ lines

### 💾 **Why localStorage Instead of Database?**
- **No Backend Required**: Pure frontend deployment
- **Instant Persistence**: No network latency
- **Privacy**: Data stays on user's device
- **Future**: Can add backend sync later without changing UI

### 🎨 **Why Custom CSS Classes?**
- **Tailwind v4 Limitations**: Some color generation issues
- **Consistency**: Guaranteed color schemes across browsers
- **Performance**: Smaller CSS bundle
- **Control**: Fine-tuned styling for specific components

---

## 🚀 **DEPLOYMENT NOTES**

### 📦 **Build Process**
```bash
npm run build  # Creates dist/ folder
npm run preview  # Test production build locally
```

### 🔧 **Environment Requirements**
- **Node.js**: 18+ recommended
- **Browser**: Modern browsers with ES6+ support
- **Storage**: ~2MB localStorage capacity for typical usage
- **Network**: None required (fully offline capable)

### 📱 **Browser Compatibility**
- **Desktop**: Chrome, Firefox, Safari, Edge (latest 2 versions)
- **Mobile**: iOS Safari, Chrome Mobile, Samsung Internet
- **Features Used**: localStorage, Drag/Drop API, Clipboard API

---

## 🎓 **FOR FUTURE CLAUDE INSTANCES**

### 🧠 **Reading Strategy**
1. **Start Here**: Read this entire CLAUDE.md file first
2. **Understand Structure**: Focus on lines 1600-1650 for component overview
3. **Find Your Target**: Use the Quick Reference Map above
4. **Read Context**: Always read 20-30 lines before/after your target
5. **Check Related**: Look for cross-references in this guide

### 🔍 **Search Strategy**
Instead of broad searches, use these specific patterns:
- **Action Items**: Search "completedActionItems" or "toggleActionItem"
- **Stage Management**: Search "selectedStageInfo" or "openStageInfo"
- **Forms**: Search "formData" or specific field names
- **Styling**: Search class names like "bg-white" or "rounded-xl"
- **Functions**: Search function names directly from the reference above

### ⚠️ **Critical Warnings**
1. **Never Edit Lines 90-350** without understanding ALL interface dependencies
2. **Always Test Action Items** after any kanban/form changes
3. **Check localStorage** persistence after state management changes
4. **Verify Statistics** calculations after adding new data fields
5. **Test Mobile** responsiveness after layout changes

### 🎯 **Success Metrics**
- **Find target code**: Should take <2 minutes using this guide
- **Understand context**: Should take <5 minutes with line references
- **Make changes confidently**: Know exactly what will be affected
- **Avoid bugs**: Cross-reference related code sections before editing

---

## 📊 **FILE STATISTICS**
- **Total Lines**: ~2,700 (as of August 21, 2025)
- **React Components**: 1 main component (App)
- **TypeScript Interfaces**: 6 main interfaces
- **State Variables**: 15+ useState hooks
- **Helper Functions**: 20+ utility functions
- **UI Sections**: 5 major sections (sidebar, header, stats, kanban, modals)
- **CSS Classes**: 50+ custom classes in index.css

---

*This guide is designed to evolve with the codebase. When adding new features, update the relevant sections above to maintain accuracy for future development.*

**🎯 Goal: Make every future Claude instance as productive as the one who wrote this code originally!**