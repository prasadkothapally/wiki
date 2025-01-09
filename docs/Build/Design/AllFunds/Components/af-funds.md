# Funds Microservice

<span dir="">Funds component is responsible to upload funds details. Once funds will be uploaded and will be validated. Then these funds will be stored into Database once validation will be done.</span>\
We can search funds by passing either fully match or partial match of text. \
\
**Upload:** This api can be used to upload excel containing funds details.\
\
**Search:** This api is used to search fund name by passing partial text or exact match fund name.\
\
**Filter:** This api is used to filter funds by passing Asset class type and Consistency factory.\
\
**Facts by ISIN:** This api is used to filter facts by isin.

# Interface upload

## api : /api/rest/funds/upload

## Request and Response of Upload funds

### Request

#### Request Body

<span dir="">We can upload excel file as funds details</span>.

| Content Type | Body | key | value |
|--------------|------|-----|-------|
| multipart/form-data | Excel file | file | excel file |

### Response

#### Response Body

| body | Headers |
|------|---------|
| JSON | accept=application/json |

# Interface search

## api : /api/funds/search

## Request and Response of search

### Request

#### Request Body

<span dir="">We can search fund by request param</span>

| request param |
|---------------|
| phrase |

### Response

#### Response Body

| body | Headers |
|------|---------|
| JSON | accept=application/json |

# Interface filter

## api : /api/funds/filter

## Request and Response of filter

### Request

#### Request Body

<span dir="">We can filter funds by passing asset class type and consistency factor as FilterRequest</span>

| Request name | body | Headers |  |
|--------------|------|---------|--|
| FilterRequest | JSON | accept=application/json |  |

### Response

#### Response

| Headers |
|---------|
| contentType=text/csv |

# Interface facts

## api : /api/funds/{isin}/facts

## Request and Response of facts

### Request

#### Request Body

<span dir="">We can fetch fatcs by isin</span>.

| request-param |
|---------------|
| isin |

### Response

#### Response Body

| Headers |
|---------|
| contentType=text/csv |

# Interface attributes

## api : /api/funds/{isin}/attributes

## Request and Response of attributes

### Request

#### Request Body

<span dir="">We can fetch attributes by isin</span>.

| request-param |
|---------------|
| fund-name |

### Response

#### Response Body

| Headers |
|---------|
| contentType=text/csv |

# Interface recommendation

## api : /api/rest/recommendation

## Request and Response

### Request

#### Request Body

<span dir="">We can get recommendations</span>

| Request name | body | Headers |  |
|--------------|------|---------|--|
| PortfolioRecommendationRequest | JSON | accept=application/json |  |

### Response

#### Response Body

| Request name | body | Headers |  |
|--------------|------|---------|--|
| PortfolioRecommendationResponse | JSON | accept=application/json |  |

# Diagrams

Data flow diagram

## Example diagram

```kroki-mermaid
flowchart TD
    A[Client] -->|uploading excel file\n of fund details|B(Fund upload API)
    B -->|uploading excel file| C[File Upload Service]
    C --> B
    B --> |parsing catalog|D[Catalog Excel Parser Service]
    D --> B
    B --> |calling fund service to \nstore funds in Database|E[Fund Service]
    E ==> |store funds| F[(Funds Database)]
    E ==> |store funds returns| F
    E ==> |validate funds \n stored procedure will be callded| F
```

# Persistence

## Postgres

| Aspect | Value |
|--------|-------|
| Database Engine | postgresql |
| Schema |  |
| Migrations | Yes / No |
| Charset | UTF-8 |

### Dictionary

#### Tables

| Table | Purpose |
|-------|---------|
| templates | Maintain all templates |
| notifications_audit | Maintain notification data |

#### Fields

| Table | Field | Purpose | Type | Size | Nullable | Keys |
|-------|-------|---------|------|------|----------|------|
| notifications_audit | id | Identifier | int |  | No | PK |
| notifications_audit | sender | notification sender | text | 255 | Yes |  |
| notifications_audit | receiver | notification receiver | text | 255 | Yes |  |
| notifications_audit | message | message | text | 255 | Yes |  |
| notifications_audit | createdDate | notification created date | date | 20 | Yes |  |

| Table | Field | Purpose | Type | Size | Nullable | Keys |
|-------|-------|---------|------|------|----------|------|
| templates | key | Identifier | text |  | No | PK |
| templates | description | template description | text | 255 | Yes |  |
| templates | type | notification type | text | 255 | Yes |  |
| templates | subject | email subject | text | 255 | Yes |  |
| templates | body | email body | text | 255 | Yes |  |
| templates | status | template status | text | 1 | Yes |  |

## Mongo

### Collections

#### Example

```json
```

# Build

| Aspect | Value |
|--------|-------|
| Artifacts |  |
| Location |  |

# Deployment

To be filled

# Security

To be filled

# Scalability

To be filled

# Resilience

To be filled