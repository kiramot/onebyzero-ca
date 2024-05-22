# onebyzero-ca
data engineer technical exam


Overview
This application simulates a transaction processing system that reads transaction data from CSV files in a specified folder and processes it in real-time. The application also provides a REST API to retrieve transaction details and summaries.

Features
Load transaction data: Loads transaction data from CSV files every 5 minutes.
Load product reference data: Loads static product reference data from a CSV file.
API Endpoints: Provides RESTful endpoints to retrieve individual transactions and summaries by product and manufacturing city.
Concurrency: Designed to handle concurrent requests without blocking data processing.
Project Structure
css
Copy code
project-root/
│
├── app/
│   ├── __init__.py
│   ├── api.py
│   ├── data_loader.py
│   └── generate_transactions.py
│
├── reference/
│   └── ProductReference.csv
│
├── transactions/
│   └── [Generated transaction files will be stored here]
│
├── README.md
└── requirements.txt
Installation
Clone the repository:

bash
Copy code
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
Create and activate a virtual environment:

bash
Copy code
python -m venv env
source env/bin/activate   # On Windows, use `env\Scripts\activate`
Install the dependencies:

bash
Copy code
pip install -r requirements.txt
Configuration
Ensure that the transactions and reference folders exist in the project root directory.
Place the ProductReference.csv file inside the reference folder.
The application will generate transaction files inside the transactions folder.
Usage
Generating Transaction Data
To generate transaction data files, use the generate_transactions.py script:

bash
Copy code
python app/generate_transactions.py
This script will create transaction files in the transactions folder with 50 transaction records, each file containing 10 records, and each record is 5 minutes apart.

Running the Application
Start the FastAPI server:

bash
Copy code
uvicorn app.api:app --reload
Access the API Documentation:
Open your browser and navigate to http://127.0.0.1:8000/docs to view the automatically generated API documentation.

API Endpoints
Get Transaction by ID:

http
Copy code
GET /assignment/transaction/{transaction_id}
Retrieve details of a specific transaction by its ID.

Get Transaction Summary by Products:

http
Copy code
GET /assignment/transactionSummaryByProducts/{last_n_days}
Retrieve a summary of transactions by product for the last N days.

Get Transaction Summary by Manufacturing City:

http
Copy code
GET /assignment/transactionSummaryByManufacturingCity/{last_n_days}
Retrieve a summary of transactions by manufacturing city for the last N days.

Concurrency and Scalability
Concurrency: The application uses FastAPI, which is built on top of Starlette and supports asynchronous endpoints, enabling it to handle multiple requests concurrently.
Non-blocking I/O: The transaction loading process runs in a separate thread to ensure that API requests are not blocked by data processing.
Scalability: Designed to handle large volumes of transaction files and high concurrency. Additional scaling can be achieved by deploying the application in a containerized environment and using load balancers.
Error Handling
The API endpoints provide meaningful error messages and HTTP status codes to indicate issues such as missing transactions (404 Not Found).
Logging
The application logs important events, such as loading data and processing transactions, using Python’s built-in logging module. This helps in monitoring and debugging.
Future Improvements
Persistent Storage: Integrate a database for persistent storage of transaction data.
Enhanced Security: Add authentication and authorization for API endpoints.
Monitoring and Alerts: Implement monitoring and alerting for better observability.
