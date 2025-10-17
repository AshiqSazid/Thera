# TheraMuse Deployment Guide

## Fixed Issues

### 1. Database Path Issues ✅
- Fixed hardcoded database path for Streamlit Cloud compatibility
- Added automatic path detection for local vs cloud environments
- Database is now created as `theramuse.db` in the app directory on Streamlit Cloud

### 2. Missing Method Error ✅
- Fixed `_validate_location_relevance` method call in DementiaTherapy class
- Changed from `self._validate_location_relevance` to `self.youtube_api._validate_location_relevance`

### 3. Database Schema Migration ✅
- Added automatic database migration for existing tables
- Fixed corrupted `therapy_sessions` table schema
- Database auto-migrates on first run

### 4. Circular Import Issue ✅
- **Root Cause**: File was named `streamlit.py` which conflicted with the streamlit package
- **Solution**: Renamed file to `app.py`
- This was causing the "cannot import name 'TheraMuse' from partially initialized module 'ml'" error

## File Structure
```
/home/spectre-rosamund/Documents/github/
├── app.py              # Main app file (renamed from streamlit.py)
├── ml.py               # Core therapy logic and classes
├── theramuse.db        # SQLite database (auto-created)
├── requirements.txt    # Python dependencies
├── run_app.py         # Convenience script to run the app
├── .streamlit/
│   └── config.toml    # Streamlit configuration
└── README_DEPLOYMENT.md
```

## Running Locally

### Option 1: Using the run script
```bash
python run_app.py
```

### Option 2: Direct Streamlit command
```bash
streamlit run app.py
```

The app will open at http://localhost:8501

## Deploying to Streamlit Cloud

1. Push all changes to your GitHub repository
2. In Streamlit Cloud, connect your repository
3. Make sure the main file is set to `app.py`
4. Click Deploy

The app should now work without any database or import errors!

## Key Changes Made

1. **streamlit.py → app.py**: Fixed naming conflict with streamlit package
2. **Database path handling**: Added `get_database_path()` function for cross-platform compatibility
3. **Method call fix**: Fixed DementiaTherapy method reference
4. **Database migration**: Added automatic table schema migration
5. **Import error handling**: Added robust import error handling with debugging info

## Troubleshooting

If you still encounter issues:

1. Clear browser cache
2. Check that both `app.py` and `ml.py` are in the same directory
3. Verify `requirements.txt` includes all dependencies
4. Check Streamlit Cloud logs for any error messages

## Support

For any issues, check the error messages in:
- Streamlit Cloud logs (click "Manage app" in the lower right)
- Local console output when running the app