# Test Day-Specific Study Hours Persistence

## Issue
Day-specific study hours were not being saved when the page was reloaded.

## Root Causes Found
1. **Missing fields in default settings** - `daySpecificStudyHours` and `showDaySpecificHoursSection` were missing from default settings objects in App.tsx
2. **No auto-save for day-specific hours operations** - Adding, deleting, or toggling day-specific hours only updated local state but didn't trigger an immediate save to localStorage

## Fixes Applied
1. Added `daySpecificStudyHours: []` and `showDaySpecificHoursSection: false` to all default settings objects in App.tsx
2. Modified day-specific hours handlers in Settings.tsx to immediately call `onUpdateSettings()` after state changes
3. Updated the settings parsing logic to handle the new fields when loading from localStorage

## Test Instructions
1. Go to Settings tab
2. Toggle on "Day-Specific Study Hours" section 
3. Add a day-specific study hour setting (e.g., Monday: 8 hours)
4. Reload the page
5. Go back to Settings
6. Verify the day-specific hours are still there and the section is still expanded

The fix ensures that:
- Day-specific study hours are immediately saved when added/edited/deleted
- The toggle state for showing the day-specific hours section persists
- Page reloads correctly restore all day-specific hour settings
