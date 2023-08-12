
# Team Dashboard Automation

## Overview
This automation system is developed for the Google Spreadsheet titled **Planilla_Empleados_WG**. Its main aim is to seamlessly update a central dashboard sheet from various team sheets and generate an email report based on specific dates. The data in team sheets is dynamically populated from Google Form submissions processed by Zapier.

## Architecture

### Google App Script:
- Custom functions to handle various tasks, e.g., updating the dashboard and sending the email report.
- Custom UI menu items that trigger these functions.

### Google Spreadsheet:
- Sheets for different teams, populated from Google Form submissions.
- A central "Dashboard" sheet that consolidates data from all team sheets.
- "Teams management" sheet for team info.

### HTML Dialog:
- A simple interface to collect start and end dates from the user before generating the email report.

## Code Breakdown:

### Menu Creation:
```javascript
function onOpen() {
   var ui = SpreadsheetApp.getUi();
   ui.createMenu('Custom Menu')
     .addItem('Send report', 'showDatePrompt')
     .addItem('Update dashboard', 'copyDataToDashboard')
     .addToUi();
}
```
This function adds a custom menu to the spreadsheet UI. It includes two items:
- Send report: Opens the date prompt dialog.
- Update dashboard: Updates the dashboard with the latest team data.

### Dashboard Updation:
The `copyDataToDashboard()` function performs the core logic. It:
- Extracts team member data.
- Clears the dashboard.
- Sets the header.
- Loops through each team sheet and populates the dashboard.
- Colors the rows for clarity.

### Date Prompt and Email Report:
- `showDatePrompt()`: Displays the HTML dialog to collect start and end dates.
- `sendReportEmail(startDate, endDate)`: Generates an email report based on the provided dates, sending it to the specified email address.
- `getDirectLink(url)`: Converts Google Drive shareable link to direct image link.

### HTML Dialog (DatePrompt.html):
A simple dialog with two date input fields and a button. It uses JavaScript to validate the date entries and initiate the email report generation.

## Instructions for Users:

### Team Sheet Data:
**English:** 
- Ensure that the Google Form is live and collecting responses.
- Verify that the Zapier integration is active and sending data to the correct team sheet.

**Spanish:** 
- Para el correcto funcionamiento, por favor seguir los patrones sobre como actualizar la información de equipos.
- Siempre nombrar en una celda el nombre del equipo, "Team" seguido del numero del equipo. Si es posible no elimine el encabezado "Team" solo actualice los nombres.
- Este espacio entre un Team y el otro siempre debe estar separando los equipos.

### Updating Dashboard:

**English:** 
- The Dashboard will automatically update every 30 minutes. Still, it can also be updated manually by running the "Update Dashboard" function in the "Custom Menu" in the top right of the spreadsheet.

**Spanish:** 
- El Dashboard se actualizara automáticamente cada 30 minutos, pero también se puede actualizar manualmente ejecutando la función "Update Dashboard" en el "Custom Menu" en la parte superior derecha del spreadsheet.

### Team Member Form Entry:

**English:** 
- Ensure that each team member filling out the form, when entering the assigned team number, only enters the number without any letters. If the team is "Team1", they should only enter the number "1", or the form information will not reach this spreadsheet.

**Spanish:** 
- Asegurarse de que cada miembro de un equipo que llene el formulario, al ingresar el número de equipo asignado solo ingrese el número sin ninguna letra. Si el equipo es "Team1", solamente debe ingresar el número "1" o la información del formulario no llegará a esta hoja de cálculo.

**Note:** Always back up your data before making major changes.
