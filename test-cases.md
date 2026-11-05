### TC-001 - Get all products

**Endpoint:** GET /products
**Objectives:** Verify that the products endpoint returns a valid response containing a correctly structured list of products and pagination information.
**Preconditions:**  
- The DummyJSON API is reachable.
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send GET request to /products.
2. Verify the HTTP response status code.
3. Verify that the response Content-Type is JSON.
4. Verify that the response contains the expected pagination fields.
5. Validate the data types and values of the pagination fields.
6. Verify that the products field is a non-empty array.
7. Validate the structure and data types of the first product.

**Expected Results:**
- TC-001A - The response status code is `200 OK`.
- TC-001B - The response content-type is JSON.
- TC-001C - The response contains `products`, `total`, `skip` and `limit` fields. 
- TC-001D - The pagination fields contain valid numeric values. 
- TC-001E - The `products` array is not empty. 
- TC-001F - The returned product count does not exceed the values of `limit` and `total`. 
- TC-001G - The first product contains a numeric `id`, a non-empty `title`, and a numeric `price`.
**Execution Result:** PASS
**Checks passed:** 7/7
**Checks failed:** 0

### TC-002 - Limit Pagination

**Endpoint:** GET /products?limit=5
**Objectives:** Verify that the API respects the requested pagination limit.
**Preconditions:** 
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
GET /products?sortBy=title&order=desc

**Objective:** Verify that products are correctly sorted alphabetically by title in ascending/descending order.

**Test steps:**
1. Send a GET request with `sortBy=title` and `order=asc` or `order=desc`
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
- Product titles are sorted alphabetically in ascending/descending order.

**Execution Result:** PASS
**Checks Passed:** 5/5
**Checks Failed:** 0
**Notes:** 

### TC-009 - Get All Product Categories

**Endpoint:** GET /products/categories

**Objective:** Verify the products categories and the fields validity.

**Test Steps:** 
1. Send a GET request to /products/categories.
2. Verify the HTTP status code.
3. Verify that the response is a non-empty array.
4. Verify that the number of categories is valid and every category has a valid slug, name and URL.
5. Verify that there are no duplicate categories.

**Expected Results:** 
- TC-010A: Status code is 200
- TC-010B: Response is a non-empty array
- TC-010C: API returns 24 categories
- TC-010D: All categories have a valid slug
- TC-010E: All categories have a valid name
- TC-010F: All categories have a valid URL
- TC-010G: Category slugs are unique

**Execution Result:** PASS
**Checks Passed:** 7/7
**Checks Failed:** 0
**Notes:** 

### TC-010 - Get Products by Category

**Endpoint:** `GET /products/category/smartphones`

**Objective:** Verify that the API returns the products belonging to the requested category and that the returned product data is valid.

**Test steps:**
1. Send a GET request for the `smartphones` category.
2. Verify the HTTP status code.
3. Validate the response structure.
4. Verify pagination values.
5. Verify that the number of returned products matches the total.
6. Verify that all products belong to the `smartphones` category.
7. Validate product IDs, titles, and descriptions.
8. Verify that all product descriptions contain the word `smartphone`, regardless of letter case.

**Expected results:**
- TC-010A - HTTP status code is `200 OK`.
- TC-010B - Response contains a non-empty products array.
- TC-010C - Pagination fields are valid.
- TC-010D - All products are returned.
- TC-010E - Every product belongs to the `smartphones` category.
- TC-010F - Every product has a valid ID, non-empty title, and description.
- TC-010G - Every description contains the word `smartphone`.

**Execution Result:** PASS
**Checks Passed:** 7/7
**Checks Failed:** 0
**Notes:** 

### TC-011 - Product Creation

**Endpoint:** POST /products/add
**Objective:** 

**Test Steps:**
1. Send a POST request to `/products/add`.
2. Add the products fields.
3. Verify the status code.
4. Verify the response is valid JSON.
5. Verify that the response contains the valid input data.

**Expected Results:**
- TC-011A: Status code is 201 Created
- TC-011B: Response is valid JSON
- TC-011C: Response contains a numeric product ID
- TC-011D: Product title matches the request
- TC-011E: Product description matches the request
- TC-011F: Product category matches the request
- TC-011G: Product price matches the request
- TC-011H: Product stock matches the request
- TC-011I: Product brand matches the request

**Execution Result:** PASS
**Checks Passed:** 9/9
**Checks Failed:** 0
**Notes:**

### TC-012 – Response Time Validation

**Endpoint:** GET /products

**Objective:** Verify the response time of the API.

**Test Steps:**
1. Send a GET request to `/products'
2. Verify the status code of the request.
3. Verify that the response time is less than 500 ms
4. Verify that the response is JSON and contains products array that are not empty.

**Expected Results:**

- TC012A: Status code is 200

- TC-012B: Response time is less than 500ms
- TC-012C: Response body is valid JSON and contains products array
- TC-012D: Products array is not empty
