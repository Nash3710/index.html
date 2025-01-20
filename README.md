# index.html
import json

def get_course_marks():
    marks = []
    while True:
        try:
            mark = input("Enter course mark (or type 'done' to finish): ")
            if mark.lower() == 'done':
                break
            mark = float(mark)
            if 0 <= mark <= 100:
                marks.append(mark)
            else:
                print("Please enter a valid mark between 0 and 100.")
        except ValueError:
            print("Invalid input. Please enter a number or 'done'.")
    return marks

def calculate_weighted_average(marks, weights):
    if len(marks) != len(weights):
        raise ValueError("Marks and weights must have the same length.")
    weighted_sum = sum(mark * weight for mark, weight in zip(marks, weights))
    total_weight = sum(weights)
    return weighted_sum / total_weight if total_weight > 0 else 0

def display_results(marks, average):
    print("\nFinal Grades:")
    for i, mark in enumerate(marks):
        print(f"Course {i + 1}: {mark}")
    print(f"Weighted Average: {average:.2f}")

def save_results(marks, average):
    results = {
        "marks": marks,
        "average": average
    }
    with open('grades.json', 'w') as f:
        json.dump(results, f)
    print("Results saved to grades.json")

def main():
    print("Welcome to the Student Grade Calculator!")
    
    # Get course marks
    marks = get_course_marks()
    
    # Define weights for each course (for simplicity, we assume equal weights)
    weights = [1] * len(marks)  # You can modify this to have different weights
    
    # Calculate weighted average
    if marks:
        average = calculate_weighted_average(marks, weights)
        display_results(marks, average)
        save_results(marks, average)
    else:
        print("No marks entered.")

if __name__ == "__main__":
    main()
