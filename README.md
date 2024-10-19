# Morphle-labs

from flask import Flask
import os
import datetime
import subprocess
import pytz

app = Flask(__name__)

@app.route('/htop')
def htop():
    # Get the full name (hardcode it)
    full_name = "Your Full Name"
    
    # Get the system username
    system_username = os.getlogin()
    
    # Get the server time in IST
    ist = pytz.timezone('Asia/Kolkata')
    server_time_ist = datetime.datetime.now(ist).strftime("%Y-%m-%d %H:%M:%S")
    
    # Get the output of top command
    top_output = subprocess.getoutput("top -b -n 1")
    
    # Format the response
    response = f"""
    <h1>Server Information</h1>
    <p><b>Name:</b> {full_name}</p>
    <p><b>Username:</b> {system_username}</p>
    <p><b>Server Time (IST):</b> {server_time_ist}</p>
    <pre><b>TOP Output:</b><br>{top_output}</pre>
    """
    
    return response

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
