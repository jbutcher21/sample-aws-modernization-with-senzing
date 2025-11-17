# Customer Data Schema

**File:** customers.csv  
**Total Records:** 120  
**Entity Types:** Person (I) and Organization (C)

## Field Analysis

### Core Identity Fields

| Field | Type | Population | Sample Values |
|-------|------|------------|---------------|
| **customer_id** | Integer | 100% (120/120) | 1001, 1002, 2011, 2031 |
| **customer_name** | String | 100% (120/120) | "Smith, Robert", "Kusha, Edward", "Hajah Mamunah (Jln Pisang)" |
| **customer_type** | String | 100% (120/120) | "I" (Individual/Person: 114), "C" (Company/Organization: 6) |

### Demographics

| Field | Type | Population | Sample Values |
|-------|------|------------|---------------|
| **gender** | String | 17% (20/120) | "M", "F", "Male", "Female", "U", "Unknown" |
| **dob** | String | 53% (64/120) | "12/11/1978", "3/1/1970", "Mar 1 1970", "1997-11-12" |

### Address Information

| Field | Type | Population | Sample Values |
|-------|------|------------|---------------|
| **address** | String | 61% (73/120) | "123 Main Street, Las Vegas NV 89132", "1304 Poppy Hills Dr" |
| **city** | String | 35% (42/120) | "Las Vegas", "Blacklick", "San Francisco", "Toronto" |
| **state** | String | 32% (38/120) | "NV", "OH", "CA", "OHIO", "Nevada" |
| **zip_code** | String | 35% (42/120) | "89132", "43004", "94105", "M1S 1T4" |
| **country** | String | 15% (18/120) | "US", "USA", "Germany", "Singapore", "China" |

### Contact Information

| Field | Type | Population | Sample Values |
|-------|------|------------|---------------|
| **phone** | String | 18% (22/120) | "702-919-1300", "512-353-8633", "(807) 422-9031", "+39 0352 6553537" |
| **email** | String | 38% (46/120) | "bsmith@work.com", "Kusha123@hmail.com", "info@ca-state.gov" |

### Government Identifiers (Dynamic Pattern)

| Field | Type | Population | Sample Values |
|-------|------|------------|---------------|
| **id_type** | String | 30% (36/120) | "SSN", "PASSPORT", "DRIVERS_LICENSE", "NATIONAL_ID" |
| **id_number** | String | 30% (36/120) | "294-66-9999", "112233", "10251111", "832721" |
| **id_country** | String | 30% (36/120) | "US", "NV", "CA", "Hong Kong", "China" |

### Business/Operational Data

| Field | Type | Population | Sample Values |
|-------|------|------------|---------------|
| **registration_date** | String | 83% (100/120) | "1/2/18", "3/10/17", "1997-11-12", "3/15/1992" |
| **account_status** | String | 83% (100/120) | "Active", "Inactive", "Terminated" |
| **account_balance** | Integer | 75% (90/120) | 100, 200, 500, 900 |
| **customer_tier** | String | 8% (10/120) | "Platinum", "Gold", "Silver" |

## Data Quality Observations

### Entity Distribution
- **Person Records (I):** 114 (95%)
- **Organization Records (C):** 6 (5%)

### Identifier Coverage
- **30% have government IDs** with type/number/country pattern
- **ID Types:** SSN (most common), PASSPORT, DRIVERS_LICENSE, NATIONAL_ID
- **Countries:** US, Canada, Germany, Hong Kong, China

### Address Patterns
- **Structured addresses:** Some in single field, others split across components
- **International addresses:** US, Canada, Germany, Singapore, Cambodia, China
- **Format variations:** Street abbreviations (St/Street, Dr/Drive, Ln/Lane)

### Name Variations
- **Person names:** Last, First format predominant
- **Variations:** Nicknames, abbreviations, spelling differences
- **International names:** Chinese characters, Khmer script
- **Organizations:** Company names with location identifiers

### Date Formats
- **DOB formats:** MM/DD/YYYY, DD/MM/YYYY, DD-MMM-YY, YYYY-MM-DD
- **Registration dates:** M/D/YY, MM/DD/YYYY formats

### Contact Information
- **Phone formats:** Various (XXX-XXX-XXXX, (XXX) XXX-XXXX, international +XX)
- **Email patterns:** Standard format, some with display names

## Mapping Considerations

1. **Entity Type Handling:** Conditional mapping based on customer_type (I vs C)
2. **Dynamic Identifiers:** Map id_type/id_number/id_country as a group
3. **Address Normalization:** Handle both structured and unstructured addresses
4. **Date Standardization:** Multiple date formats need parsing
5. **Name Variations:** Consider fuzzy matching for similar names
6. **International Data:** Multi-language and character set support needed