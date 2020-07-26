### Venv Creation

``cd ~/app
python -m venv env
source env/bin/activate 
``

* This creates a virtual Environment of Python, venv allows package isolation and non interference with development machine. 

`pip install --upgrade pip`

* Update pip as good security measure

* Install required packages.

``pip install pewpew``

* The most popular way is package method, lets take an example of flask app. 
* ├── app
│   ├── __init__.py
│   └── views.py
├── env
├── requirements.txt
└── run.py
* to create requirements, 
* `pip freeze > requirements.txt`

