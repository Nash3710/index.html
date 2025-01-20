<!DOCTYPE html>
<html>
<head>
    <title>Student Grade Calculator</title>
    <script>
        function getCourseMarks() {
            const marks = [];
            let mark;
            while (true) {
                mark = prompt("Enter course mark (or type 'done' to finish):");
                if (mark.toLowerCase() === 'done') {
                    break;
                }
                mark = parseFloat(mark);
                if (!isNaN(mark) && mark >= 0 && mark <= 100) {
                    marks.push(mark);
                } else {
                    alert("Please enter a valid mark between 0 and 100.");
                }
            }
            return marks;
        }

        function calculateWeightedAverage(marks, weights) {
            if (marks.length !== weights.length) {
                throw new Error("Marks and weights must have the same length.");
            }
            const weightedSum = marks.reduce((sum, mark, index) => sum + mark * weights[index], 0);
            const totalWeight = weights.reduce((sum, weight) => sum + weight, 0);
            return totalWeight > 0 ? weightedSum / totalWeight : 0;
        }

        function displayResults(marks, average) {
            let results = "\nFinal Grades:\n";
            marks.forEach((mark, index) => {
                results += `Course ${index + 1}: ${mark}\n`;
            });
            results += `Weighted Average: ${average.toFixed(2)}`;
            alert(results);
        }

        function saveResults(marks, average) {
            const results = {
                marks: marks,
                average: average
            };
            const jsonResults = JSON.stringify(results);
            console.log("Results saved to console as:", jsonResults);
        }

        function main() {
            alert("Welcome to the Student Grade Calculator!");

            // Get course marks
            const marks = getCourseMarks();

            // Define weights for each course (for simplicity, we assume equal weights)
            const weights = new Array(marks.length).fill(1);  // You can modify this to have different weights

            // Calculate weighted average
            if (marks.length > 0) {
                const average = calculateWeightedAverage(marks, weights);
                displayResults(marks, average);
                saveResults(marks, average);
            } else {
                alert("No marks entered.");
            }
        }
    </script>
</head>
<body onload="main()">
</body>
</html>
