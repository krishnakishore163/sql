# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).

![SQL Assignment1 drawio](https://github.com/krishnakishore163/sql/assets/166779922/2e7f1918-b7f4-43cb-be4e-55a585dc33f6)



## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.

![SQL Assignment2 drawio](https://github.com/krishnakishore163/sql/assets/166779922/d70dc778-de0b-4a25-a6a1-6f3d1695eaa6)


## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

_Hint, search type 1 vs type 2 slowly changing dimensions._

Bonus: Are there privacy implications to this, why or why not?
```
Your answer...
```
1. Overwrite (Type 1 Slowly Changing Dimension):
In this architecture, whenever there is a change in the customer's address, the existing record in the CUSTOMER_ADDRESS table is updated with the new address information. There is no retention of historical data, the old address information is replaced by the new address details.
Columns: CUSTOMER_ID(PRIMARY KEY and FOREIGN KEY), ADDRESS1, ADDRESS2, CITY, PROVINCE, COUNTRY, LAST_UPDATED_DATE
Only the current address information is stored in this architecture, with no history of changes retained.
This architecture simplifies the data model but does not provide historical tracking of address changes.
2. Retain Changes (Type 2 Slowly Changing Dimension):
In this architecture, whenever there is a change in the customer's address, a new record is added to the CUSTOMER_ADDRESS table with a new primary key (ADDRESS_ID). This new record contains the updated address information along with the start and end dates indicating the validity period of the address.
Columns: ADDRESS_ID (PRIMARY KEY), CUSTOMER_ID (FOREIGN KEY), ADDRESS, CITY, STATE, COUNTRY, START_DATE, END_DATE, LAST_UPDATED_DATE
This architecture retains historical information about customer addresses, allowing the store to track changes over time.
Type 2 Slowly Changing Dimension (Retain Changes) is suitable for the first architecture, while Type 1 Slowly Changing Dimension (Overwrite) is suitable for the second architecture.
Privacy Implications:
Storing historical address data (Type 2) without proper security measures can pose privacy risks. Customers might be uncomfortable with their past addresses being available, especially if they have moved for privacy or security reasons. On the other hand, replacing old address data (Type 1) can also have privacy concerns if the old data is not securely removed. If the old addresses are still stored elsewhere in the system, they could potentially be accessed, creating privacy concerns.
In both cases, it is important for the store to implement appropriate data protection measures to ensure customer privacy and comply with required regulations.


## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

Highlight at least two differences between it and your ERD. Would you change anything in yours?
```
Your answer...
```
I could see the following key differences between the AdventureWorks schema and the ERD I provided earlier are:

1. The AdventureWorks schema contains more complex relationships between entities compared to the simpler one-to-many relationships in the ERD I provided. For example, the SalesOrderHeader and SalesOrderDetail tables in AdventureWorks have a one-to-many relationship, but they also have relationships with other tables like Customer, Product, and SalesPerson. These relationships involve multiple tables and may require more complex querying and data management strategies.

2. In some tables of the AdventureWorks schema, composite keys are used, whereas the ERD I provided uses single-column primary keys for simplicity. For instance, the SalesOrderHeader table in AdventureWorks has a composite primary key consisting of SalesOrderID and BusinessEntityID columns. Composite keys can offer more granularity and uniqueness, but they can also add complexity to queries and indexing.

3. AdventureWorks schema involves dbo for error handling however in my ERD its not available. 

Proposed changes to ERD based on the AdventureWorks schema:
   1. If the bookstore's operations were to expand significantly and involve more complex relationships between entities, I might consider revising the ERD to include similar complexities. This could involve introducing composite keys where necessary and refining the relationships between entities to better represent the bookstore's operations and data model. However, for a small-scale operation, the simpler ERD I provided should suffice.
   
   2. We can also add an ErrorLog table within our ERD schema to store information about errors encountered during database operations. The ErrorLog table might include columns such as ErrorID (Primary Key), ErrorDateTime, ErrorMessage, ErrorSeverity, ErrorState, etc. to capture relevant details about each error.


# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `June 1, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
