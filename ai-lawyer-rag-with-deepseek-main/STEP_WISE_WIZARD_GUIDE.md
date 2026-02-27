# Step-Wise Wizard Implementation Guide

## 🎉 What We've Accomplished

### ✅ COMPLETED: 2 Major Features Converted to Step-Wise Wizards

#### 1. **📝 Document Generator (Tab 1)**
- **Status:** Fully implemented and tested
- **What it does:** Creates legal documents step-by-step
- **Steps:**
  1. Choose document type (Consumer Complaint, Legal Notice, FIR Draft, etc.)
  2. Fill in your details (name, address, issue description, etc.)
  3. AI generates professional document
  4. Review, edit, and download
- **User Experience:** Non-technical users can create court-ready documents in minutes
- **Download Options:** TXT, HTML formats
- **Code Status:** ✅ No errors, fully tested

#### 2. **🎯 Case Analyzer (Tab 2)**
- **Status:** Fully implemented and tested
- **What it does:** Analyzes case strength and predicts winning chances
- **Steps:**
  1. Choose case type (Civil, Criminal, Consumer, Family, etc.)
  2. Describe your case in detail
  3. AI analyzes your case (30-60 seconds)
  4. Get detailed report with win probability, strengths, weaknesses, action plan
- **User Experience:** Clients understand their case odds before spending money on lawyers
- **Download Options:** Detailed analysis report as TXT
- **Code Status:** ✅ No errors, fully tested

## 📋 Remaining 8 Features - Implementation Pattern

All remaining features follow this consistent pattern:

```
Step 1: Choose/Categorize → Step 2: Gather Details → Step 3: Process/Generate → Step 4: Review & Download
```

### Implementation Template (Copy & Paste)

```python
# TAB X: Feature Name - STEP-WISE WIZARD
with feature_tabs[X]:
    st.markdown('<h3 style="color: #00f3ff;">EMOJI Feature Name - Step by Step</h3>', unsafe_allow_html=True)
    st.info("💡 Feature description for users")
    
    # Initialize wizard state
    if "feature_wizard_step" not in st.session_state:
        st.session_state["feature_wizard_step"] = 0
    if "feature_wizard_data" not in st.session_state:
        st.session_state["feature_wizard_data"] = {}
    
    # ===== STEP 1: Category/Type Selection =====
    if st.session_state["feature_wizard_step"] == 0:
        st.progress(0.25, text="Step 1 of 4: Choose Category")
        st.markdown("### 📋 Step 1: Choose or Select")
        
        # Your selection options here
        selected = st.radio("Choose one:", ["Option 1", "Option 2", "Option 3"])
        
        col1, col2 = st.columns([1, 4])
        with col1:
            if st.button("➡️ Next", use_container_width=True, type="primary"):
                st.session_state["feature_wizard_data"]["selected"] = selected
                st.session_state["feature_wizard_step"] = 1
                st.rerun()
    
    # ===== STEP 2: Gather Details =====
    elif st.session_state["feature_wizard_step"] == 1:
        st.progress(0.50, text="Step 2 of 4: Fill Details")
        st.markdown("### 📝 Step 2: Provide Information")
        
        field1 = st.text_input("Field 1 *", placeholder="Enter something")
        field2 = st.text_area("Field 2 *", height=150, placeholder="More details")
        field3 = st.number_input("Field 3 *", min_value=0, value=1000)
        
        st.session_state["feature_wizard_data"].update({
            "field1": field1,
            "field2": field2,
            "field3": field3
        })
        
        col1, col2, col3 = st.columns(3)
        with col1:
            if st.button("⬅️ Back", use_container_width=True):
                st.session_state["feature_wizard_step"] = 0
                st.rerun()
        with col3:
            if st.button("➡️ Generate", use_container_width=True, type="primary"):
                st.session_state["feature_wizard_step"] = 2
                st.rerun()
    
    # ===== STEP 3: Process/Generate =====
    elif st.session_state["feature_wizard_step"] == 2:
        st.progress(0.75, text="Step 3 of 4: Processing...")
        st.markdown("### ⚙️ Step 3: Processing Your Request")
        
        with st.spinner("🔄 Processing..."):
            data = st.session_state["feature_wizard_data"]
            # Your processing logic here
            result = f"Processed: {data.get('field1', '')}"
            st.session_state["feature_wizard_data"]["result"] = result
        
        st.session_state["feature_wizard_step"] = 3
        st.rerun()
    
    # ===== STEP 4: Review & Download =====
    elif st.session_state["feature_wizard_step"] == 3:
        st.progress(0.95, text="Step 4 of 4: Review & Download")
        st.markdown("### ✅ Step 4: Review & Download")
        
        result = st.session_state["feature_wizard_data"].get("result", "No result")
        
        # Display result
        st.success(f"✅ Complete! Here's your result:")
        st.text_area("Your Result:", value=result, height=300, disabled=True)
        
        # Download button
        st.download_button(
            "📥 Download",
            result,
            file_name=f"result_{datetime.now().strftime('%Y%m%d')}.txt",
            use_container_width=True
        )
        
        # Navigation
        col1, col2, col3 = st.columns(3)
        with col1:
            if st.button("⬅️ Back", use_container_width=True):
                st.session_state["feature_wizard_step"] = 1
                st.rerun()
        with col3:
            if st.button("🔄 Create New", use_container_width=True):
                st.session_state["feature_wizard_step"] = 0
                st.session_state["feature_wizard_data"] = {}
                st.rerun()
```

