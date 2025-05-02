# Teams Mail Merge Application

This desktop application allows you to send personalized messages to multiple recipients via Microsoft Teams, similar to a traditional mail merge but for Teams communication. It's built with Python and customTkinter for the GUI.

## Features

- Upload data from Excel or CSV files
- Create message templates with placeholders for personalization
- Preview personalized messages before sending
- Authenticate with Microsoft Teams using Microsoft Graph API
- Send messages to individual recipients or run in test mode
- Track message delivery status and handle errors
- Rich text formatting support (bold, italic, links, mentions)

## Prerequisites

- Python 3.7 or higher
- Microsoft Azure account with permissions to register applications
- Registered Azure AD application with Microsoft Graph API permissions

## Installation

1. Clone or download this repository
2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

The required dependencies are:
- customtkinter
- pandas
- msal
- requests
- Pillow

## Azure AD App Registration

Before using the application, you must register an app in Azure AD:

1. Go to the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)
2. Click "New registration"
3. Enter a name for your application
4. Select the appropriate account types (single tenant or multi-tenant)
5. Add a redirect URI: `http://localhost:8000` (Web)
6. After registration, note the Application (client) ID and Directory (tenant) ID
7. Go to "Certificates & secrets" and create a new client secret
8. Go to "API permissions" and add the following Microsoft Graph permissions:
   - Chat.ReadWrite
   - User.Read
   - User.ReadBasic.All
9. Click "Grant admin consent" for these permissions

## Usage

1. Run the application:

```bash
python teams_mail_merge_app.py
```

2. **Setup Tab**: Read the instructions and navigate to the Settings tab to configure your API credentials.

3. **Settings Tab**: Enter your Azure AD application details:
   - Client ID
   - Tenant ID
   - Client Secret
   - Redirect URI (default: http://localhost:8000)
   - Click "Save Settings"

4. **Data Source Tab**: Upload your Excel or CSV file containing recipient information:
   - Click "Browse" to select your data file
   - Select the column containing recipient email addresses or Teams IDs
   - Click "Next"

5. **Message Template Tab**: Create your message template:
   - Use placeholders in the format `{ColumnName}` to insert personalized data
   - Use formatting buttons to add bold, italic, links, or mentions
   - Click "Next"

6. **Preview Tab**: Preview personalized messages for each recipient:
   - Use the navigation buttons to cycle through recipients
   - Review the personalized content
   - Click "Next"

7. **Send Messages Tab**: Send your messages:
   - Click "Sign In" to authenticate with Microsoft Teams
   - Set the delay between messages
   - Enable "Test Mode" to send all messages to yourself for testing
   - Click "Send Messages" to start the process

## Data Source Format

Your Excel or CSV file should contain columns for:
- Email addresses or Teams user IDs (required)
- Personalization fields (any additional data you want to include)

Example:
| Email | FirstName | Team | Project |
|-------|-----------|------|---------|
| user1@example.com | John | Marketing | Website |
| user2@example.com | Jane | Sales | Q2 Targets |

## Message Template Format

Create a message template using placeholders in curly braces that match your data source column names:

```
Hello {FirstName},

I wanted to reach out about the {Project} project. Your contribution to the {Team} team has been outstanding.

Could we schedule some time to discuss the next steps?

Thanks,
[Your Name]
```

## Troubleshooting

- **Authentication Issues**: Ensure your Azure AD app has the correct permissions and admin consent
- **User Not Found**: Verify that the email addresses in your data source are valid Teams users
- **Rate Limiting**: If you receive rate limiting errors, increase the delay between messages
- **Check Logs**: Review the application log file (`teams_mail_merge.log`) for detailed error information

## Security Note

This application stores your Azure AD application credentials in a local configuration file. Make sure to keep this file secure and do not share it with unauthorized users.
