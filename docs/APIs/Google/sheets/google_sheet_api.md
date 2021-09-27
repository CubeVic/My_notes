# Google Sheets API

The task we can perform with the RESTful API will be:

- Create spreadsheets
- Read and write spreadsheets cell values
- update spreadsheets formatting
- Manage connected sheets


## Common terms

Some terms used in the API 

### Spreadsheet

It is the primary object, and it contains multiple sheets. It has a unique ID `spreeadsheetId` made with letters, numbers, hyphens, and underscores. You can find it in the google sheet URL. 

```python
https://docs.google.com/spreadsheets/d/spreadsheetId/edit#gid=0
```

[REST Resource: spreadsheets | Sheets API | Google Developers](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets)

### Sheet

A page or tab in the spreadsheet, sheets have a unique title and a numeric `sheetId` value which can be found in a google sheet URL.

```python
https://docs.google.com/spreadsheets/d/aBC-123_xYz/edit#gid=sheetId
```

[Sheets API | Google Developers](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets/sheets)

### Cell

An individual field of text or data within the sheets. Cells can be group vertically by rows and horizontally by columns.

### A1 notation

The method refers to one or a group of cells. It uses the sheet name, the column letter, and a numeric value that indicates the row. Bellow examples taken from the google sheet documentation: 

- `Sheet1!A1:B2` refers to the first two cells in the top two rows of Sheet1.
- `Sheet1!A:A` refers to all the cells in the first column of Sheet1.
- `Sheet1!1:2` refers to all the cells in the first two rows of Sheet1.
- `Sheet1!A5:A` refers to all the cells of the first column of Sheet 1, from row 5 onward.
- `A1:B2` refers to the first two cells in the top two rows of the first visible sheet.
- `Sheet1` refers to all the cells in Sheet1.

### R1C1 notation

This method is less common than A1 notation, and it is used to refer to some cells or cells about a specific point. It uses the sheet name and the starting and ending coordinates of the cell using the row and column numbers.

- `Sheet1!R1C1:R2C2` refers to the first two cells in the top two rows of Sheet1.
- `R1C1:R2C2` refers to the first two cells in the top two rows of the first visible sheet.
- `Sheet1!R[3]C[1]` refers to the cell that is three rows below and one column to the right of the current cell.

[Cells | Sheets API | Google Developers](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets/cells)

## Python Quickstart

There will be some prerequisites. They can be fine in the official documentation.

[Python Quickstart | Sheets API | Google Developers](https://developers.google.com/sheets/api/quickstart/python)

### 1. Install the google client library

```python
pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

### 2. Configure the example 

```python
from __future__ import print_function
import os.path
from googleapiclient.discovery import build
from google_auth_oauthlib.flow import InstalledAppFlow
from google.auth.transport.requests import Request
from google.oauth2.credentials import Credentials

# If modifying these scopes, delete the file token.json.
SCOPES = ['https://www.googleapis.com/auth/spreadsheets.readonly']

# The ID and range of a sample spreadsheet.
SAMPLE_SPREADSHEET_ID = '1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms'
SAMPLE_RANGE_NAME = 'Class Data!A2:E'

def main():
    """Shows basic usage of the Sheets API.
    Prints values from a sample spreadsheet.
    """
    creds = None
    # The file token.json stores the user's access and refresh tokens, and is
    # created automatically when the authorization flow completes for the first
    # time.
    if os.path.exists('token.json'):
        creds = Credentials.from_authorized_user_file('token.json', SCOPES)
    # If there are no (valid) credentials available, let the user log in.
    if not creds or not creds.valid:
        if creds and creds.expired and creds.refresh_token:
            creds.refresh(Request())
        else:
            flow = InstalledAppFlow.from_client_secrets_file(
                'credentials.json', SCOPES)
            creds = flow.run_local_server(port=0)
        # Save the credentials for the next run
        with open('token.json', 'w') as token:
            token.write(creds.to_json())

    service = build('sheets', 'v4', credentials=creds)

    # Call the Sheets API
    sheet = service.spreadsheets()
    result = sheet.values().get(spreadsheetId=SAMPLE_SPREADSHEET_ID,
                                range=SAMPLE_RANGE_NAME).execute()
    values = result.get('values', [])

    if not values:
        print('No data found.')
    else:
        print('Name, Major:')
        for row in values:
            # Print columns A and E, which correspond to indices 0 and 4.
            print('%s, %s' % (row[0], row[4]))

if __name__ == '__main__':
    main()
```
Now from the code above:

1. The import of the packages, in this case, I'm importing from the google library. It will make easy the interaction with the google API.  
2. `SCOPES` It is the limitation on the actions. For this case, it is limited to `readonly`.  
3. `SAMPLE_SPREADSHEET_ID` and `SAMPLE_RANGE_NAME` these are the ID for the spreadsheet and the range where I'm going to work in.  
4. Inside the main function will be a section where I will consult the file `credentials.json` this is the file I download from the dashboard in the OAuth 2.0 client ID section. 