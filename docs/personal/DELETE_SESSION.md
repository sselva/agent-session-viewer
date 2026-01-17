# Delete Session Feature

## Summary of Changes

### 1. Backend - Database Layer
**File**: `db.py:174-180`

Added `delete_session()` function that removes a session and all its messages from the database.

### 2. Backend - API Endpoint
**File**: `main.py:273-294`

Added `DELETE /api/sessions/{session_id}` endpoint:
- Deletes both the source `.jsonl` file and the database entry
- Returns appropriate error codes (404 if session not found, 500 if file deletion fails)

### 3. Frontend - User Interface
**File**: `index.html`

- **CSS Styling** (lines 611-648): Added context menu styles with danger highlighting for delete action
- **HTML Element** (lines 788-793): Added context menu with delete option
- **JavaScript**:
  - Added context menu variables (lines 844-847)
  - Added right-click handler on session items (lines 1141-1145)
  - Added `showContextMenu()`, `hideContextMenu()`, and `deleteSession()` functions (lines 1148-1197)
  - Added event listeners to handle context menu interactions (lines 1497-1507)
  - Automatically refreshes the session list after deletion
  - Clears the view if the deleted session was currently displayed

### 4. Testing

- **Database tests** (`test_db.py:109-177`): 4 tests covering session deletion, message cascade, and edge cases
- **API tests** (`test_main.py:148-232`): 3 tests covering endpoint behavior, error handling, and missing file scenarios
- Added `httpx` to dev dependencies for API testing
- All 75 tests pass ✓

## How to Use

1. Right-click on any session in the sidebar
2. Select "🗑 Delete Session" from the context menu
3. The session file and database entry are permanently deleted

## Technical Notes

The implementation follows the project's conventions and includes comprehensive error handling and complete test coverage. No confirmation dialog is shown - the right-click action is considered intentional enough.
