# REST API Testing with Postman

## Project Overview

This is a personal API testing project focused on testing the DummyJSON Products API using Postman.

The purpose of this project is to practice REST API testing, validate API responses, write automated assertions using JavaScript, and document test execution results.

The project covers positive and negative scenarios, data validation, pagination, sorting, product search, category filtering, product creation simulation, and basic response-time validation.

## Tools and Technologies

* Postman - API request execution and automated testing
* JavaScript - Writing test scripts and resonse assertions
* REST API - HTTP methods and endpoint testing
* JSON - Request payloads and response validation
* Git and GitHub - Version control and project documentation

## API Under Test

DummyJSON provides sample REST API endpoints for development and testing.

* API base URL: `https://dummyjson.com`
* Documentation: https://dummyjson.com/docs/products

## Test Scope
The project contains 12 test cases covering the following scenarios:
| Test Case | Description | Method | 
| --- | --- | ---|
| TC-001 | Get All Products | GET |
| TC-002 | Limit Products | GET |
| TC-003 | Get Ptoduct by ID | GET |
| TC-004 | Get Non-existing Product | GET |
| TC-005 | Search Products | GET |
| TC-006 | Search Without Results | GET |
| TC-007 | Pagination with Skip | GET |
| TC-008 | Product Sorting | GET |
| TC-009 | Get All Product Categories | GET |
| TC-010 | Get Products by Category | GET | 
| TC-011 | Product Creation | POST |
| TC-012 | Response Time Validation | GET |

## Testing Areas

- HTTP status code validation
- JSON response structure and data type validation
- Positive and negative testing
- Product data validation
- Search functionality
- Pagination and duplicate detection
- Ascending and descending sorting
- Product category validation
- POST request and response validation
- Basic response-time validation

## Test Execution Results

| Metric | Results |
| --- | --- |
| Total Test Cases | 12 |
| Total Assertions | 76 | 
| Passed Assertions | 76 | 
| Failed Assertions | 0 |
| Pass Rate | 100% |

For Detailed test steps, expected results, and execution results, see `test-cases.md`.

## Project Structure
```
rest-api-testing-postman/
├── README.md
├── postman/DummyJSON-Products-API.postman_collection.json
├── test-cases/test-cases.md
└── test-results/postman-run-results.json
```
## Limitations

DummyJSON is a demonstration API. Some write operations may simulate changes instead of persisting them. Results must be interpreted according to the API documentation and observed behavior.

## Disclaimer

This is an independent learning project. It is not affiliated with or endorsed by DummyJSON or Postman.

