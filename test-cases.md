### TC-001 - Get all products

**Endpoint:** `GET /products`

**Objectives:** Verify that the products endpoint returns a valid response containing a correctly structured list of products and pagination information.

**Preconditions:**  
- The DummyJSON API is reachable.
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send GET request to `/products`.
2. Verify the HTTP response status code.
3. Verify that the response Content-Type is JSON.
4. Verify that the response contains the expected pagination fields.
5. Validate the data types and values of the pagination fields.
6. Verify that the `products` field is a non-empty array.
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

**Endpoint:** `GET /products?limit=5`

**Objectives:** Verify that the API respects the requested pagination limit.

**Preconditions:** 
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send a `GET` request to `/products?limit=5`.
2. Verify the HTTP response status.
3. Validate the pagination fields.
4. Verify that exactly five products are returned.
5. Validate the basic structure and data types of each returned product.
6. Save the returned product IDs in a Postman collection variable for use in TC-007.

**Expected Results:**
- TC-002A - The response status is 200 OK.
- TC-002B - The `limit` field equals 5.
- TC-002C - The limit is respected in the response. 
- TC-002D - The `skip` fields equals 0.
- TC-002E - The `total` field is numeric and is greater than or equal to the number of returned products. 
- TC-002F - Each returned product contains a numeric id, a non-empty string title, and a numeric price.

**Execution Result:** PASS

**Checks passed:** 6/6

**Checks failed:** 0

### TC-003 - Get Product by ID

**Endpoint:** `GET /products/1`

**Objective:** Verify that the returned product matches the product ID.

**Preconditions:**
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send a `GET` request to `/products/1`.
2. Verify the HTTP response status.
3. Verify that the response is valid JSON.
4. Verify that the returned product ID matches the requested ID.
5. Validate the required product fields and their data types.

**Expected Results:**
- TC-003A - The response status code is `200 OK`.
- TC-003B - The response is JSON.
- TC-003C - The returned product ID matches the requested ID (1).
- TC-003D - The product title is a non-empty string. 
- TC-003E - The product price is numeric.
- TC-003F - The product description is a non-empty string. 
- TC-003G - The product category is a non-empty string.

**Execution Result:** PASS

**Checks passed:** 7/7

**Checks failed:** 0

### TC-004 - Non-existing Product ID

**Endpoint:** `GET /products/999999`

**Objective:** Verify the API behavior when a requested product does not exist.

**Preconditions:**
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send a `GET` request to `/products/999999`.
2. Verify the HTTP response status code.
3. Verify that the response content-type is JSON.
4. Verify that the response contains a meaningful error message.
5. Validate that the error message references the requested product ID.

**Expected Results:**
- TC-004A - The response status code is `404 Not Found`.
- TC-004B - The response is JSON.
- TC-004C - The response contains a non-empty error message.
- TC-004D - The error message contains the requested id value.
- TC-004E - The error message matches the expected result.

**Execution Result:** PASS

**Checks passed:** 5/5

**Checks failed:** 0

### TC-005 - Product Search

**Endpoint:** `GET /products/search?q=phone`

**Objective:** Verify the search functionality and the structure of the response.

**Preconditions:**
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send a `GET` request to `/products/search?q=phone`.
2. Verify the HTTP response status code.
3. Verify that the response content-type is JSON.
4. Verify the validity of the `products` array and `Total` field.
5. Verify that at least one returned product contains the search term in its title or description.

**Expected Results:**
- TC-005A - The response status code is `200 OK`.
- TC-005B - The response is valid JSON.
- TC-005C - The `products` field is an array.
- TC-005D - The value of `Total` is a valid non-negative number.
- TC-005E - The value of `Total` matches the number of returned products.
- TC-005F - At least one returned product has the search term `phone` in its title or description (case-insensitive).

**Execution Result:** PASS

**Checks passed:** 6/6

**Checks failed:** 0

### TC-006 - Search Without Results

**Endpoint:** `GET /products/search?q=qa-no-match-987654321`

**Objective:** Verify how the API handles a search with no results

**Preconditions:**
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.

**Test Steps:**
1. Send a `GET` request to `/products/search?q=qa-no-match-987654321`.
2. Verify the HTTP response status code.
3. Verify that the response content-type is JSON.
4. Verify that `products` array is empty.
5. Verify that `total`, `skip` and `limit` equal to 0.

**Expected Results:**
- TC-006A - The response status code is `200 OK`.
- TC-006B - The response is valid JSON.
- TC-006C - `Products` is an empty array.
- TC-006D - `Total` equals 0.
- TC-006E - `Skip` equals 0.
- TC-006F - `Limit` equals 0.

**Execution Result:** PASS

**Checks passed:** 6/6

**Checks failed:** 0

### TC-007 - Pagination with Skip

**Endpoint:** `GET /products?limit=5&skip=5`

**Objective:** Verify that the API correctly returns the next page of products when the skip parameter is applied, without duplicating products from the previous page.

**Preconditions:**
- TC-002 has been executed successfully.
- The first page product IDs have been saved in the Postman collection variable firstPageProductIds.

**Test Steps:**
1. Execute TC-002 (`GET /products?limit=5`) to retrieve and save the first page product IDs.
2. Send a `GET` request to `/products?limit=5&skip=5`.
3. Verify the HTTP response status code and pagination parameters.
4. Verify that exactly five products are returned.
5. Compare the returned product IDs with the IDs saved from the first page.
6. Verify that no products are duplicated between the two pages.

**Expected Results:**
- TC-007A: The response status code is `200 OK`.
- TC-007B: The response is valid JSON.
- TC-007C: The `limit` field equals 5.
- TC-007D: The `skip` field equals 5.
- TC-007E: Exactly 5 products are returned.
- TC-007F: The first-page product IDs are available in the collection variable for comparison.
- TC-007G: No product IDs overlap between the first and second pages.

