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

## Project Structure
`
rest-api-testing-postman/
├── README.md
├── postman/
├── test-cases/
├── bug-reports/
└── test-results/
`

## Test Scope

The planned test coverage includes:

* Product list and individual product retrieval
* Response structure and data type validation
* Search and empty search results
* Pagination
* Sorting
* Field selection
* Product category filtering
* Negative scenarios involving invalid resource identifiers
* Product creation
* Response time validation

## Test Execution

Test cases will be executed using Postman. Actual results, execution status, and supporting evidence will be documented after execution.

No test execution results are reported until the corresponding tests have been run.

## Results Summary

* Planned test cases: 12
* Executed test cases: 12
* Passed: 12
* Failed: 0
* Blocked: 0

## Limitations

DummyJSON is a demonstration API. Some write operations may simulate changes instead of persisting them. Results must be interpreted according to the API documentation and observed behavior.

## Disclaimer

This is an independent learning project. It is not affiliated with or endorsed by DummyJSON or Postman.