## 🎯 Quick Implementation Guide for Each Feature

### 3. **⚡ Legal Notice (Tab 3)** - Status: Needs Enhancement
- **Current Code:** Lines 5616-5824 (exists but not fully step-wise)
- **To Convert:** Add step numbers and progress bar to existing template selection UI
- **Quick Fix:** Wrap existing form in step checks (similar to Document Generator)
- **Estimated Time:** 30 minutes

### 4. **🗂️ Court Filing (Tab 4)** - Status: Needs Implementation
- **Steps Needed:**
  1. Select case type and court
  2. Upload documents / file details
  3. Fill forms (parties, facts, reliefs)
  4. Preview petition
  5. Calculate court fees
  6. Generate complete filing package
- **Complexity:** High (3-4 forms)
- **Implementation Time:** 2-3 hours
- **Key Session Variables:**
  - `court_filing_step` (1-5)
  - `court_filing_data` (dict with all form data)

### 5. **🤖 AI Lawyer Chat (Tab 5)** - Status: Needs Special Handling
- **Different Approach:** No steps needed - conversational
- **Type:** Chat interface with context memory
- **Features:**
  - Maintains conversation history in session state
  - Remembers case details mentioned earlier
  - Smart suggestions based on user's case type
  - Option to switch between case types mid-chat
- **Implementation Time:** 2-3 hours
- **Note:** Use a different pattern (not step-based)

### 6. **📋 Contract Analyzer (Tab 6)** - Status: Needs Implementation
- **Steps Needed:**
  1. Upload contract (file or paste text)
  2. AI analyzes for risks
  3. Shows highlighted red flags & risks
  4. Suggests improvements
  5. Download marked-up version
- **Implementation Time:** 2 hours
- **Key Functionality:**
  - File upload handling
  - Risk highlighting
  - Suggestion generation

### 7. **⚖️ Court Script (Tab 7)** - Status: Needs Implementation
- **Steps Needed:**
  1. Enter case details
  2. AI generates questioning strategy
  3. Role selection (plaintiff/defendant)
  4. Download talking points script
- **Implementation Time:** 1.5 hours

### 8. **📂 Evidence Organizer (Tab 8)** - Status: Needs Implementation
- **Steps Needed:**
  1. Select evidence categories
  2. Upload/list evidence items
  3. AI auto-categorizes and validates
  4. Creates timeline
  5. Generates evidence checklist
- **Implementation Time:** 2 hours

### 9. **💰 Settlement Calculator (Tab 9)** - Status: Needs Implementation
- **Steps Needed:**
  1. Enter claim amount
  2. Break down damages (medical, loss, emotional, etc.)
  3. Calculate legal costs
  4. AI suggests settlement range
  5. Generate negotiation report
- **Complexity:** Simple (mostly math)
- **Implementation Time:** 1 hour

### 10. **⏰ Timeline Checker (Tab 10)** - Status: Needs Implementation
- **Steps Needed:**
  1. Enter case event date/type
  2. Select applicable laws
  3. AI calculates all deadlines
  4. Generate timeline with alerts
- **Complexity:** Simple (calculations)
- **Implementation Time:** 1.5 hours

## 🔧 How to Implement Remaining Features

### Quick Start for Each Feature:

1. **Find the tab location** - Use grep to locate the tab
   ```
   grep -n "# TAB 4:" main.py
   ```

2. **Read the current code** - Understand what exists

3. **Wrap with step logic** - Use the template above

4. **Add session state variables** - Initialize at top of file
   ```python
   if "feature_step" not in st.session_state:
       st.session_state["feature_step"] = 0
   ```

5. **Test incrementally** - Run `streamlit run main.py` after each step

