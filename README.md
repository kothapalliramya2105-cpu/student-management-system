# student-management-system
A Python-based Student Management System for managing student records using file handling and CRUD operations.
#code
import os

FILE_NAME = "students.txt"

def add_student():
    name = input("Enter Student Name: ")
    roll = input("Enter Roll Number: ")
    course = input("Enter Course: ")

    with open(FILE_NAME, "a") as file:
        file.write(f"{roll},{name},{course}\n")

    print("Student Added Successfully!")

def view_students():
    if not os.path.exists(FILE_NAME):
        print("No Records Found.")
        return

    with open(FILE_NAME, "r") as file:
        data = file.readlines()

    print("\nStudent Records")
    print("---------------------------")

    for student in data:
        roll, name, course = student.strip().split(",")
        print(f"Roll No: {roll}")
        print(f"Name    : {name}")
        print(f"Course  : {course}")
        print("---------------------------")

def search_student():
    roll = input("Enter Roll Number: ")

    found = False

    with open(FILE_NAME, "r") as file:
        for student in file:
            r, name, course = student.strip().split(",")

            if r == roll:
                print("\nStudent Found")
                print("Name:", name)
                print("Course:", course)
                found = True

    if not found:
        print("Student Not Found.")

def delete_student():
    roll = input("Enter Roll Number: ")

    students = []

    with open(FILE_NAME, "r") as file:
        students = file.readlines()

    with open(FILE_NAME, "w") as file:
        for student in students:
            r, name, course = student.strip().split(",")

            if r != roll:
                file.write(student)

    print("Record Deleted Successfully.")

while True:

    print("\n===== Student Management System =====")

    print("1. Add Student")
    print("2. View Students")
    print("3. Search Student")
    print("4. Delete Student")
    print("5. Exit")

    choice = input("Enter Choice: ")

    if choice == "1":
        add_student()

    elif choice == "2":
        view_students()

    elif choice == "3":
        search_student()

    elif choice == "4":
        delete_student()

    elif choice == "5":
        print("Thank You")
        break

    else:
        print("Invalid Choice")
