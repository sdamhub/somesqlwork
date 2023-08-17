
""""
#The top part of the code

import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="#put your username, most users will have this as 'root''",
    passwd="#put your password here",
    database="malp"
)

"""



""""
This creates the database
mycursor.execute("CREATE DATABASE malp")
"""

"""
mycursor.execute("SHOW DATABASES")
for db in mycursor:
    print(db)
"""

"""
#This creates the content of the table already created
mycursor.execute("CREATE TABLE students (name VARCHAR(255), age INTEGER(10))")
"""

"""
#This shows the table that has been created
mycursor.execute("SHOW TABLES")

for tb in mycursor:
    print(tb)
"""

"""
#This adds a single student name to the database
sqlFormula = "INSERT INTO students (name, age) VALUES (%s, %s)"
student1 = ("John", 18)

mycursor.execute(sqlFormula, student1)
mydb.commit()
"""

"""
# This adds many students to the database
sqlFormula = "INSERT INTO students (name, age) VALUES (%s, %s)"
students = [("John", 18),
            ("James", 19),
            ("Rice", 17),
           ("Wood", 16),
           ("Luke", 18)
]
mycursor.executemany(sqlFormula, students)
mydb.commit() #This ensures it is saved in the database
# Also when you make a change to the database table, you
#need to use databasename.commit() command to save it
"""

"""
# Running a select command that will display all the names in the database
# row by row
mycursor.execute("SELECT * FROM students")
myresult = mycursor.fetchall()

for row in myresult:
    print(row)
"""

"""
# Running a select command that will display specific detail such as age
# in the database row by row
mycursor.execute("SELECT age FROM students")
myresult = mycursor.fetchall()

for row in myresult:
    print(row)
"""

"""
# Running a select command that will display specific detail such as age
# in the first database row
mycursor.execute("SELECT age FROM students")
myresult = mycursor.fetchone()

for row in myresult:
    print(row)
"""

"""
# updating a value in the table

sql = "UPDATE students SET age = 13 WHERE name = 'wood'"
mycursor.execute(sql)
mydb.commit()

"""

"""
# This limits what is displayed

mycursor = mydb.cursor()
mycursor.execute("SELECT * FROM students LIMIT 5")
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

"""
# This limits what is displayed and the display begins from a certain row

mycursor = mydb.cursor()
mycursor.execute("SELECT * FROM students LIMIT 5 OFFSET 2")
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

"""
# This limits what is displayed using the WHERE command

mycursor = mydb.cursor()
sql = "SELECT * FROM students WHERE age = 17" # you can also use WHERE name = wood
mycursor.execute(sql)
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

"""
# This limits what is displayed using the WHERE command
# and you want values that have a particular phrase in them

mycursor = mydb.cursor()
sql = "SELECT * FROM students WHERE name LIKE 'ri%'"
mycursor.execute(sql)
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

"""
# This limits what is displayed using the WHERE command
# and prevents sql injections

sql = "SELECT * FROM students WHERE name = %s" #%s serves as a placeholder
mycursor.execute(sql, ("wood", ))
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

# This display the result in ascending order

sql = "SELECT * FROM students ORDER BY name"
mycursor.execute(sql)
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

# This display the result in descending order

sql = "SELECT * FROM students ORDER BY name DESC"
mycursor.execute(sql)
myresult = mycursor.fetchall()

for result in myresult:
    print(result)
"""

# This deletes an entry, where you have double,
#it deletes the first on the table

sql = "DELETE FROM students WHERE name = 'john'"
mycursor.execute(sql)
mydb.commit()

"""

"""

# This deletes a table

sql = "DROP TABLE IF EXISTS students"
mycursor.execute(sql)
mydb.commit()

"""