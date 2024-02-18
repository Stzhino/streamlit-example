import streamlit as st
from mitosheet.streamlit.v1 import spreadsheet
import pandas as pd
import os 

st.set_page_config(layout="wide")
st.write("Please import a .csv file and have it sorted and graphed with mito!!!!!.")

uploaded_files = st.file_uploader("Choose a CSV file", accept_multiple_files=True)
if uploaded_files is not None:
    for uploaded_file in uploaded_files:
        file_name = uploaded_file.name
        target_path = "./import_files/" + file_name  # Specify target folder and filename

        try:
            with open(target_path, "wb") as f:  # Open in binary mode for CSV files
                f.write(uploaded_file.getbuffer())
            st.success("File uploaded successfully: " + file_name)
        except Exception as e:
            st.error(f"Error saving file: {e}")

import_folder = "./import_files"  # Use the folder where you saved the uploaded files
new_dfs, usrdata = spreadsheet(import_folder=import_folder)
st.code(usrdata)