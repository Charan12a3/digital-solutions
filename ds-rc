import os
import PyPDF2
import pandas as pd

# Function to extract details from a single PDF
def extract_invoice_details(pdf_path):
    with open(pdf_path, 'rb') as file:
        pdf_reader = PyPDF2.PdfFileReader(file)
        # Assuming the details are in the first page, adjust if needed
        page = pdf_reader.getPage(0)
        
        # Extracting text (You may need to adjust the text extraction logic based on your invoices)
        text = page.extract_text()
        
        # Extracting specific details (Assuming a simplified scenario)
        invoice_number = extract_specific_detail(text, "Invoice Number")
        invoice_date = extract_specific_detail(text, "Invoice Date")
        gross_amount = extract_specific_detail(text, "Gross Amount")
        net_quantity = extract_specific_detail(text, "Net Quantity")
        total_amount = extract_specific_detail(text, "Total Amount")
        tax_percentage = extract_specific_detail(text, "Tax Percentage")
        
        return {
            "Invoice Number": invoice_number,
            "Invoice Date": invoice_date,
            "Gross Amount": gross_amount,
            "Net Quantity": net_quantity,
            "Total Amount": total_amount,
            "Tax Percentage": tax_percentage,
        }

# Function to extract a specific detail from text (You may need to adjust this based on your invoices)
def extract_specific_detail(text, detail_name):
    # Assuming a simple logic here, adjust based on your invoice structure
    start_index = text.find(detail_name) + len(detail_name)
    end_index = text.find('\n', start_index)
    return text[start_index:end_index].strip()

# Function to update the Daily Invoice Tracker
def update_invoice_tracker(data, tracker_path):
    # Check if the tracker file exists
    if os.path.exists(tracker_path):
        # Read existing data
        tracker_data = pd.read_csv(tracker_path)
    else:
        # Create a new DataFrame if the file doesn't exist
        tracker_data = pd.DataFrame(columns=["Invoice Number", "Invoice Date", "Gross Amount", "Net Quantity", "Total Amount", "Tax Percentage"])
    
    # Append new data to the DataFrame
    tracker_data = tracker_data.append(data, ignore_index=True)
    
    # Write the updated DataFrame back to the tracker file
    tracker_data.to_csv(tracker_path, index=False)

# Directory containing PDF invoices
invoices_directory = "/path/to/invoices"

# Daily Invoice Tracker file path
tracker_file_path = "/path/to/DailyInvoiceTracker.csv"

# Loop through each PDF in the directory
for filename in os.listdir(invoices_directory):
    if filename.endswith(".pdf"):
        pdf_path = os.path.join(invoices_directory, filename)
        
        # Extract details from the current PDF
        invoice_data = extract_invoice_details(pdf_path)
        
        # Update the Daily Invoice Tracker
        update_invoice_tracker(invoice_data, tracker_file_path)

print("Automation completed successfully.")
