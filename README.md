# Python_Project_VijayR
##Name : Vijay R

import PyPDF2
import tkinter
import os

root=tkinter.Tk()
root.withdraw()

## for Specific file

#file_name= filedialog.askopenfilename()

pdf_folder = r"C:\Users\VIJAY\PycharmProjects\pythonProject\dummy"  #for folder
for x,y,z in os.walk(pdf_folder):
    print("root",x)
    print("dirs",y)
    print("files",z)

output=os.listdir(pdf_folder)

File_size = os.path.getsize(pdf_folder)  #Know about the file size
print(output)
print("File Size is :", File_size, "bytes")

pdf_in_file=open(r"C:\Users\VIJAY\PycharmProjects\pythonProject\dummy",'rb')
inputpdf= PyPDF2.PdfFileReader(pdf_in_file)
pages_no= inputpdf.numPages
output= PyPDF2.PdfFileWriter()

for i in range(pages_no):
    inputpdf= PyPDF2.PdfFileReader(pdf_in_file)

    import random
    import string

## Create random passwords

    def get_random_string(length):

        letters = string.ascii_lowercase
        result_str = ''.join(random.choice(letters) for i in range(length))
        print("Random string of length", length, "is:", result_str)


    get_random_string(8)

    output.addPage(inputpdf.getPage(i))
    output.encrypt(result_str)


    with open("Protectedfile.pdf","wb") as outputStream:
        output.write(outputStream)

## Save the encrypted files in different paths

        path = "C:\Users\VIJAY\PycharmProjects\pythonProject"

        os.chdir(path)

        def read_text_file(file_path):
            with open(file_path, 'r') as f:
                print(f.read())


        for file in os.listdir():

            if file.endswith(".txt"):
                file_path = f"{path}\{file}"

                read_text_file(file_path)

## for timestamp

        from datetime import datetime

        date = datetime.now().strftime("%Y_%m_%d-%I:%M:%S_%p")
        print(date)


pdf_in_file.close()
#delete the input folders

os.remove("C:\Users\VIJAY\PycharmProjects\pythonProject\dummy")


## Create db have a details about the encrypted files

import sqlite3
def My_DB_Execution(query,db):
    connection=sqlite3.connect(db)
    execution=connection.execute(query)
    db_data=execution.fetchall()
    print(db_data)
    connection.commit()
    connection.close()

a = """CREATE TABLE filedetails("file_name"text,"file_size"integer,"time_encryption",%Y_%m_%d-%I:%M:%S_%p)"""
#a="""INSERT INTO filedetails("file_name","file_size","time_encryption")(values(output:file_name,File_size:file_size,date:time_encryption))"""
#a=""" SELECT* FROM filedetails"""

My_DB_Execution(a, db="project.db")

