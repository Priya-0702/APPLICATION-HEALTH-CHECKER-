# APPLICATION-HEALTH-CHECKER-
import requests

def check_application_status(url):
    """
    Checks the uptime of an application by sending an HTTP request and 
    determining if it is 'up' or 'down' based on the status code.

    Args:
        url (str): The URL of the application to check.

    Returns:
        str: 'up' if the application is functioning correctly, 'down' otherwise.
    """
    try:
        response = requests.get(url, timeout=5)
        
        # Check if the response status code is in the range of 200-299 (successful response)
        if 200 <= response.status_code < 300:
            return f"The application at {url} is UP (status code: {response.status_code})."
        else:
            return f"The application at {url} is DOWN (status code: {response.status_code})."
    except requests.exceptions.RequestException as e:
        # Handle network-related errors or timeouts
        return f"The application at {url} is DOWN. Error: {e}"

if __name__ == "__main__":
    # Example URL to check
    
    application_url = "https://play.google.com/store/apps/details?id=com.ril.ajio"
    
    # Check the status of the application
    status = check_application_status(application_url)
    print(status)

    
