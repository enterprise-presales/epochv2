# Scenario-Based EMR Demonstration

This document explains how to use the scenario-based functionality in the EMR demonstration mockup.

## Overview

The EMR demonstration mockup now supports loading predefined scenarios via URL parameters. This allows for consistent demonstrations of different patient cases and exam types without needing to manually enter data.

## Available Scenarios

Currently, there are 2 scenarios available:

1. **Pediatric Well Visit** (`pediatric-well-visit`) - A routine well-child visit for a 26-month-old patient
2. **Comprehensive Eye Examination** (`eye-examination`) - An eye exam for a patient with cataracts and dry eye syndrome

## How to Use Scenarios

### URL Parameters

The application supports the following URL parameters:

- `scenario`: Specifies which scenario to load (e.g., `pediatric-well-visit`, `eye-examination`)
- `examType`: Specifies which exam type to display (e.g., `Clinic Visit`, `Eye Exam`, `Flowsheets`, `Wrap Up`, `Procedure Note`)

### Example URLs

- `/?scenario=pediatric-well-visit` - Loads the pediatric well visit scenario with its default exam type
- `/?scenario=eye-examination` - Loads the eye examination scenario with its default exam type
- `/?scenario=pediatric-well-visit&examType=Flowsheets` - Loads the pediatric well visit scenario with the Flowsheets exam type

### Behavior

When a scenario is loaded via URL parameter:

1. Patient demographics are automatically populated in the sidebar and header
2. Clinical data is loaded into the Progress Notes section
3. The EMR is automatically synced with the scenario data
4. The appropriate exam type is selected based on the scenario or URL parameter

If no scenario parameter is specified, the application will use default data and rely on clipboard input as before.

## Testing Scenarios

To test a scenario:

1. Start the application with `npm run dev`
2. Navigate to `http://localhost:3000/?scenario=pediatric-well-visit` (or any other scenario ID)
3. Verify that the patient demographics, progress notes, and exam section are populated with the scenario data

## Adding New Scenarios

To add new scenarios:

1. Edit the `public/scenarios.json` file
2. Add a new scenario object to the `scenarios` array following the existing format
3. Ensure each scenario has a unique `id` field
4. Include all required patient and clinical data fields

## Scenario Data Structure

Each scenario in the `scenarios.json` file follows this structure:

```json
{
  "id": "unique-scenario-id",
  "name": "Human-Readable Scenario Name",
  "examType": "Default Exam Type",
  "patientData": {
    "patientName": "Last, First",
    "patientDOB": "MM/DD/YYYY",
    "visitDate": "MM.DD.YYYY",
    "providerName": "Dr. Provider Name",
    "interpreterNeeded": "Yes/No/Sometimes",
    "insurance": "Insurance Provider",
    "preferredLab": "Lab Name",
    "previousExam": "Time period",
    "nextVisit": "MM/DD/YYYY"
  },
  "clinicalData": {
    "historyOfPresentIllness": "Text content...",
    "physicalExamination": "Text content...",
    "results": "Text content...",
    "assessmentPlan": "Text content...",
    "attestation": "Text content...",
    "flowsheet": { /* JSON object with flowsheet data */ },
    "eyeExam": { /* JSON object with eye exam data */ },
    "orders_list": { /* JSON object with orders data */ },
    "problems_list": { /* JSON object with problems data */ },
    "education_instructions": "Text content...",
    "procedure_note": "Text content...",
    "med_recon": "Text content..."
  }
}
```

## Future Enhancements

Potential future enhancements for the scenario system:

1. Add more scenarios covering different medical specialties and conditions
2. Support for scenario workflows that guide users through multiple exam types
3. Add a UI for selecting scenarios without URL parameters
4. Support for saving and loading custom scenarios