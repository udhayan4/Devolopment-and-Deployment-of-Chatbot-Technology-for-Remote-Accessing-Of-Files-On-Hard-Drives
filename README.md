import requests

import uipath_api_python

Authenticate to UiPath RPA:

uipath = uipath_api_python.UiPathAPI(

    tenant_logical_name="<TENANT_LOGICAL_NAME>",

    client_id="<CLIENT_ID>",

    client_secret="<CLIENT_SECRET>",

    username="<USERNAME>",

    password="<PASSWORD>")

Get the files from PC or laptop:

def get_files(folder_path):

    file_list = []

    #by Using requests library to retrieve the list of files from PC or laptop

    response = requests.get("http://<PC_OR_LAPTOP_IP>/files?folder_path=" + folder_path)

    if response.status_code == 200:

        file_list = response.json()

    return file_list

#function is called to retrieve the list of files

files = get_files("C:\MyFiles")

Start a UiPath process to retrieve the files from the memory:

def retrieve_files(file_list):

    #UiPath process to retrieve the files

    uipath.start_process("RetrieveFiles", {"files": file_list})

#Calling the function to start the UiPath process

retrieve_files(files)

