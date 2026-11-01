### TC-001 - Get all products

##### Endpoint: GET /products
##### Objectives: Verify the products endpoint response structure and data types.
##### Preconditions:  
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

##### Test Steps:
1. Send GET request to /products
2. Verify the HTTP response status
3. Verify that the response Content-Type is JSON.
4. Verify that pagination fields have the expected data types and validate values
5. Verify that "products" is a non-empty array.
6. Verify that the returned product count does not exceed "limit" and does not exceed "total"
7. Verify that the first product contains valid "id", "title" and "price" fields.

##### Expected Results:
- TC-001A - The response status is 200 OK.
- TC-001B - The response content-type is JSON.
- TC-001C - The response contains "products", "total", "skip" and "limit" fields. 
- TC-001D - The pagination fields are numeric and have valid values. 
- TC-001E - The "products" array is not empty. 
- TC-001F - The returned product count does not exceed the values of "limit" and "total". 
- TC-001G - Verify that the first object of the "products" array has valid "id", "title" and "price" fields.
##### Execution Result: PASS
##### Checks passed: 7/7
##### Checks failed: 0
##### Notes: Results are base on the recorded execution against the DummyJSON API.

### TC-002 - Limit Pagination

##### Endpoint: GET /products?limit=5
##### Objective: Verify that the API respects the requested pagination limit.
##### Preconditions:
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

##### Test Steps:
1. Send a GET request to /products?limit=5.
2. Verify the HTTP response status.
3. Validate the pagination fields in the response body.
4. Verify the number and structure of returned products.

##### Expected Results:
- TC-002A - The response status is 200 OK.
- TC-002B - The limit field equals 5.
- TC-002C - The limit is respected in the response. 
- TC-002D - The "skip" fields equals 0.
- TC-002E - The "total" field is numeric and is greater than or equal to the number of returned products. 
- TC-002F - Each returned product contains a numeric id, a non-empty string title, and a numeric price.
##### Execution Result: PASS
##### Checks passed: 6/6
##### Checks failed: 0
##### Notes: Results are base on the recorded execution against the DummyJSON API.

### TC-003 - Get Product by ID

##### Endpoint: GET /products/1
##### Objective: Verify that the returned product matches the product ID.
##### Preconditions:
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

##### Test Steps:
1. Send a GET request to /products/1.
2. Verify the HTTP response status.
3. Verify that the returned product ID matches the requested ID (1).
4. Verify the structure and the validity of the returned product's fields. 

##### Expected Results:
- TC-003A - The response status code is 200.
- TC-003B - The response is JSON.
- TC-003C - The returned product ID matches the requested ID (1).
- TC-003D - The product title is a non-empty string. 
- TC-003E - The product price is numeric.
- TC-003F - The product description is a non-empty string. 
- TC-003G - The product category is a non-empty string.
##### Execution Result: PASS
##### Checks passed: 7/7
##### Checks failed: 0
##### Notes: Results are base on the recorded execution against the DummyJSON API.

### TC-004 - Non-existing Product ID

##### Endpoint: GET /products/999999
##### Objective: Verify the API behavior when a requested product does not exist.
##### Preconditions: 
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

##### Test Steps:
1. Send a GET request to /products/999999.
2. Verify the HTTP response status.
3. Verify that the response content-type is JSON.
4. Verify the response error message.

##### Expected Results:
- TC-004A - The response status code is 404.
- TC-004B - The response is JSON.
- TC-004C - The response contains a non-empty error message.
- TC-004D - The error message contains the requested id value.
- TC-004E - The error message matches the expected result.
##### Execution Result: PASS
##### Checks passed: 5/5
##### Checks failed: 0
##### Notes: Results are base on the recorded execution against the DummyJSON API.

### TC-005 - Product Search

##### Endpoint: GET /products/search?q=phone
##### Objective: Verify the search functionality and the structure of the response.
##### Preconditions:
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

##### Test Steps:
1. Send a GET request to /products/search?q=phone
2. Verify the HTTP response status.
3. Verify that the response content-type is JSON.
4. Verify the validity of the "Total" field.
5. Identify the search term in the description or title of the returned product/products.

##### Expected Results:
- TC-005A - The response status code is 200.
- TC-005B - The response is JSON.
- TC-005C - "Products" is an array.
- TC-005D - The value of "Total" is a valid non-negative number.
- TC-005E - The value of "Total" matches the number of returned products.
- TC-005F - The search returns at least one product whose title or description contains the search term.

##### Execution Results: PASS
##### Checks Passed: 6/6
##### Checks Failed: 0
##### Notes: Results are base on the recorded execution against the DummyJSON API.

### TC-006 - Search Without Results

##### Endpoint: GET /products/search?q=qa-no-match-987654321
##### Objective: Verify how the API handles a search with no results
##### Preconditions:
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

##### Test Steps:
1. Send a GET request to /products/search?q=qa-no-match-987654321
2. Verify the HTTP response status.
3. Verify that the response content-type is JSON.
4. Verify that "products" is an empty array.
5. Verify that "total", "skip" and "limit" equal to 0.

##### Expected Results:
- TC-006A - The response status code is 200.
- TC-006B - The response is JSON.
- TC-006C - "Products" is an empty array.
- TC-006D - "Total" equals 0.
- TC-006E - "Skip" equals 0.
- TC-006F - "Limit" equals 0.

##### Execution Results: PASS
##### Checks Passed: 6/6
##### Checks Failed: 0
##### Notes: Results are base on the recorded execution against the DummyJSON API.

### TC-007 - Pagination with Skip

##### Endpoint: GET /products?limit=5&skip=5
##### Objective: Verify that the API correctly returns the next page of products when the skip parameter is applied, without duplicating products from the previous page.
##### Preconditions:
- TC-002 has been executed successfully.
- The first page product IDs have been saved in the Postman collection variable firstPageProductIds.

##### Test Steps:
1. Execute TC-002 (GET /products?limit=5) to retrieve and save the first page product IDs.
2. Execute TC-007 (GET /products?limit=5&skip=5) to retrieve the second page.
3. Verify the response status and pagination parameters.
4. Verify that exactly 5 products are returned.
5. Compare the returned product IDs with the IDs saved from the first page.
6. Verify that no products are duplicated between the two pages.

##### Expected Results:
- The response status code is 200 OK.
- The limit field equals 5.
- The skip field equals 5.
- Exactly 5 products are returned.
- First-page product IDs are available for comparison.
- No product IDs overlap between the first and second pages.

##### Execution Results: PASS
##### Checks Passed: 6/6
##### Checks Failed: 0
##### Notes: TC-007 uses a Postman collection variable to dynamically compare the results of the two requests.

### TC-008 - Product Sorting

**Endpoint:** GET /products?sortBy=title&order=asc

**Objective:** Verify that products are correctly sorted alphabetically by title in ascending order.

**Test steps:**
1. Send a GET request with `sortBy=title` and `order=asc`.
2. Verify the HTTP status code.
3. Verify pagination parameters.
4. Verify that the response contains products.
5. Compare the returned titles against an alphabetically sorted copy.
6. Verify that every product has a non-empty title.

**Expected results:**
- HTTP status code is `200 OK`.
- Products are returned in an array.
- `limit` equals 30 and `skip` equals 0.
- All products have non-empty titles.
- Product titles are sorted alphabetically in ascending order.

**Execution Result:** PASS
**Checks Passed:** 5/5
**Checks Failed:** 0
**Notes:** 
