# Frontend Specification

## Product Summary
This frontend is a Korean freelancer invoice management application.
It supports authentication, onboarding, dashboard metrics, client management, invoice CRUD, invoice detail views, and reminder preset configuration.

## Route Map
- /login
- /signup
- /onboarding/profile
- /dashboard
- /clients
- /invoices
- /invoices/new
- /invoices/:id
- /invoices/:id/edit
- /settings/reminders

## Auth Expectations
- Public pages: login and signup
- Protected pages: all dashboard routes
- Session-based auth with cookie storage

## API Contracts
### Auth
- POST /api/auth/signup
- POST /api/auth/login
- POST /api/auth/logout
- POST /api/auth/password-reset

### Profile
- GET /api/profile
- PATCH /api/profile

### Clients
- GET /api/clients
- POST /api/clients
- PATCH /api/clients/:id
- DELETE /api/clients/:id

### Invoices
- GET /api/invoices
- POST /api/invoices
- GET /api/invoices/:id
- PATCH /api/invoices/:id
- POST /api/invoices/:id/status
- POST /api/invoices/:id/send-email
- GET /api/invoices/:id/pdf

### Reminder Presets
- GET /api/reminder-presets
- POST /api/reminder-presets
- PATCH /api/reminder-presets/:id
- DELETE /api/reminder-presets/:id

## Data Models
### Client
- id
- name
- email
- contactPhone
- memo
- createdAt

### InvoiceItem
- id
- description
- quantity
- unitPrice
- amount
- sortOrder

### Invoice
- id
- invoiceNumber
- clientId
- status: draft | sent | paid | overdue | cancelled
- issueDate
- dueDate
- currency
- subtotal
- taxRate
- taxAmount
- withholdingRate
- withholdingAmount
- total
- memo
- reminderPresetId
- createdAt
- updatedAt

### ReminderPreset
- id
- name
- isDefault
- rules

## Frontend State Requirements
- Invoice form recalculates totals in real time.
- Client search is debounced.
- Reminder preset preview updates live.
- Invoice detail page shows status history and reminder history.

## Error Handling
- Korean validation messages on all forms.
- Empty states for client and invoice lists.
- Loading skeletons on dashboard and list pages.

## External Services
- Email delivery provider for invoice send and reminders.
- PDF generation for invoice export.

## Assumptions
- Real backend must preserve the same request and response contracts as the mock frontend API layer.
- Reminder delivery is email-only in MVP.
