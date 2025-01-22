students = {}
subjects = {}
marks = {}

def add_student(student_id, name, roll_number, dob):
    students[student_id] = {"name": name, "roll_number": roll_number, "dob": dob}
    marks[student_id] = {}
    print(f"Student {name} added successfully.")

def update_student(student_id, name=None, roll_number=None, dob=None):
    if student_id in students:
        if name:
            students[student_id]["name"] = name
        if roll_number:
            students[student_id]["roll_number"] = roll_number
        if dob:
            students[student_id]["dob"] = dob
        print(f"Student {student_id} updated successfully.")
    else:
        print(f"Student ID {student_id} not found.")

def delete_student(student_id):
    if student_id in students:
        del students[student_id]
        del marks[student_id]
        print(f"Student ID {student_id} deleted successfully.")
    else:
        print(f"Student ID {student_id} not found.")

def add_subject(subject_id, subject_name):
    subjects[subject_id] = subject_name
    print(f"Subject {subject_name} added successfully.")


def input_marks(student_id, subject_id, mark):
    if student_id not in students:
        print(f"Student ID {student_id} not found.")
        return
    if subject_id not in subjects:
        print(f"Subject ID {subject_id} not found.")
        return
    
    marks[student_id][subject_id] = mark
    print(f"Marks for {students[student_id]['name']} in {subjects[subject_id]} updated.")

def calculate_total_marks(student_id):
    if student_id not in marks:
        return 0
    return sum(marks[student_id].values())

def calculate_grade(total_marks):
    if total_marks >= 90:
        return 'A+'
    elif total_marks >= 80:
        return 'A'
    elif total_marks >= 70:
        return 'B+'
    elif total_marks >= 60:
        return 'B'
    elif total_marks >= 50:
        return 'C'
    else:
        return 'F'


def generate_report_card(student_id):
    if student_id not in students:
        print(f"Student ID {student_id} not found.")
        return

    student = students[student_id]
    student_marks = marks.get(student_id, {})
    total_marks = calculate_total_marks(student_id)
    grade = calculate_grade(total_marks)

    print("\nReport Card")
    print(f"Name: {student['name']}")
    print(f"Roll Number: {student['roll_number']}")
    print(f"Date of Birth: {student['dob']}")
    print("-" * 20)
    for subject_id, mark in student_marks.items():
        print(f"{subjects[subject_id]}: {mark}")
    print("-" * 20)
    print(f"Total Marks: {total_marks}")
    print(f"Grade: {grade}")
    print("-" * 20)

def class_performance():
    print("\nClass Performance")
    print("-" * 20)
    for student_id, student_data in students.items():
        total_marks = calculate_total_marks(student_id)
        grade = calculate_grade(total_marks)
        print(f"{student_data['name']} ({student_data['roll_number']}): Total Marks = {total_marks}, Grade = {grade}")
    print("-" * 20)


add_student(1, "prajwal", "08", "2005-02-28")
add_student(2, "mitesh", "1002", "2004-11-20")

add_subject(1, "Math")
add_subject(2, "Science")

input_marks(1, 1, 85)  
input_marks(1, 2, 92)  
input_marks(2, 1, 76)  

generate_report_card(1)  
class_performance() 
