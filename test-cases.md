### TC-001 - Get all products
**Endpoint:** GET /products
##### Objectives: Verify the products endpoint response structure and data types.
##### Preconditions:  
- The API is reachable
- Postman is configured to send requests to the DummyJSON API.
##### Test Steps:
1. Send GET request to /products
2. Verify the HTTP response status
3. Verify that the response Content-Type is JSON.
4. 
 -TC-001A - Verify that the server responds as required. - PASS
 -TC-001B - Verify that the response is JSON. -PASS
 -TC-001C - Verify that the response contains the required top-level fields. - PASS
 -TC-001D - Verify the required data type of required fields. - PASS
 -TC-001E - Verify that the required array is a non-empty array. - PASS
 -TC-001F - Verify that the required array is consistent with the pagination. - PASS
 -TC-001G - Verify that the first object of the array has valid basic fields. - PASS
 Result: PASS 7/7

TC-002 - Limit Pagination
 -TC-002A - Vewrify that the server responds as required. - PASS
 -TC-002B - Confirm that the pagination limit to is set to 5. - PASS
 -TC-002C - Verify that the limnit is respected in the response. - PASS
 -TC-002D - Confirm that no object is skipped. - PASS
 -TC-002E - Verify that the total number of objects is valid. - PASS
 -TC-002F - Verify that the returned entries contain the required fields which have valid values. - PASS
