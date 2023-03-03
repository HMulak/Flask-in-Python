# Flask-in-Python
Setting up a Flask Application

# Using the json file and python code here, set up a flask application to recieve: 1 GET call, returning the name of a customer given the customer email; 1 POST call, changing the name of an existing customer given the name and email.

#Flask Example

import json
from flask import Flask,request

app = Flask(__name__, template_folder='')
app.config['TEMPLATES_AUTO_RELOAD'] = True

@app.route('/hello_world', methods=["GET"])
def hell_world():
    return "Hello World"

@app.route('/get_data', methods=["GET"])
def get_data():
  with open('flask_data.json') as f:
    data = json.load(f)
  return data
  
@app.route('/post_data', methods=["POST"])
def post_data():
  email = request.args.get('email')
  name = request.args.get('name')
  with open('flask_data.json') as f:
    data = json.load(f)
  data[email] = name
  with open('flask_data.json', 'w') as f:
    json.dump(data, f)
  return data
  
if __name__ == "__main__":
  app.run()
  
#Code:
  
import requests
import json
email = input("What's the customer email? ")
name = input("And their name? ")
url = 'http://127.0.0.1:5000/post_data?email='+ email + '&name=' + name
resp = requests.post(url)
weather = resp.json()
