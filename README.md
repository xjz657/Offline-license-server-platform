# Offline-license-server-platform
Establish an offline CDKEY verification web background for a web application deployable in Ubuntu.
In order to cooperate with other WEB applications, it provides a trial (such as: 30 days, can be modified) function for a period of time.
Users use HTTP method to contact the web background. Users can query the current activation status through the HTTP API interface.
If it is not activated, the user needs to input a CDKEY.
If the decrypted and re-verified CDKEY is valid, the used CDKEY (anti-replay attack) and the valid date of the current trial CDKEY are recorded.
If another valid CDKEY is activated during the validity period, the valid date accumulates.
CDKEY is a combination of letters and numbers, not too long to affect the user experience.

This platform uses Django framework development
The language used is: python 3.5.2rc1
Database: MySQL
System: Ubuntu 16.04

Directory Structure:
  Project: LicenseServer
  Main directory:         LicenseServer
  Settings.py:            configuration of the entire project
  Urls.py:                routing
  App directory:          functions
  Models.py:              orm class is used to generate data tables
  Views.py:               request response function
  Static file directory:  static
  Html file directory:    templates

Create a database:        create_database.py
Create a registered user: create_user.py
Generate CDKEY code:      produce_cdkey.py

Start the hypervisor:     manage.py


Install before you run the project Pip3(18.1) and MySQL database,
then use pip3 to install the module:
Pycryptodome 3.7.2
Jsonpickle 1.0
PyMySQL 0.9.2
Django 2.1.3

MySQL password user: root, password: 123,
If you need to modify it, modify it together in create_database.py, create_user.py, produce_cdkey, LicenseServer/settings.py
(Some of the database does not support Chinese input initially, so I changed it to a letter, unlike the Chinese in the picture)

Encryption module: Python + js is encrypted by the RSA algorithm, and the public and private keys are generated in the need_rsa method and the need_rsa_nocdkey method in views.py.
The public key is passed to the front end for encryption and the private key is used for decryption at the back end.
The front-end encryption is done in rsa.js and rsa_nocdkey.js, which is the JSEncrypt encryption method.

The entire platform, after the above conditions are ready, submit the script to run in the main directory: sh start.sh
In the browser input: server ip address: (opened in Google Chrome)
Such as 120.79.192.192:8000, 120.79.192.192:8000/, 120.79.192.192:8000/index/etc.

Notes: 
1. If sh start.sh fails, you can try to submit using sh start_err.sh
2. script submission, after the end of Ctrl+C, you can use
   Python3 manage.py runserver 0.0.0.0:8000 --insecure
   Run the program again
3. Open with Google Chrome
