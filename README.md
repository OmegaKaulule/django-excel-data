# django-excel-data


This script automates the process of adding products to an inventory management system by reading data from an Excel file (Inventory.xlsx) and submitting it to a Django-based web application through a POST request.

Requirements
Python 3.x
The following Python libraries are required:
requests: To handle HTTP requests.
openpyxl: To read Excel files.
beautifulsoup4: For parsing HTML and extracting CSRF tokens.
re: For cleaning and extracting numeric values.
You can install the required packages using pip:

bash
Copy code
pip install requests openpyxl beautifulsoup4
File Structure
Inventory.xlsx: The Excel file containing the product data to be uploaded.
Columns:
Product Name: The name of the product.
Category: The product category.
Cost: The cost of the product.
Price: The selling price of the product.
Quantity: The quantity of the product in stock.
Serial Number: The serial number of the product.
Description: A description of the product.
How It Works
Read Excel File: The script loads product data from the specified Excel file using openpyxl.

Session Handling: It opens a session with the web server and retrieves the CSRF token required for form submissions.

Product Categories: The script fetches available categories from the product form page and maps them for validation.

Data Cleaning:

Numeric values in the "Cost", "Price", and "Quantity" columns are cleaned using regular expressions to ensure they are valid.
Invalid rows are skipped, and errors are logged.
Form Submission: For each valid row in the Excel file:

If the product category exists on the server, it is used directly.
If the category is new, it is added as a new category in the submission.
The script posts the product data to the web server.
Error Handling:

Successful submissions are logged.
Server errors (HTTP status 500) and other failures are logged with the appropriate status code.
Usage
Set the Excel File Path: Update the path of the Excel file (excel_file_path) to point to your local file.

python
Copy code
excel_file_path = 'C:/Users/User/Desktop/Inventory.xlsx'
Set the URL: Update the url variable to point to the URL of the form submission page of your Django web application.

python
Copy code
url = 'https://example.com/newproduct/'
Run the Script: Execute the script from the terminal or an IDE.

bash
Copy code
python upload_inventory.py
Output:

The script prints messages to the console based on the success or failure of each product submission.
For successful submissions, it prints:
javascript
Copy code
Successfully added product: <Product Name>
For server errors, it prints:
arduino
Copy code
Server error while adding product: <Product Name>
For other failures (like a 403 Forbidden error), it prints:
less
Copy code
Failed to add product: <Product Name>, Status code: <Status Code>
Customization
CSRF Token Handling: The script uses BeautifulSoup to extract the CSRF token from the form. If your Django form has a different setup, you might need to adjust the line extracting the CSRF token:

python
Copy code
csrf_token = soup.find('input', {'name': 'csrfmiddlewaretoken'})['value']
Error Handling: You can customize how errors are handled. Currently, the script skips rows with invalid data and prints an error message.

python
Copy code
print(f"Skipping invalid row due to error: {e}")
Limitations
Network Dependency: The script relies on network connectivity to access the web server and submit forms.
Server-Side Validation: The script assumes that the server will properly handle errors and return appropriate status codes (200 for success, 500 for server errors).
Excel Formatting: Ensure that your Excel file is correctly formatted with numeric values where required (e.g., cost, price, quantity).
License
This script is provided "as-is" with no warranties. Modify and use it at your own risk.