**Execution Result:** PASS

**Checks passed:** 7/7

**Checks failed:** 0

### TC-008 - Product Sorting

**Endpoint:** `GET /products?sortBy=title&order=asc`

**Objective:** Verify that products are correctly sorted alphabetically by title in ascending order.

**Test steps:**
1. Send a GET request with `sortBy=title` and `order=asc`.
2. Verify the HTTP status code.
3. Verify pagination parameters.
4. Verify that the response contains products.
5. Compare the returned titles against an alphabetically sorted copy.
6. Verify that every product has a non-empty title.

**Expected results:**
- TC-008A: HTTP status code is `200 OK`.
- TC-008B: Products are returned in an array.
- TC-008C: `limit` equals 30 and `skip` equals 0.
- TC-008D: Product titles are sorted alphabetically in ascending/descending order.
- TC-008E: All products have non-empty titles.

**Execution Result:** PASS

**Checks Passed:** 5/5

**Checks Failed:** 0

### TC-009 - Get All Product Categories

**Endpoint:** `GET /products/categories`

**Objective:** Verify that the API returns a valid list of product categories and that each category contains the expected fields.

**Preconditions:**
- The DummyJSON API is reachable.
- Postman is configured to send requests to the API.

**Test Steps:** 
1. Send a `GET` request to `/products/categories`.
2. Verify the HTTP status code.
3. Verify that the response is a non-empty array.
4. Verify that the number of categories is valid and every category has a valid slug, name and URL.
5. Verify that there are no duplicate categories.

**Expected Results:** 
- TC-010A: The response status code is `200 OK`.
- TC-010B: The response is a non-empty array.
- TC-010C: The API returns 24 categories.
- TC-010D: Every category has a valid, non-empty slug.
- TC-010E: Every category has a valid, non-empty name.
- TC-010F: Every category has a valid URL.
- TC-010G: Category slugs are unique.

**Execution Result:** PASS

**Checks Passed:** 7/7

**Checks Failed:** 0 

### TC-010 - Get Products by Category

**Endpoint:** `GET /products/category/smartphones`

**Objective:** Verify that the API returns the products belonging to the requested category and that the returned product data is valid.

**Preconditions:**

- The DummyJSON API is reachable.
- Postman is configured to send requests to the API.
- The smartphones category exists.

**Test steps:**
1. Send a `GET` request for the `smartphones` category.
2. Verify the HTTP status code.
3. Verify that the response contains a non-empty products array.
4. Verify pagination values.
5. Verify that the number of returned products matches the `total` value.
6. Verify that all products belong to the `smartphones` category.
7. Validate product IDs, titles, and descriptions.
8. Verify that all product descriptions contain the word `smartphone`, regardless of letter case.

**Expected results:**
- TC-010A - The response HTTP status code is `200 OK`.
- TC-010B - The response contains a non-empty `products` array.
- TC-010C - The pagination fields are valid.
- TC-010D - The number of returned products matches the `total` value.
- TC-010E - Every product belongs to the `smartphones` category.
- TC-010F - Every product has a valid ID, non-empty title and description.
- TC-010G - Every description contains the word `smartphone`.

**Execution Result:** PASS

**Checks Passed:** 7/7

**Checks Failed:** 0

### TC-011 - Product Creation

**Endpoint:** `POST /products/add`

**Objective:** Verify that the API accepts a valid product creation request and returns a response containing the submitted product data and a generated product ID. 

**Test Data:**
`{
    "title": "Asus ROG Phone",
    "description": "Powerfull smartphone created for mobile gaming",
    "category": "smartphones",
    "price": 1299.99,
    "stock": 23,
    "brand": "Asus"
}`

**Test Steps:**
1. Send a `POST` request to `/products/add` with the test data above.
2. Verify the HTTP response status code.
3. Verify that the response is valid JSON.
4. Verify that the response contains a numeric product ID.
5. Compare the returned product fields with the submitted request data.

**Expected Results:**
- TC-011A: The response status code is `201 Created`.
- TC-011B: The response is valid JSON.
- TC-011C: The response contains a numeric product ID.
- TC-011D: The returned product title matches the submitted title.
- TC-011E: The returned product description matches the submitted descriprion.
- TC-011F: The returned product category matches the submitted category.
- TC-011G: The returned product price matches the submitted price.
- TC-011H: The returned product stock matches the submitted stock.
- TC-011I: The returned product brand matches the submitted brand.

**Execution Result:** PASS

**Checks Passed:** 9/9

**Checks Failed:** 0

### TC-012 – Response Time Validation

**Endpoint:** `GET /products`

**Objective:** Verify that the API responds within the defined response-time threshold while returning a valid products response.

**Prerequisites:**
- The DummyJSON API is reachable
- Postman is configured to send requests to the API.

**Test Steps:**
1. Send a `GET` request to `/products`.
2. Verify the HTTP response status code.
3. Measure the response time and compare it against the defined threshold of 500 ms.
4. Verify that the response is valid JSON.
5. Verify that the response contains a non-empty products array.

**Expected Results:**

- TC-012A: The response status code is `200 OK`.
- TC-012B: The response time is less than 500 ms.
- TC-012C: The response body is valid JSON and contains a `products` array.
- TC-012D: The `products` array is not empty.

**Execution Result:** PASS

**Checks passed:** 4/4

**Checks failed:** 0

**Notes:**
- The 500 ms threshold is a project-defined target, not an official DummyJSON performance SLA. This test validates the response time of an individual request and does not represent load or stress testing.
