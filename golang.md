# Go

## 2025-09-08

concurrency in go is pretty useful and straight forward. capitlization matters in structs (caps = public, uncap = private)

```go
package main

import (
	"fmt"
	"pluralsight-jeff/faculty"
	"strconv"
	"strings"
	"time"
)

// Gradebook holds a student's name and score.
type Gradebook struct {
	Name  string
	Score int
}

// demonstratePointers shows how pointers work in Go.
func demonstratePointers(name string, otherName *string) {
	name = "bob"
	*otherName = "Slim Cashmore"
}

// demonstrateConcurrency shows how goroutines and channels work.
func demonstrateConcurrency() {
	ch1, ch2 := make(chan string), make(chan string)

go func() {
		ch1 <- "Hello from a goroutine 1!"
	}()
	go func() {
		ch2 <- "Hello from a goroutine 2!"
	}()

	time.Sleep(10 * time.Millisecond)

	select {
	case msg := <-ch1:
		fmt.Println(msg)
	case msg := <-ch2:
		fmt.Println(msg)
	default:
		fmt.Println("No message received")
	}
}

// gradebookApp runs the interactive gradebook program.
func gradebookApp() {
	fmt.Println("Welcome to the gradebook program!")
	fmt.Println()
	fmt.Println(strings.Repeat("=", 50))
	fmt.Println()

	var gradebook []Gradebook
	var choice string
	var option int
	shouldContinue := true

	for shouldContinue {

		fmt.Println("Please pick an option:")
		fmt.Println("1. Add entry into gradebook")
		fmt.Println("2. View all entries")
		fmt.Println("3. Exit")
		fmt.Scanln(&choice)
		option, _ = strconv.Atoi(choice)
		fmt.Println()

		switch option {
		case 1:
			var studentName, rawScore string
			var score int
			fmt.Println("Enter name and score:")
			fmt.Scanln(&studentName, &rawScore)
			score, _ = strconv.Atoi(rawScore)
			gradebook = append(gradebook, Gradebook{Name: studentName, Score: score})
		case 2:
			fmt.Println()
			fmt.Println("Current entries in the gradebook:")
			for _, entry := range gradebook {
				fmt.Printf("Student %s earned a %d\n", entry.Name, entry.Score)
			}
			fmt.Println()
		case 3:
			fmt.Println("Exiting the program. Goodbye!")
			shouldContinue = false
		default:
			fmt.Println("Invalid option. Please try again.")
		}
	}
}

// demonstrateFaculty shows how to import and use a struct from another package.
func demonstrateFaculty() {

teacher := faculty.Teacher{
		Name:           "John Doe",
		Subject:        "Computer Science",
		EducationLevel: "PhD",
	}

	fmt.Printf("Teacher: %s, Subject: %s, Education: %s\n", teacher.Name, teacher.Subject, teacher.EducationLevel)
}

func main() {
	// Run the gradebook application
	gradebookApp()

	// Demonstrate pointers
	fmt.Println()
	fmt.Println(strings.Repeat("=", 50))
	fmt.Println("Demonstrating Pointers:")
	name := "John"
	otherName := "Jane"
	demonstratePointers(name, &otherName)
	fmt.Println("Original name variable:", name)
	fmt.Println("Modified otherName variable (via pointer):", otherName)

	// Demonstrate concurrency
	fmt.Println()
	fmt.Println(strings.Repeat("=", 50))
	fmt.Println("Demonstrating Concurrency:")
	demonstrateConcurrency()

	// Demonstrate importing from another package
	fmt.Println()
	fmt.Println(strings.Repeat("=", 50))
	fmt.Println("Demonstrating Importing Packages:")
	demonstrateFaculty()
}
```