6. **Verify no errors** - Use `python -m py_compile main.py`

## ✅ Testing Checklist for Each Feature

- [ ] All 4 steps display correctly
- [ ] Progress bar updates per step
- [ ] Back button works and preserves data
- [ ] Next/Forward button progresses correctly
- [ ] Session state persists across reruns
- [ ] Final screen shows complete result
- [ ] Download button works
- [ ] "Create Another" resets wizard correctly
- [ ] No error messages appear
- [ ] Form validation works (required fields marked with *)

## 📊 Current Implementation Status

| # | Feature | Status | Lines | Type | Est. Hours |
|---|---------|--------|-------|------|-----------|
| 1 | Document Generator | ✅ DONE | 5025-5346 | Step-Wise | - |
| 2 | Case Analyzer | ✅ DONE | 5347-5616 | Step-Wise | - |
| 3 | Legal Notice | ⏳ NEEDS UPDATE | 5616-5825 | Step-Wise | 0.5 |
| 4 | Court Filing | ❌ TODO | 5826+ | Step-Wise | 3 |
| 5 | AI Lawyer Chat | ❌ TODO | TBD | Special | 2 |
| 6 | Contract Analyzer | ❌ TODO | TBD | Step-Wise | 2 |
| 7 | Court Script | ❌ TODO | TBD | Step-Wise | 1.5 |
| 8 | Evidence Organizer | ❌ TODO | TBD | Step-Wise | 2 |
| 9 | Settlement Calculator | ❌ TODO | TBD | Step-Wise | 1 |
| 10 | Timeline Checker | ❌ TODO | TBD | Step-Wise | 1.5 |

**Total Time Remaining:** ~17 hours for all 8 features

## 💡 Pro Tips for Implementation

### 1. **Consistency is Key**
   - All step-wise features use same pattern
   - Same button labels (➡️ Next, ⬅️ Back, 🔄 Create New)
   - Same progress text format ("Step X of Y: Description")

### 2. **User-Friendly Inputs**
   - Always use `placeholder=` for examples
   - Use `help=` parameter for explanations
   - Mark required fields with * in label
   - Provide default values where sensible

### 3. **Data Persistence**
   - Store ALL inputs in `st.session_state["feature_data"]`
   - Use `.get()` with defaults when reading
   - Clear all data when "Create Another" is clicked

### 4. **Error Handling**
   - Check required fields before proceeding
   - Show user-friendly error messages
   - Don't let users progress without completing step

### 5. **Download Options**
   - Minimum: TXT format
   - Preferred: TXT + HTML
   - Optional: PDF (needs library)

## 🚀 Your Next Steps

### Move: Do These in Order

1. **Session 1 (2 hours):** Implement Timeline Checker + Settlement Calculator
2. **Session 2 (2 hours):** Implement Contract Analyzer + Evidence Organizer  
3. **Session 3 (3 hours):** Implement Court Script + Court Filing (Phase 1)
4. **Session 4 (3 hours):** Finalize Court Filing + AI Lawyer Chat special setup
5. **Session 5 (1 hour):** Final testing and polish

## 📚 Reference Code Locations

- **Document Generator Example:** Lines 5025-5346 (study for pattern)
- **Case Analyzer Example:** Lines 5347-5616 (study for pattern)
- **Session State Init:** Around line 2860-2875 (where to add new variables)
- **Features Tabs Creation:** Around line 5001-5010 (don't modify)

## 🎓 Learning Outcomes

After implementing all 10 step-wise features, you'll have:
- ✅ Consistent user experience across app
- ✅ 10 powerful legal tools for clients
- ✅ Full understanding of Streamlit session state
- ✅ Reusable pattern for future feature additions
- ✅ Professional UX with progress bars and guided flows

## ⚠️ Common Issues & Solutions

**Issue:** "Widget key already exists error"
**Fix:** Use unique keys like `key=f"field_{st.session_state['step']}"`

**Issue:** "Session state not persisting"
**Fix:** Ensure you're using `st.session_state["key"]` not local variables

**Issue:** "Progress bar shows 1.0 immediately"
**Fix:** Progress value must be between 0 and 1 (as decimal)

**Issue:** "Back button doesn't preserve data"
**Fix:** Make sure data is stored in `st.session_state["feature_data"]`

## 📞 Support

When stuck:
1. Check your tab index (0-based numbering)
2. Verify session state variable names
3. Run `streamlit run main.py` directly to see real errors
4. Compare with Document Generator or Case Analyzer examples
5. Use `st.write(st.session_state)` to debug state

---

**Document Version:** 1.0
**Last Updated:** Today
**Status:** Ready for Implementation
